- **How it works**
	- Lets you send, store, and receive messages between software components at any volume, without losing messages or requiring other services to be available.
- **Benefits**
	- **Overhead made simple**
		- Eliminate overhead with no upfront costs and without needing to manage software or maintain infrastructure.
	- **Reliability at scale**
		- Reliably deliver large volumes of data, at any level of throughput, without losing messages or needing other services to be available.
	- **Security**
		- Securely send sensitive data between applications and centrally manage your keys using AWS Key Management.
	- **Cost-effective scalability**
		- Scale elastically and cost-effectively based on usage so you don’t have to worry about capacity planning and preprovisioning.
- **Use cases**
	- **Increase application reliability and scale**
		- Amazon SQS provides a simple and reliable way for customers to decouple and connect components (microservices) together using queues.
	- **Decouple microservices and process event-driven applications**
		- Separate frontend from backend systems, such as in a banking application. Customers immediately get a response, but the bill payments are processed in the background.
	- **Ensure work is completed cost-effectively and on time**
		- Place work in a single queue where multiple workers in an autoscale group scale up and down based on workload and latency requirements.
	- **Maintain message ordering with deduplication**
		- Process messages at high scale while maintaining the message order, allowing you to deduplicate messages.
## Core Concepts

### The Queue/Message Model
- A **queue** holds **messages** (plain text/JSON payloads, up to 256 KB).
- **Producer** — sends messages to the queue
- **Consumer** — polls the queue and processes messages
- The queue decouples producer and consumer — they don't need to run at the same time or know about each other, which is the whole point ("decouple microservices" from your notes).

### Standard vs. FIFO Queues
- **Standard Queue** — near-unlimited throughput, but messages may arrive **out of order** and **more than once** (at-least-once delivery).
- **FIFO Queue** (First-In-First-Out) — strict ordering + exactly-once processing, but lower throughput.pre
- This is what "maintain message ordering with deduplication" in your notes is describing — that's a FIFO queue feature specifically, not a Standard queue default.

### Visibility Timeout
- When a consumer pulls a message, it isn't deleted — it becomes "invisible" to other consumers for a set period (the visibility timeout).
- If the consumer finishes processing, it explicitly deletes the message.
- If it crashes/times out before deleting, the message becomes visible again and another consumer can pick it up.
- This is the mechanism behind "reliably deliver... without losing messages" — nothing is removed until it's confirmed processed.

### Dead-Letter Queue (DLQ)
- A separate queue where messages get sent after failing processing too many times (exceeding a max retry count).
- Prevents a single "poison" message from blocking the queue forever or being retried infinitely.
- Common real-world pattern: monitor the DLQ to catch systematic processing failures.

### Polling: Short vs. Long
- **Short polling** — consumer asks "any messages?" and gets an immediate response, even if empty. Wastes API calls when the queue is often empty.
- **Long polling** — consumer's request waits (up to 20s) for a message to arrive before returning empty. More efficient, lower cost, generally preferred.

### Message Retention
- Messages are kept in the queue for a configurable period (default 4 days, up to 14) if never consumed/deleted, then automatically expire.

## How It Fits the Roadmap
- SQS sits between S3/Lambda in event-driven pipelines: e.g., S3 event notification → message pushed to SQS → Lambda (or an autoscaled worker fleet) polls the queue and processes each file, at a pace it can handle rather than getting overwhelmed by a burst of uploads.
- This is the "buffer" pattern — SQS smooths out spiky workloads so downstream services aren't hit all at once.