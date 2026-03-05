# Docker Foundations

This document captures my current understanding of Docker fundamentals based on hands-on practice.

It serves as a baseline before maintaining daily learning logs for containerization.

---

## What is Docker

Docker is a containerization platform that packages an application and its dependencies into containers so they run consistently across different environments.

Containers share the host OS kernel while remaining isolated from each other.

---

## Containers vs Virtual Machines

| Feature | Containers | Virtual Machines |
|--------|-------------|-----------------|
| Isolation | Process level | Hardware level |
| OS | Shared kernel | Separate OS |
| Startup | Seconds | Minutes |
| Resource Usage | Lightweight | Heavy |

---

## Docker Image

A Docker image is a read-only template used to create containers.

Images contain:
- Application code
- Runtime
- Libraries
- Dependencies
- Environment configuration

Images are typically stored and distributed through container registries.

---

## Docker Container

A container is a running instance of an image.

Containers are:
- Lightweight
- Isolated
- Portable
- Ephemeral by default

---

## Container Lifecycle

Typical lifecycle:

Create → Run → Stop → Remove

Common commands:

docker run  
docker stop  
docker start  
docker rm  

---

## Listing Containers

View running containers:

docker ps

View all containers:

docker ps -a

---

## Executing Commands in Containers

Run commands inside a running container:

docker exec

Useful for debugging or inspecting running containers.

---

## File Transfer Between Host and Container

Docker supports copying files between the host system and containers.

Host → Container

docker cp host_path container:path

Container → Host

docker cp container:path host_path

---

## Port Mapping

Containers run in isolated networks.

Ports can be mapped to expose container services to the host.

Syntax:

host_port:container_port

Example concept:

Host port 8085 → Container port 80

---

## Volume Mapping

Volumes allow containers to persist data outside the container filesystem.

Syntax:

host_directory:container_directory

Benefits:
- Persistent storage
- Data sharing between host and container
- Easier updates without rebuilding containers

---

## Container Inspection

Container configuration and metadata can be viewed using:

docker inspect

This reveals information such as:
- Volume mappings
- Network settings
- Container status
- Image details

---

## Key Takeaways

Core Docker concepts understood:

- Containerization fundamentals
- Docker images and containers
- Container lifecycle management
- Container inspection
- File transfer between host and containers
- Port mapping
- Volume mapping