- For the GO backend, we need to pick a Postgres driver
	- pgx used directly gives native access to Postgres-specific things this project actually needs — most importantly, custom type registration. This is exactly why pgvector's Go integration (pgvector-go/pgx) hooks into pgx's connection setup, not into database/sql's generic driver interface. Using database/sql at the start would have meant a rework later when pgvector support was needed.
- We establish a connection pool in db.go
	- If everything shared a single Postgres connection, requests would either serialize behind it (defeating the point of concurrency) or corrupt each other (Postgres connections aren't safe to use from multiple goroutines at once). A pool hands out separate connections to concurrent callers and reuses them once released — this is precisely what lets `HandleSubmit`, `HandleStatus`, and a background ingestion goroutine all touch the database at the same time safely, later.
- YouTube Transcript Ingestion with Supadata
	- Getting captions out requires either scraping YouTube's internal caption endpoints (fragile, unofficial, ToS-questionable) or a third-party service that's already solved that problem.
- Chunking
	- Chunking exists to **regroup these small segments into ~500-word blocks** — big enough to carry real context, small enough to stay specific to one topic rather than blending in unrelated parts of the video.
	- Count the incoming segment's words (`strings.Fields` — a simple whitespace split).
	- **Before adding it**, check: would adding this segment push the currently-building chunk over `maxWords`? If so, close the current chunk now (`newChunk`) rather than let it keep growing unbounded.
	- When closing a chunk, don't start the next one empty — carry forward a _tail_ of the just-closed chunk (`trailingOverlap`) so there's continuity across the boundary.
	- Add the current segment to the (possibly now-reset) buffer, and keep going.
	- At the very end, whatever's left in the buffer becomes the final chunk (there's no next segment to trigger a close, so this has to happen explicitly after the loop).
- Embeddings
	-  So every chunk's text has to be converted into a **vector**: a fixed-length list of numbers positioned in space such that texts with similar meaning end up numerically close together. That conversion is what an embedding model does, and it's the one thing that makes semantic search possible instead of plain keyword matching.
- Synchronous Ingestion Pipeline
	-  This piece is the first one that actually **writes real rows to Postgres**, wiring transcript → chunk → embed together into one real, callable flow that produces a genuine `videos` row and genuine `chunks` rows with real embeddings. Before this, the pipeline existed only as four separate, unconnected functions.
- Async Wrapper + HTTP Server
	- A real product needs an actual HTTP surface — something a browser/frontend can call. - We need the HTTP Server
	- Async Wrapper - accept the request instantly, do the real work in the background, let the client poll for progress
- Q&A Endpoint
	- This is the piece that actually turns that stored data into an answer to a real question. Without it, the product has ingested video after video and has nothing to show for it.
	- Retrieve the top 5 most relevant transcript chunks, then sends those chunks to **GPT-4o** with a prompt that instructs it to answer only from the given excerpts and cite each one's `[MM:SS-MM:SS]` timestamp range.
- Upload Ingestion (S3 + ffmpeg + Whisper)
	- Second ingestion path (so when the user uploads a file instead of a YouTube link)
	- It uploads the file to Amazon S3 first and then the background goroutine downloads it back down to a local temp file and then runs it through ffmpeg to extract a MP3 audio track and sends that to OpenAI Whisper for a real timestamped transcript.
	- Feeds it to the same chunk->embed->store pipeline as YouTube
- JWT-based Authentication
	-  Passwords get bcrypt-hashed (one-way, so a leaked database doesn't leak real passwords), and logging in exchanges an email/password for a signed JWT containing the user's ID — a token the server can verify with just a signature check, no session store needed to remember who's logged in. Every video endpoint now runs through a middleware that checks this token and rejects the request if it's missing or invalid, and the user ID for any action comes from that verified token rather than a client-supplied field, so there's nothing left to fake. On top of that, an ownership check means even a valid token only grants access to _your_ videos — a mismatch returns 404, not 403, so someone probing a random video ID can't even tell whether it exists.
-  RDS (Relational Database Service)
A managed database — AWS runs and maintains the actual Postgres server for you (patching, backups, storage) instead of you installing Postgres on a machine yourself. We created verbatim-db, a PostgreSQL 16.14 instance with the pgvector extension enabled (needed for the vector similarity search your Q&A feature relies on). It has no public IP by default — it's meant to only be reachable from inside your AWS network (VPC), not the open internet, which is why we hit connectivity issues until we temporarily flipped "Public access" on for the one-time schema setup, then locked it back down.

IAM (Identity and Access Management)
AWS's permissions system — it controls who (or what) can do what to your AWS resources. We used two IAM concepts:

Roles: an identity that isn't a person — we created verbatim-ec2-role and attached it to the EC2 instance itself. This lets the instance prove its identity to AWS automatically (via the instance metadata service) without ever storing a password/key file on disk.
Policies: the actual permission grants attached to a role. verbatim-ec2-role's policy only allows three specific S3 actions (PutObject/GetObject/DeleteObject) on one specific bucket — deliberately narrow, so even if the instance were somehow compromised, the blast radius is limited to that one bucket.
S3 (Simple Storage Service)
Object storage — basically a place to store files (your uploaded videos/audio) that isn't a traditional filesystem. We created a dedicated production bucket (verbatim-uploads-prod-francisnguyen), private by default, and the backend reaches it using the IAM role above instead of a hardcoded access key/secret.

EC2 (Elastic Compute Cloud)
A virtual machine you rent by the hour — this is what actually runs your Go backend container 24/7. We picked Ubuntu as the OS, launched a t3.micro first (cheap, 1GB RAM), hit a real wall when it couldn't handle compiling the Docker image, and resized to t3.small (2GB RAM).

Security Groups
A virtual firewall attached to an EC2 instance or RDS database — a set of rules saying "only allow traffic in on these ports, from these sources." We used two:

verbatim-ec2-sg: allows SSH (22, from specific admin IPs only), and HTTP/HTTPS (80/443, from anywhere — since real users need to reach it)
verbatim-db-sg: allows Postgres (5432) only from verbatim-ec2-sg — meaning only your backend instance can talk to the database, nothing else on the internet can even attempt a connection
VPC (Virtual Private Cloud)
The private network your resources live inside — we didn't create one, just used the account's auto-created "Default VPC," which was enough here. It's what makes "RDS is only reachable from EC2" actually enforceable at the network level, not just the security-group level.x`