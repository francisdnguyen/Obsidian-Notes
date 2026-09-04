- **What can you build with AWS Lambda?**
	- **Event-driven applications**
		- Connect to 220+ AWS services and respond to events automatically. An object lands in Amazon S3, a record hits Amazon DynamoDB, an API call comes in. Lambda Functions handle the scaling, you handle the logic. Pay only for what runs.
	- **Isolated code execution**
		- Run untrusted or third-party code with VM-level isolation. No shared kernel, no shared memory, no shared state between tenants. Three levels of isolation, to per-tenant isolation to full MicroVM environments, so you pick the boundary that fits your threat model.
	- **AI agent orchestration and durable workflows**
		- Build multi-step, long-running workflows that can pause, wait for signals, retry on failure, and run for hours. Lambda durable functions gives you the control flow primitives (branching, parallelism, timeouts) without bolting on a separate orchestrator. Works for agentic AI loops, human approval chains, and saga patterns alike.
	- **Real-time data processing**
		- Process streams, transform records, and fan out to downstream systems as data arrives. Lambda Functions sits natively on Amazon Kinesis, Apache Kafka, Amazon SQS, and Amazon DynamoDB Streams, so you get sub-second processing without provisioning or tuning throughput. For sustained, high-throughput pipelines, Lambda Managed Instances provide dedicated capacity with predictable latency.
	- **Data analytics, notebooks, and interactive query platforms**
		- Preserve packages, computed results, and execution context across sessions, with no resets and no re-computation. Lambda MicroVMs launch and resume rapidly with per-tenant isolation, retain state across sessions, and pause automatically when idle so you only pay for active use.
- **How do I choose between Lambda Functions and Lambda MicroVMs**
	- They are complementary.
	- ## Lambda Functions vs. Lambda MicroVMs

| Workload                                               | Lambda Functions                     | Lambda MicroVMs                            |
| ------------------------------------------------------ | ------------------------------------ | ------------------------------------------ |
| Web and API backends                                   | ✓                                    |                                            |
| Sandbox to execute AI-generated code                   |                                      | ✓                                          |
| Event-driven pipelines (SQS, SNS, S3)                  | ✓                                    |                                            |
| Interactive notebooks and data analytics               |                                      | ✓                                          |
| Real-time streaming (Kafka, Kinesis)                   | ✓                                    |                                            |
| Security scanning and CI/CD with sudo access           |                                      | ✓                                          |
| Isolated request processing for separate tenants/users | ✓ (stateless, per-request isolation) | ✓ (stateful execution with full OS access) |
- **When should I use Lambda Managed Instances?**
	- Lambda runs your functions on fully managed infrastructure by default, with automatic scaling and pay-per-use pricing. Lambda Managed Instances give you dedicated EC2-backed capacity with built-in routing, load balancing, and multi-concurrency. Best for compute-intensive workloads like large-scale data processing, media transcoding, and scientific simulations. Up to 32 GB memory and 16 vCPUs, with no operational overhead.

## Core Concepts

### What a Lambda Function Actually Is
- A single function (your code) that AWS runs on-demand, in response to a **trigger** (an event source — S3 upload, SQS message, API call, schedule, etc.).
- You don't manage a server — AWS provisions, runs, and tears down the execution environment per invocation (or reuses it briefly for back-to-back calls — see cold starts below).
- You write a **handler function** — the entry point Lambda calls with the event data.

### Cold Starts vs. Warm Starts
- **Cold start** — the first invocation (or one after idle time) requires AWS to spin up a new execution environment, adding latency.
- **Warm start** — a subsequent invocation reuses an already-running environment, much faster.
- This is a classic Lambda gotcha in system design discussions — latency-sensitive apps need to account for cold start delay (or use Provisioned Concurrency to keep environments warm).

### Execution Limits
- Max execution time: 15 minutes per invocation (this is why long-running work gets split into steps/workflows rather than one giant function).
- Memory: configurable from 128 MB up to 10 GB — CPU scales proportionally with memory allocated.
- Lambda is billed by **execution time × memory allocated**, not a flat rate — efficient code directly saves money.

### Triggers (Event Sources)
- The "220+ AWS integrations" your notes mention are triggers — the most common ones you'll actually touch:
  - **S3** — object created/deleted → invoke Lambda
  - **SQS** — Lambda polls the queue and invokes per message/batch (ties directly to your SQS notes)
  - **API Gateway** — HTTP request → invoke Lambda (this is how you build a serverless API backend)
  - **EventBridge** — scheduled (cron-like) or event-pattern-based triggers

### IAM Execution Role
- Every Lambda function runs with an **execution role** — an IAM role defining exactly what other AWS services/resources it's allowed to touch.
- This is the security boundary: a Lambda reading from S3 needs explicit read permission on that bucket via its role, nothing is open by default.

### Statelessness
- Each invocation is independent — no guaranteed memory/state carried between calls (aside from opportunistic reuse during warm starts, which you shouldn't rely on).
- Any state that needs to persist goes to an external store — S3, DynamoDB, etc.
### Layers
- Reusable packages of code/dependencies (e.g. a shared library) that multiple functions can attach without bundling the dependency into every deployment package individually.

### Versions & Aliases
- Publish immutable versions of a function; point an alias (e.g. `prod`, `staging`) at a specific version.
- Enables safe rollouts/rollbacks without changing calling code.

### Concurrency & Throttling
- Lambda scales by running many instances of your function in parallel.
- Account-level concurrency limit (default 1,000, raisable) — exceeding it causes throttling.
- Relevant when processing SQS bursts: SQS buffers the load so Lambda pulls at a controlled pace instead of getting slammed all at once.

### Deployment Packages
- Your code + dependencies zipped up (or a container image for larger workloads), uploaded as the function's code.

### Environment Variables
- Configuration (API keys, table names, etc.) passed to the function without hardcoding — set per-function.

### VPC Access
- By default Lambda runs outside your VPC.
- If it needs to reach a private resource (e.g. an RDS database in a VPC), you configure it to attach to that VPC.
- Used to add meaningful cold-start latency; much less of an issue with modern Lambda networking.

## Setting Up Lambda in AWS

1. **Sign in to the Lambda console** — Search "Lambda" in the AWS Console. Same region-scoping as SQS — confirm you're in the intended region.
2. **Create a function** — Click "Create function" → "Author from scratch" → name it → pick a runtime (Python). AWS auto-creates a basic IAM execution role at this step.
3. **Write the handler code** — Use the inline code editor for small functions. Python handler pattern:
```python
   def lambda_handler(event, context):
       # event = trigger's event data
       # context = runtime info
       return response
```
4. **Set permissions (IAM role)** — In the "Configuration" tab, review the auto-generated execution role. Attach permission policies if the function needs to touch other services (e.g. read from S3).
5. **Add a trigger** — Click "Add trigger," pick an event source (S3 object created, SQS new message, API Gateway HTTP request are the common starting points), and configure which bucket/queue/API it listens to.
6. **Test the function** — Use the "Test" tab with a sample event payload (AWS provides templates for S3/SQS-style events) and check execution results/logs before relying on the real trigger.
7. **Invoke it with boto3 (optional)**:
```python
   lambda_client = boto3.client('lambda')
   lambda_client.invoke(FunctionName=name, Payload=json.dumps(data))
```
   Same client/method pattern as S3 and SQS.