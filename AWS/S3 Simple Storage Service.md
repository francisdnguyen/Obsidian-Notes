## What is Amazon S3?
- An object storage service offering industry-leading scalability, data availability, security, and performance.
- Cost-effective storage classes and easy-to-use management features let you optimize costs, organize/analyze data, and configure fine-tuned access controls for business and compliance requirements.

## Core Data Model
- **Bucket** — a container with a globally unique name (unique across *all* AWS accounts, not just yours)
- **Object** — the actual data stored, identified by a **key** (looks like a file path, e.g. `uploads/resume.pdf`)
  - S3 has no real folder hierarchy — it's a flat namespace; the `/` in keys is just a string convention
- **Region** — each bucket lives in one AWS region (matters for latency/compliance)

## Benefits

### Scalability
- Store virtually any amount of data, up to exabytes, with unmatched performance.
- Fully elastic — automatically grows/shrinks as you add/remove data.
- No need to provision storage; pay only for what you use.

### Durability and Availability
- Most durable storage in the cloud, industry-leading availability.
- **Durability: 99.999999999%** (11 nines) — will the data survive over time
- **Availability: 99.99%** — can you access it right now
- These are two distinct metrics — don't conflate them.

### Security and Data Protection
- Secure, private, and encrypted by default.
- Supports numerous auditing capabilities to monitor access requests.
- Access controlled via three mechanisms: **IAM policies**, **bucket policies**, **ACLs**.
- Common real-world mistake: misconfigured bucket policies leading to accidentally public buckets.

### Lowest Price and Highest Performance
- Multiple storage classes with best price/performance for any workload, plus automated data lifecycle management.
- Delivers resiliency, flexibility, latency, and throughput so storage never limits performance.

## Storage Classes
- **S3 Standard** — frequent access, higher cost
- **S3 Infrequent Access** — cheaper storage, higher retrieval cost
- **S3 Glacier** — cheapest, for archival, slow retrieval
- **S3 Intelligent-Tiering** — auto-moves objects between tiers based on access patterns
- **S3 Express One Zone** — fastest storage class, single-digit ms latency, up to 10x faster than S3 Standard; built for AI training/inference, real-time analytics, media processing

## Data Foundation for AI
- Foundation of modern data lakes — centralize structured/unstructured data, run analytics, build applications without managing infrastructure.
- **S3 Tables** — native Apache Iceberg support
- **S3 Vectors** — native vector storage and query for AI applications
  - Store/query vectors alongside source data in a fully serverless architecture
  - Reduces vector storage/query costs by up to 90% while maintaining subsecond query performance
  - Relevant to RAG pipelines (e.g. Verbatim) — S3 as raw data/blob store, OpenSearch as vector index on top

## Use Cases

### High Performance Workloads
- S3 Express One Zone accelerates performance-intensive workloads with consistent single-digit ms latency.
- Ideal for AI training/inference, real-time analytics, media processing, interactive applications.
- Improves compute efficiency, lowers API request costs, reduces TCO.

### AI
- Access diverse data types (unstructured, structured, streaming, vector) to train/fine-tune/customize models or improve contextual understanding via RAG.
- Direct integrations across AWS analytics and AI/ML services.

### Semantic Search
- Enables AI applications to understand meaning/context via vector embeddings representing relationships across content (documents, images, video).
- S3 Vectors brings native vector support to S3, storing/querying vectors alongside source data serverlessly.

## Developer Access
- **Console** — web UI, good for manual verification
- **CLI** — e.g. `aws s3 cp file.txt s3://my-bucket/`, `aws s3 ls`
- **SDK (boto3 for Python)** — used in application code to upload/download/list objects programmatically

## Practical Features

### Versioning
- When enabled on a bucket, uploading to an existing key doesn't overwrite the old object — both versions are kept.
- Protects against accidental deletes/overwrites.
- Tradeoff: storage costs quietly grow if old versions aren't managed/cleaned up.

### Lifecycle Policies
- Rules that automatically transition objects between storage classes (or delete them) based on age.
- Example: move to Infrequent Access after 30 days → Glacier after 90 → delete after 365.
- This is how "automated data lifecycle management" actually works — no manual tier-moving.

### Presigned URLs
- A temporary, signed URL granting time-limited access to a private object without making the bucket public.
- Standard pattern for letting a user upload/download a specific file without exposing credentials or opening the whole bucket.
- Common in web apps (e.g. file upload features) instead of using public buckets.

### Event Notifications
- S3 can trigger other services (commonly Lambda, or SQS/SNS) when something happens to a bucket — object created, deleted, etc.
- This is the connective tissue for pipeline architectures: file lands in S3 → event fires → Lambda picks it up → message to SQS → processed → indexed into OpenSearch.

### Multipart Upload
- For large files, S3 allows uploading in parallel chunks rather than one big request, and resuming if a chunk fails.
- Relevant for large files like video/audio (e.g. RAG pipelines ingesting raw video).

---

# boto3 (AWS SDK for Python)

## What it is
- The official AWS SDK for Python — how application code talks to AWS services (S3, SQS, Lambda, etc.) instead of using the CLI or console manually.
- Install: `pip install boto3`

## Client vs Resource
- boto3 offers two interface styles for interacting with AWS services:
  - *(to be filled in — client vs resource comparison)*