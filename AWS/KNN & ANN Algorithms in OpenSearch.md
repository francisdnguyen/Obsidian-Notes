
## The Basic k-NN Problem
- Given a set of points and a query, find the *k* nearest points in the set to the query.
- **Naive/exact solution**: compute the distance from the query to every point, keep the top *k*.
- Runtime complexity: O(N log k), where N = number of vectors. Fine at thousands of points, becomes a real bottleneck at millions+.
- Exact k-NN algorithms that try to speed this up still tend to degrade to naive-like performance in high dimensions (this is the "curse of dimensionality" — distance metrics get less discriminative as dimension count grows).
## k-NN as a Classical ML Algorithm (Wikipedia) vs. k-NN Search (OpenSearch)

### The Original Algorithm (Fix & Hodges, 1951)
- k-NN is fundamentally a **supervised learning** method for **classification** or **regression** — it predicts a label or value for a new data point based on its k nearest labeled neighbors.
- **Classification**: majority vote among the k nearest neighbors' class labels.
- **Regression** (a.k.a. nearest neighbor smoothing): average of the k nearest neighbors' values.
- **No explicit training phase** — the "training" step is just storing the labeled data. All computation happens at prediction/query time (this is why it's called "lazy learning").

### Choosing k
- Larger k reduces noise sensitivity but blurs decision boundaries between classes.
- For binary classification, odd k avoids tied votes.
- k=1 is a special case called the nearest neighbor / nearest neighbor interpolation algorithm.

### The Curse of Dimensionality
- In high-dimensional space, Euclidean distance becomes less meaningful — nearly all points end up roughly equidistant from the query, since points concentrate near the surface of a hypersphere rather than clustering meaningfully in the volume.
- This is directly why dimension reduction (PCA, LDA) is often applied before k-NN in classic ML, and why OpenSearch's ANN algorithms (HNSW/IVF) exist — high-dimensional exact search is both slow *and* less meaningful on raw distance alone.

### Weighting and Feature Scaling
- Neighbors can be weighted by inverse distance (closer neighbors count more) rather than equal votes.
- Feature scaling/normalization matters a lot — if features are on different scales/units, distance calculations get distorted toward whichever feature has the largest raw magnitude.

## The Key Distinction to Keep Straight
- **Wikipedia's k-NN** = a full ML algorithm that predicts labels/values by voting/averaging over neighbors — used for tasks like classification.
- **OpenSearch's "k-NN search"** = repurposes the *nearest-neighbor retrieval* half of this idea as a general-purpose similarity search primitive — it just returns the k closest vectors, with no voting or label prediction involved. It's retrieval, not prediction.
- This is exactly why Verbatim's use of k-NN (via pgvector) isn't "classifying" anything — it's using nearest-neighbor search purely to retrieve the most relevant chunks for a RAG query. Different goal, same underlying distance-based mechanism.

## Why Approximate Nearest Neighbor (ANN) Search
- ANN trades exactness for speed by loosening constraints:
  - Allow indexing to take longer
  - Allow more memory at query time
  - Return an *approximation* of the true k-NN (not guaranteed exact)
- This tradeoff is why "recall" becomes a key metric — recall@10 = fraction of the true top-10 neighbors actually found in the approximate result.

## HNSW (Hierarchical Navigable Small Worlds)
- Graph-based ANN algorithm — one of the most popular, best latency-vs-recall tradeoff, no training required.
- **Core idea**: builds a graph connecting nearby vectors; search partially traverses this graph, always moving to the closest candidate to the query.
- **Hierarchy of graphs**: all vectors are in the bottom layer; a random subset bubbles up to each layer above (like a skip list). Search starts at the top layer (sparse, fast to traverse) to find a good starting point, then works down to the bottom layer (dense, precise) for the actual k-NN result.
- **Tunable parameters**:
  - `m` — max edges per vector in the graph. Higher = more memory, better recall.
  - `ef_construction` — candidate queue size when inserting a node. Higher = slower indexing, better graph quality.
  - `ef_search` — candidate queue size during search traversal. Higher = slower search, better recall.
- **Memory cost**: roughly `1.1 * (4*d + 8*m) * num_vectors` bytes (before replication). At billion-vector scale with typical settings, this reaches **~1.4 TB+** — HNSW is the most memory-hungry of the three options.

## IVF (Inverted File System)
- Bucket-based ANN algorithm (Faiss implementation) — this is the family Verbatim's `IVFFlat` pgvector index belongs to.
- **Core idea**: split vectors into buckets, each with a representative vector (a centroid). A vector gets assigned to the bucket with the closest centroid. At search time, only a subset of buckets gets searched — not the whole index.
- **Requires a training step**: k-Means clustering runs on training data to produce the bucket centroids.
- **Tunable parameters**:
  - `nlist` — number of buckets. More buckets = longer training, finer granularity.
  - `nprobes` — number of buckets searched per query. More = slower but better recall.
- **Memory cost**: lower than HNSW — no per-vector edge list to store. Same billion-vector case: **~1.1 TB**, vs. HNSW's higher figure, at the cost of a worse latency/recall tradeoff.

## Product Quantization (PQ) — a compression technique, not a standalone algorithm
- Used *alongside* IVF (or HNSW) to shrink memory footprint further, at the cost of accuracy.
- **Core idea**: break each vector into `m` sub-vectors, encode each sub-vector as an ID into a lookup table (built via k-Means during training) instead of storing raw floating-point values.
- Example from the blog: a 1024-dim vector normally taking 4,096 bytes can shrink to ~8 bytes with `m=8`, `code_size=8` — a massive compression ratio, at the cost of losing information (lossy compression).
- **Memory cost**: dramatically lower — the blog's billion-vector IVFPQ example used **~70 GB** vs. HNSW's 1,400+ GB.

## The Actual Tradeoff (from AWS's own billion-vector benchmark)
| | HNSW | IVFPQ |
|---|---|---|
| Recall@10 | up to 0.99 | up to ~0.61 |
| Query latency (p50) | 9–104 ms | 75–163 ms |
| Memory | ~1,180–2,055 GB | ~68–114 GB |
| Relative cluster cost | ~$75/hr | ~$11/hr |

- **HNSW**: best recall and latency, by far the most expensive in memory and infrastructure cost.
- **IVFPQ**: dramatically cheaper, but noticeably worse recall — roughly 40-60% worse in this benchmark.
- There's no universal "best" choice — it depends on your accuracy requirements, latency budget, and cost constraints.

## Setting Up k-NN in OpenSearch
1. **Create an index with a `knn_vector` field**, specifying the algorithm (`hnsw` or `ivf`), the distance function (`space_type`: `l2` for Euclidean, or cosine/inner product), and algorithm parameters.
2. **For IVF/PQ specifically**, you must first train a model via the training API (since these need k-Means-derived centroids), pointing at a training index/field with vectors of the target dimension.
3. **Ingest documents** via the bulk API, each with its vector field populated.
4. **Query** using a `knn` query type, specifying the query vector and `k`.

## Connection to Verbatim
- Verbatim's `IVFFlat` pgvector index is conceptually identical to OpenSearch's IVF — same bucket/centroid approach, same `nlist`/`nprobes`-style tuning knobs (pgvector calls it `lists`/`probes`).
- Verbatim doesn't use PQ-style compression — at portfolio scale (thousands, not billions, of chunks), the memory savings wouldn't matter, so skipping it was the right call.
- If Verbatim ever needed to scale to a much larger corpus, this benchmark data gives a concrete way to reason about the HNSW-vs-IVF decision rather than guessing.