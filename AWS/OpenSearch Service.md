## What Is Amazon OpenSearch Service
- A managed retrieval engine built on OpenSearch for agentic AI, search, and analytics.
- Combines vector, lexical, hybrid, and agentic retrieval in a single system, delivering low-latency, highly relevant results at petabyte scale.
- Native AI/ML capabilities enable embedding generation, inference, and agentic workflows directly within the service.
- Integrates with Amazon Bedrock and third-party models to accelerate AI development.

## Core Features
- **Serverless** — instant scale up and scale to zero, no infrastructure to manage, no idle costs.
- **Vector database** — scalable, secure, high-performance vector database for vector-driven search and enterprise AI applications.
- **Observability** — analyze logs, traces, and metrics through unified dashboards with built-in anomaly detection and automated alerting.

## Benefits
- **Integrated retrieval for any use case** — combines lexical, vector, and hybrid retrieval in one system, with indexing strategies like HNSW and IVF, and vector quantization to balance accuracy/latency/cost. Agentic search orchestrates multi-step retrieval workflows that adapt dynamically to queries.
- **Accelerate AI development** — AWS handles backups, patching, monitoring, cluster maintenance. OpenSearch Serverless eliminates capacity planning with automatic scaling.
- **Flexibility without tradeoff** — built on open-source OpenSearch (Linux Foundation project, 1.7+ billion downloads, 3,000+ contributors). No single-vendor dependency; start locally, then move to the managed service for production.
- **Operate at scale with confidence** — intelligent tiering manages data across storage tiers by access pattern; memory- or disk-optimized vector search configs balance performance/cost. 99.99% availability with Multi-AZ deployments and automatic failover.

## Use Cases
- **RAG for agentic/generative AI** — improves LLM response accuracy/relevance by using OpenSearch as a knowledge base (this is the Verbatim use case, essentially).
- **Vector database for semantic/multimodal search** — store/search high-dimensional vectors across text, image, audio, video at scale; integrates with Bedrock/SageMaker/third-party models.
- **Intuitive/personalized search** — lexical + vector + hybrid retrieval with ML-powered relevance tuning (e-commerce, media, enterprise).
- **Real-time logs and observability** — centralize/analyze security and observability data for real-time threat detection and incident management.

## Core Concepts (mapped to what Verbatim already does)

### Index, Document, Shard
- An **index** is like a database/table — a named collection of documents.
- A **document** is a single JSON record (in a vector search context, this is roughly your "chunk" — analogous to a row in your `pgvector` table).
- A **shard** is how an index is split across nodes for scalability — this is the distributed-systems piece pgvector on a single Postgres instance doesn't give you out of the box.

### Lexical vs. Vector vs. Hybrid Search
- **Lexical search** — traditional keyword/text matching (like classic full-text search).
- **Vector search** — semantic similarity search over embeddings (what Verbatim does with pgvector + cosine distance).
- **Hybrid search** — combines both, so exact keyword matches and semantic matches both contribute to ranking — something pgvector alone doesn't do natively, but OpenSearch supports built-in.

### HNSW and IVF (indexing strategies for vector search)
- **HNSW (Hierarchical Navigable Small World)** — a graph-based index for approximate nearest neighbor search; generally faster query performance, higher memory usage.
- **IVF (Inverted File Index)** — clusters vectors into buckets and searches only relevant clusters; this is the same family of approach as the **IVFFlat** index already used in Verbatim's pgvector setup.
- Choosing between them is a recall/speed/memory tradeoff — exactly the kind of decision already made (if informally) when picking IVFFlat for Verbatim.

### Why This Matters for the Roadmap
- OpenSearch is essentially AWS's managed, distributed alternative to running your own pgvector-on-Postgres setup — same underlying problem (store embeddings, do nearest-neighbor search), but built to scale further and integrate more tightly with the rest of AWS (S3, Bedrock, Lambda).
## Setting Up OpenSearch in AWS

1. **Sign in to the OpenSearch console** — Search "OpenSearch Service" in the AWS Console. Same region-scoping as other services — confirm you're in the intended region.
2. **Choose Managed Cluster vs. Serverless**:
   - **Managed cluster** — you provision instance types/counts, more control, closer to a traditional cluster.
   - **Serverless** — no capacity planning, scales automatically. Better fit for a portfolio-scale project (e.g. Verbatim). Simpler on-ramp for learning.
3. **Create a collection (Serverless) or domain (Managed)** — For Serverless: create a collection, set type to "Vector search." For Managed: create a domain, choose instance types, configure storage. Name it identifiably (e.g. `verbatim-vectors-test`).
4. **Configure access policy (IAM)** — Same pattern as every other AWS service: define who/what (your account, a Lambda function, etc.) can read/write via an access policy attached to the collection/domain.
5. **Create an index with a vector field mapping** — Define the index and its `knn_vector` field: specify embedding dimension (e.g. 1536 to match OpenAI's `text-embedding-3-small`, same as Verbatim), indexing method (HNSW or IVF), and similarity metric (cosine, etc.). This is the direct equivalent of creating a pgvector column + index in Postgres.
6. **Test with a sample document** — Use the OpenSearch Dashboards Dev Tools console (built into the service) to manually index a test document with a sample vector and run a k-NN query against it, confirming setup works before wiring into code.
7. **Connect from Python with `opensearch-py`**:
```bash
   pip install opensearch-py
```
   Works like boto3 for other services — create a client pointed at your domain/collection endpoint, then:
```python
   client.index(...)   # add documents
   client.search(...)  # knn query to retrieve nearest neighbors
```
   This would replace the raw SQL `pgvector` queries Verbatim currently runs against Postgres.