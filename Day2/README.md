# Day 2 — Docker Architecture

This diagram illustrates the core components of Docker and the typical workflow between them.

![Docker Architecture](images/docker-architecture.svg)

Description:
- Docker Client: CLI or API used to communicate with the Docker daemon.
- Docker Host: Runs the Docker daemon (dockerd) which manages images, containers, networks, and volumes.
- Docker Registry: Stores images (Docker Hub or private registries).
- Images: Immutable templates built from Dockerfiles.
- Containers: Running instances of images. 

The diagram is added as Day2/images/docker-architecture.svg.
