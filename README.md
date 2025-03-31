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
- *Docker Compose:* A tool to define and run multiple containers easily.

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
- Example: A web server (NGINX) can talk to a database (MariaDB) through a shared network.

### 7. Volumes (Persistent Storage)
- Containers are ephemeral (data is lost when restarted)
- Volumes help store data permanently
- Example: Storing database data putside the container so it persists after restart.

### 8. Reverse Proxi (NGINX)
- Direct traffic to the correct service (e.g. Web request -> Your web server)
- Ensures security amd load balancing.


## Q&A

### 1. How Docker and Docker Compose work?
- Docker is a tool that helps package applications and their dependencies into containers, which are lightweight, standalone environments. Each container runs an application with all the required files, libraries, and settings, ensuring it bahaves the same regardless of where it runs.
- Docker Compose is a tool that allows you to manage multiple Docker contatiners as single application. Instead of running each container separately with individual commands, Docker Compose uses docker-compose.yml file to define all containers, their configurations, networks, and dependencies. Then, a single command (docker-compose up) starts everything at once.

### 2. Difference Between a Docker Image with and Without Docker Compose?
- Without Docker Compose:
Runnign Docker image manually requires individual docker run commands, specifying ports, volumes, networks, and environment variables manually. Example:
```
docker run -d -p 80:80 --name my_container my_image
```
- With Docker Compose:
You define the image, networking, and dependencies in docker-compose.yml. Then, all configurations are applied automatically when running docker-compose up. This is especially useful for multi-container applications. Example docker-compose.yml:
```
services:
	web:
		image: my_image
		ports:
			- "80:80"
```

### 3. Benefits of Docker Compared to Virtual Machines?
| Feature | Docker Containers | Virtual Machines |
|---|---|---|
|Performance|Lightweight|Heavy, each VM has its own OS|
|Startup Time|Starts in seconds|Takes minutes to boot|
|Resource Usage|Low, uses host system's resources efficiently|High, requires dedicated CPU, RAM, and storage|
|Isolation|Process-level isolation|Full OS-level isolation|
|Portability|Runs consistently on any system with Docker installed|Needs hypervision, OS compatibility may vary|

> **Main advantage:** Docker provides a faster, more efficient and more portable solution compared to VM's, making it ideal for deploying and scaling applications.

### Docker Networking???
Docker networking allows containers to communicate with each other and with the outside world. It provides different network types, but the most common ones are:

+ **Bridge Network (Default):** Each container gets its own IP adress and can communicate with the other containers on the same network.
Example: Containers running a web app and a database can talk to each other via container names instead of IP adresses.
+ **Host Network:** The Container shares the host machine's network, meaning it doesn't get an isolated IP.
+ **Overlay Networks:** used for communication between containers across different physical machines in a Docker Swarm.
+ **None:** No network access is provided to the container.

In Docker Compose, services are automatically placed on the same network making communication easy without manual setup.

Example of how two services (web and database) communicate:
```
services:
	web:
		image: my_web_app
		networks:
			- my_network

	db:
		image: postgres
		networks:
			- my_networks
	
networks:
	my_networks:
		drivers: bridge
```
Here, web can reach db using db as the hostname

### 6. How to login into the Database & Verify It's not empty
To access the database inside a Docker container, do:

**Step 1:** Find the Running Database Container
Run:
```
docker ps
```

Look for the container name or ID of your databasse (e.g., postgres or mysql).

**Step 2:** Access the Database Container
For MySQL:
```
docker exec -it <db_container_name> mysql -u <username> -p
```

**Step 3:** Check of the Database is Not Empty
For MySQL:
```
SHOW TABLES;
```

If no tables are listed, the database is empty.