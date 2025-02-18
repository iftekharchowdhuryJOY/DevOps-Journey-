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
