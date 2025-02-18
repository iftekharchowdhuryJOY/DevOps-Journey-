## How to install docker in redhat?
```
sudo yum update -y
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
sudo yum-config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo
sudo yum install -y docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
sudo systemctl enable docker
sudo docker run hello-world
sudo usermod -aG docker $USER
```
## What is Docker?

Docker is a platform where you can make your application containerization
Containerization packages your application along with all its dependencies into a standardized unit called a container. This ensures that the application runs reliably in different environments—from your local machine to production.

## Containers vs. Virtual Machines
1. VM: Like renting three separate apartments (each with kitchens, bathrooms, etc.) for three roommates. High cost but full privacy.
2. Container: Like three roommates sharing one apartment (common kitchen/bathroom). Cost-effective but shared resources.

## Working with Docker Images & Containers
1. download an image from an docker hub: docker pull nginx
2. Running a Container: docker run -d -p 80:80 --name my-nginx nginx
Explanation:
* -d: Run the container in detached mode (in the background).
* -p 80:80: Map port 80 of the host to port 80 in the container.
* --name my-nginx: Assign a custom name to the container.
* nginx: Specifies the image to use.

## Inspecting and Managing Containers
1. docker ps - list running containers
2. docker ps -a
3. docker logs my-nginx
4. docker inspect my-nginx
5. docker stop my-nginx
6. docker rm my-nginx
7. docker images
8. docker rmi nginx
9. docker run -it ubuntu /bin/bash
10. docker exec -it my-nginx /bin/bash
11. docker container prune
12. docker image prune

## Building Docker Images with Dockerfiles
A Dockerfile is a text file that contains a series of instructions for assembling a Docker image. When you build an image from a Dockerfile, Docker reads these instructions step by step and creates an image layer for each instruction.
```
FROM node:14
WORKDIR /usr/src/app
COPY package*.json
RUN npm install
COPY . .
EXPOSE 8080
CMD ["node", "server.js"]
```
## Explanation of Each Instruction:

* FROM: Specifies the base image. In this case, we're starting with the official Node.js image version 14.
* WORKDIR: Sets the working directory inside the container. All subsequent commands will be executed in this directory.
* COPY: Copies files from your host machine to the container. Here, we first copy only the package files to leverage Docker’s layer caching. Later, we copy the rest of the source code.
* RUN: Executes a command—in this example, installing dependencies with npm install.
* EXPOSE: Documents the port on which the container will listen. This does not publish the port; it’s mainly for informational purposes and for use with tools like Docker Compose.
* CMD: Specifies the default command to run when the container starts. This is the command that launches your application.

## Building the Docker Image
``` docker build -t my-node-app .```
* -t my-node-app tags the image with a name.
* The . tells Docker to use the current directory as the build context (which should include your Dockerfile).

## Managing Data & Networking
### Docker Volumes
Volumes are managed by Docker and are stored in a part of the host filesystem that’s managed by Docker (typically under /var/lib/docker/volumes/). They are the preferred mechanism for persisting data, as they provide several advantages:
1. Decoupling: They keep your data separate from the container's lifecycle.
2. Portability: Volumes can be easily backed up or migrated.
3. Performance: Volumes are optimized for I/O performance on Docker hosts.

```
* Create a Volume: docker volume create my-volume
* list volumes: docker volume ls
* inspect a volume: docker volume inspect my-volume
* Remove a Volume: docker volume rm my-volume
```
Using Volumes in a Container:
You can attach a volume to a container using the -v flag:

```
docker run -d \
  -v my-volume:/app/data \
  --name my-app \
  my-node-app
```
## Container Networking
## Default Networking: Bridge Network
By default, containers are connected to the default bridge network.
They can communicate with each other using container IP addresses, but this network is isolated from the host.

## Creating Custom Networks
```
docker network create my-network
docker run -d --name app1 --network my-network my-node-app
docker run -d --name app2 --network my-network my-node-app
docker network ls
docker network inspect my-network
```
### Example Scenario: Persistent Data and Networking Together
Imagine you have a web application that writes logs to a file and needs to be accessed from the host:
```
docker volume create app-logs
docker run -d \
  -p 8080:80 \
  -v app-logs:/var/log/app \
  --name web-app \
  my-web-app-image
```
You can inspect the logs stored in the app-logs volume by mounting it into another container or accessing it directly on the Docker host (if you know the volume path).

## Docker Compose & Orchestration
Docker Compose is a tool that allows you to define and run multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services, networks, and volumes. Then, with a single command, you can create and start all the services from your configuration.

## Key Benefits
* Multi-Container Management: Easily run, scale, and connect multiple containers.
* Service Definition: Define services (e.g., web, database, cache) in one file.
* Environment Reproducibility: Ensure that your application runs the same way across different environments.

## Basic Docker Compose File
Here’s a simple example for a web application that includes a web service and a database service:

```
version: "3.8"  # Specify the Compose file format version

services:
  web:
    build: ./web   # Build from the Dockerfile in the ./web directory
    ports:
      - "8080:80"  # Map host port 8080 to container port 80
    volumes:
      - ./web/app:/app  # Bind mount for live code changes
    environment:
      - NODE_ENV=development
    depends_on:
      - db

  db:
    image: postgres:13
    environment:
      - POSTGRES_USER=example
      - POSTGRES_PASSWORD=example
      - POSTGRES_DB=exampledb
    volumes:
      - db-data:/var/lib/postgresql/data

volumes:
  db-data:

```

## Explanation:

* version: Indicates the version of the Compose file format.
*services:
## web:
```
build: Tells Compose to build an image from the Dockerfile in the ./web directory.
ports: Maps container ports to host ports.
volumes: Mounts a host directory (./web/app) into the container.
environment: Sets environment variables.
depends_on: Specifies service dependencies (ensuring the database starts before the web service).
```
## db:
```
Uses an official PostgreSQL image.
Sets up necessary environment variables for database initialization.
Uses a named volume (db-data) for data persistence.
volumes: Defines a named volume that Docker will manage.
```
## Basic Docker Compose Commands
```
start services: docker-compose up
stop services: docker-compose down
view logs: docker-compose logs
To follow logs in real time, use: docker-compose logs -f
Rebuild Services: If you’ve made changes to your Dockerfile or code: docker-compose up --build
Scale Services: For example, to scale the web service to 3 instances: docker-compose up -d --scale web=3

```

## Advanced Topics & Best Practices
1. Run as Non-Root:
* Avoid running processes as the root user inside your containers.
* Use the USER directive in your Dockerfile to switch to a less-privileged user.

2. Minimize Attack Surface:
* Use minimal base images (e.g., Alpine or slim versions) to reduce vulnerabilities.
* Remove unnecessary packages and dependencies.
* Clean up temporary files and caches after installing dependencies: RUN apk add --no-cache <package> && rm -rf /var/cache/apk/*

3. Image Vulnerability Scanning:

Integrate tools like Clair, Anchore, or Docker's built-in scanning features to identify vulnerabilities.
Regularly update base images and dependencies.

