- An OS-level virtualization (containerization) platform, which allows applications to share the host OS kernel instead of running a separate guest OS like in traditional virtualization.
- This design makes Docker containers are lightweight, fast, and portable, while keeping them isolated from one another.
- **Docker's Solution**
	- ![[Pasted image 20260818234512.png]]
	- Standardizing the runtime environment. By bundling the application with its specific dependences into a single unit, it ensures the software runs identically whether it's on a developer's laptop, a test server, or a cloud cluster.
	- **Portability:** Runs anywhere in local machine, cloud, on-prem servers.
	- **Consistency:** Same behavior in development, testing, and production
	- **Lightweight:** No full OS per app; containers share the host kernel
	- **Scalability:** Ideal for microservices and orchestrators like Kubernetes and Docker Swarm
	- **Efficiency:** Starts in seconds, uses fewer system resources
- **Docker Architecture and Working**
	- The Docker client talks with the docker daemon which helps in building, running, and distributing the docker containers.
	- The Docker client runs with the daemon on the same system or we can connect the Docker client with the Docker daemon remotely.
	- With the help of REST API over a UNIX socket or a network, the docker client and daemon interact with each other.
	- ![[Pasted image 20260818235651.png]]
	- **The Docker Client (CLI):** The primary way users interact with Docker. When you type `docker run`, the client sends this command to the daemon via a REST API.
	- **The Docker Daemon (dockerd):** The background service (server) that manages Docker objects such as images, containers, networks, and volumes.
	- **Docker Registry (Docker Hub):** A storage system for Docker images. Docker Hub is the largest public registry, allowing developers to share and pull pre-configured images (like Ubuntu, MySQL, or Nginx).
- **Components of Docker**
	- **Docker Engine:** 
		- ![[Pasted image 20260819000521.png]]
		- Has a core part docker daemon that handles the creation and management of containers.
		- Docker images cannot be built or containers executed without this engine
		- The runtime that makes containerization possible by connecting the Docker client with the daemon to build and mange containers efficiently
	- **Dockerfile:**
		- ![[Pasted image 20260819001252.png]]
		- Text document that contains necessary commands which on execution helps assemble a Docker Image quickly that uses DSL (Domain Specific Language)
		- While creating your application, you should create a Dockerfile in order since the Docker daemon runs all of the instructions from top to bottom.
	- **Docker Image:**
		- A read only template that is made up of multiple layers that contains the instructions to build and run a Docker container. It acts as an executable package that includes application code, runtime, libraries, environment variables, and configurations.
		- Blueprint (static, read only)
		- The image defines how a container should be created.
		- Specifics which components will run and how they are configured.
		- Once ran, it becomes a Docker Container.
	- **Docker Container:**
		- Lightweight, runnable instance of a Docker Image. It packages the application code together with all its dependencies and runs it in an isolate environment.
		- Live instance of that blueprint (dynamic, executable)
		- Allow applications to run quickly and consistently across different environments.
		- Runs as an isolated process on the host machine but shares the host's operating system kernel.
		- Multiple containers can run on the same system without interfering with each other.
	- **Docker Hub:**
		- A cloud based repository that is used for finding and sharing the container images.
		- **Repository Service:** Serves as a global storage hub where users can push (upload) or pull (download) container images from anywhere via the internet.
		- **Image Management:** Offers the flexibility to host images in public registries or private registries
		- **Collaboration:** Simplifies the DevOps workflow by allowing teams to find, reuse, and share standardized environments.
		- **Accessibility:** An open-source, freely available tool compatible with all major operating systems.
		- **Resource Library:** Hosts millions of "Official Images" for popular software like Nginx, Python, and Ubuntu, ensuring a verified starting point for projects.
		- ![[Pasted image 20260819002450.png]]
	- **Docker Registry:**
		- A storage distribution system for docker images, where you can store the images in both public and private modes.
- **Docker Commands**
	- **Docker Run:** Used for launching the containers from images, with specifying the runtime options and commands.
	- **Docker Pull:** It fetches the container images from the container registry like Docker Hub to the local machine.
	- **Docker ps:** It helps in displaying the running containers along with their important information like container ID, image used and status
	- **Docker Stop:** Helps in halting the running containers gracefully shutting down the processes within them.
	- **Docker Start:** Helps in restarting the stopped containers, resuming their operations from the previous state.
	- **Docker Login:** Helps to login in to the docker registry enabling the access to private repositories.

## Additional Concepts

### Volumes & Persisting Data
- Containers are ephemeral by default — filesystem changes are lost when a container is removed.
- **Volumes** are Docker-managed storage that persists data independently of a container's lifecycle (e.g. a database's data directory).
- Needed for any stateful containerized service (e.g. a containerized Postgres instance, as opposed to using a managed service like RDS).

### Bind Mounts / Sharing Local Files with Containers
- Maps a host machine directory directly into a container.
- Commonly used in local development so code changes reflect inside the container without rebuilding the image.
- Distinct from volumes: a bind mount points to a specific host path; a volume is managed entirely by Docker.

### Publishing / Exposing Ports
- A container's internal port (e.g. an app listening on 8080) must be mapped to a port reachable from outside the container.
- Example: `docker run -p 8080:8080 my-image`
- Without this, nothing outside the container can reach the running application.

### Image Layers & Build Cache
- Each Dockerfile instruction creates a cached layer.
- Docker only rebuilds layers that changed since the last build — unchanged layers are reused from cache, making rebuilds much faster.
- Common optimization: copy dependency manifest files (e.g. `package.json`, `go.mod`) and install dependencies *before* copying application source code, so dependency installation gets cached and isn't repeated on every code change.

### Multi-Stage Builds
- Use multiple `FROM` stages in one Dockerfile so the final image only contains what's needed to *run* the app, not what was needed to *build* it (compilers, dev dependencies, build tools).
- Significantly shrinks final image size.
- Directly relevant for compiled languages (e.g. Go) — the build stage can include the full toolchain, while the final stage copies over just the compiled binary.

### Docker Compose
- Defines and runs multi-container applications (e.g. app + database + cache) from a single YAML file.
- One command (`docker compose up`) starts everything together with networking configured between containers, instead of manually running/linking each container.
- Natural stepping stone toward ECS task definitions, which similarly group multiple containers to run together.

### Additional Docker Commands
- **`docker build`** — build an image from a Dockerfile.
- **`docker tag`** — tag an image (e.g. for versioning or before pushing to a registry).
- **`docker push`** — upload a tagged image to a registry (e.g. Docker Hub, Amazon ECR).
- **`docker exec`** — run a command inside a running container (e.g. open a shell to debug: `docker exec -it <container> /bin/sh`).
- **`docker logs`** — view a container's output/logs.
- **`docker rm`** — remove a stopped container.
- **`docker rmi`** — remove an unused image.

### Dockerfile Instruction Basics
- **`FROM`** — specifies the base image to build from.
- **`RUN`** — executes a command at build time (e.g. installing dependencies).
- **`COPY`** / **`ADD`** — brings files from the host into the image.
- **`CMD`** / **`ENTRYPOINT`** — defines what runs when the container starts.
- **`EXPOSE`** — documents which port the container listens on (doesn't actually publish it — that's done via `-p` at runtime).