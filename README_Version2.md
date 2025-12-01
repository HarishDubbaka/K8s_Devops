# K8s_Devops

Kubernetes (K8s) + DevOps overview that you can use for learning, interviews, and projects.

---

## Introduction to Docker 🐳

This document provides a foundational understanding of Docker, why it's essential, and how it works.

---

### The Problem with Traditional Deployments

Before containers, deploying applications was often a challenging process. Let's consider a typical workflow with development, testing, and production environments:

1. A developer writes code for a new feature on their local machine. After testing, they push it to a version control system like Git. 
2. A build is created and deployed to the development environment, and after tests pass, it is pushed through to QA/staging and then production.

However, when the same build is promoted to the production environment, it fails. 💥

This common scenario, often called the **"it works on my machine" problem**, can happen for many reasons:

- **Environment Misconfiguration:** Subtle differences in configuration files between environments.
- **Missing Dependencies:** A library or package is present in the dev/test environments but was never installed in production.
- **Version Mismatches:** The version of a programming language, library, or OS-level package is different in production.

This leads to friction between Development and Operations teams, lengthy troubleshooting sessions, and delays in releasing new features. There was no easy way to package an application's code along with everything it needed for consistent execution across environments.

---

### How Docker Solves This: The Power of Containers

Containers solve this problem by packaging an application's code with everything it needs to run, including:

- Specific versions of libraries and frameworks
- System tools and binaries
- Runtime and configuration files

This package, called a **container image**, is a single, self-contained unit. Because the container includes its own environment, what works in development will work **exactly the same** in testing and production.

---

### What is a Container?

A container is a **lightweight, standalone, and executable** package of software that includes everything needed to run an application.

- **Isolated:** Containers run in isolated environments (sometimes called a "sandbox"). One container cannot interfere with another or with the host machine.
- **Lightweight:** Unlike a virtual machine, a container doesn't bundle a full operating system. It shares the host machine's OS kernel, only including the specific libraries and packages needed by the app.
- **Portable:** A container can run on any machine that has a container engine (like Docker) installed, regardless of the underlying OS (Ubuntu, CentOS, Windows, etc.).

The goal of a container is simple: **Build, Ship, and Run any application, anywhere**.

> **Docker vs. Container:** People often use these terms interchangeably.  
> A container is the actual running instance of an application.  
> **Docker** is the platform or tool that helps you build, ship, and run those containers.

---

### How Does Docker Work?

Docker uses a client-server architecture:

- **Docker Daemon (Server):** The server-side component that manages images, containers, networks, and storage volumes.
- **Docker Client (CLI):** The tool you use to communicate with the Docker daemon. When you run `docker run`, `docker build`, etc., you're using the Docker client.
- **Docker Registry:** Stores Docker images. Docker Hub is the default public registry, but organizations can run their own private registries.

#### Key Concepts

- **Image:** A read-only template used to create containers. Think of it as a snapshot of the file system and configuration.
- **Container:** A running instance of an image. Containers are ephemeral — if deleted, changes are lost unless saved to a persistent volume.
- **Dockerfile:** A text file with instructions on how to build a Docker image. It defines the base image, application code, dependencies, environment variables, and commands to run.
- **Volume:** Persistent storage mechanism for containers. Used when you need your data to persist, even if the container is removed.

---

### Common Docker Workflow

1. **Write a Dockerfile** — Define how to build your application image.
2. **Build the image** — `docker build -t myapp:latest .`
3. **Run the container** — `docker run -d -p 8080:80 myapp:latest`
4. **Publish the image** (optional) — Push to DockerHub or another registry using `docker push myapp:latest`

---

### Advantages of Docker

- Consistency across environments (dev, test, prod)
- Easy to share and distribute
- Fast startup, resource efficient compared to VMs
- Simplifies scaling and orchestration (especially with Kubernetes)

---

### Sample Dockerfile

```dockerfile
# Use an official Python runtime as a base image
FROM python:3.11-slim

WORKDIR /app

# Copy dependencies
COPY requirements.txt requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Copy code
COPY . .

CMD ["python", "app.py"]
```

---

### What’s Next?

After learning Docker basics, the next step is learning **Kubernetes (K8s)**, which is a system for orchestrating (deploying, scaling, and managing) containers in production.

---