# Inception

### 1. What is Docker?
- Docker is a tool that lets you package applications and their dependencies into containers.
- A container is like a lightweight virtual machine but more efficient.
- Container ensure that the app runs the same way everywhere, no matter the system.

### 2. Why Use Containers?
- Avoids "works on my machine" problems.
- Uses fewer resources than virtual machines.
- Isolated environment prevents conflicts between applications.

### 3. Key Docker Components
- *Image:* A blueprint for a container (like a template).
- *Container:* A running instance of an image.
- *Dockerfile:* A script that defines how to build an image.
- *Docler Compose:* A tool to define and run multiple containers easily.

### 4. Basic Docker Commands
- "docker build -t my_image ." -> Build an image from a Dockerfile.
- "docker run -d --name my_container my_image" -> Start a container in the background.
- "docker ps" -> List running containers.
- "docker stop my_containers" -> Stop a running container.
- "docker rm my_container" -> Remove a container.

### 5. What is Docker Compose?
- It lets you define multiple services (containers) in a single docker-compose.yml file.
- Example: Your project might have a database container and web server container.
- To start everything: "docker-compose up -d"
- To stop everything: "docker-compose down"

### 6. Networking in Docker
- Containers communicate through Docker networks.
- Example: A web server (NGIIX) can talk to a database (MariaDB) through a shared network.


### 7. Volumes (Persistent Storage)
- Containers are ephemeral (data is lost when restarted)
- Volumes help store data permanently
- Example: Storing database data putside the container so it persists after restart.

### 8. Reverse Proxi (NGINX)
- Direct traffic to the correct service (e.g. Web request -> Your web server)
- Ensures security amd load balancing.
