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

However, when the same build is promoted to the production environment, it sometimes fails. 💥

This common scenario, often called the **"it works on my machine" problem**, can happen for many reasons:

- **Environment misconfiguration:** Subtle differences in configuration files between environments.
- **Missing dependencies:** A library or package is present in the dev/test environments but was never installed in production.
- **Version mismatches:** The version of a programming language, library, or OS-level package is different in production.

This leads to friction between Development and Operations teams, lengthy troubleshooting sessions, and delays in releasing new features. There was no easy way to package an application's code along with its exact runtime environment — until containers became common.

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
- **Lightweight:** Unlike a virtual machine, a container doesn't bundle a full operating system. It shares the host machine's OS kernel, only including the specific libraries and packages needed by the application.
- **Portable:** A container can run on any machine that has a container engine (like Docker) installed, regardless of the underlying OS (Ubuntu, CentOS, Windows, etc.).

The goal of a container is simple: **Build, Ship, and Run any application, anywhere**.

> **Docker vs. Container:** People often use these terms interchangeably.  
> A container is the actual running instance of an application.  
> **Docker** is the platform or tool that helps you build, ship, and run those containers.

---

### Containers vs. Virtual Machines (VMs)

To understand containers better, it's helpful to compare them to Virtual Machines (VMs).

Think of a VM as an independent house. It has its own foundation, plumbing, electricity, and infrastructure (its own full guest OS). It's completely isolated but also heavy and resource-intensive.

Think of a container as an apartment in a large building. Each apartment is isolated and secure, but they all share the building's core infrastructure (the host OS kernel). This is far more efficient and lightweight.

| Feature           | Virtual Machine (VM)            | Container                             |
|-------------------|---------------------------------|---------------------------------------|
| Isolation         | Full OS virtualization          | Process-level isolation               |
| OS                | Has its own full Guest OS       | Shares the Host OS kernel             |
| Size              | Large (several GBs)             | Lightweight (tens to hundreds of MBs) |
| Start-up Time     | Minutes                         | Seconds or milliseconds               |
| Resource Usage    | High (dedicated RAM & CPU)      | Low (uses only what's needed)         |
| Underlying Tech   | Hypervisor                      | Container Engine (e.g., Docker)       |

Docker allows for the optimum use of infrastructure. It ensures applications only consume the resources they need and can scale up or down easily, preventing the resource wastage common with VMs.

---

## The Docker Workflow: Build, Ship, and Run

The entire Docker process can be broken down into a simple workflow.

- **Dockerfile:** It all starts with a Dockerfile. This is a simple text file containing step-by-step instructions on how to build your application's image. For example: "start with an Ubuntu base image, copy my app files, install dependencies, and set the command to run the app."
- **docker build:** You run this command, pointing to your Dockerfile. Docker reads the instructions and executes them to create a Docker image. This image is the portable package containing your application and its environment.
- **Docker Registry:** An image isn't useful if it only exists on your machine. A registry is a storage system for your images, much like GitHub is a storage system for your source code. You need a central place to store and share images.
- **docker push:** You use this command to upload your built image to a registry.
- **docker pull:** On any other machine (like a production server), you can use this command to download the image from the registry.
- **docker run:** This command takes an image and creates a running container from it. Your application is now up and running inside an isolated, consistent environment.

This workflow ensures that the exact same image is used across all environments, from development to production.

---

## Docker Architecture Overview

Docker uses a client-server architecture:

- **Docker Client:** This is the command-line tool (docker) that you use to issue commands like `docker build`, `docker run`, etc.
- **Docker Daemon (dockerd):** This is a background service running on the Docker host. It listens for API requests from the Docker Client and manages all the Docker objects: images, containers, networks, and volumes.
- **Registry:** Where images are stored and pulled from (e.g., Docker Hub, AWS ECR, GCP Artifact Registry).

When you type a command like `docker run my-app`, the Client tells the Daemon to run the image. The Daemon first checks if it has the `my-app` image locally. If not, it pulls it from the Registry and then starts the container.

---

### How Does Docker Work? (Key Concepts)

- **Image:** A read-only template used to create containers. Think of it as a snapshot of the file system and configuration.
- **Container:** A running instance of an image. Containers are ephemeral — if deleted, changes are lost unless saved to a persistent volume.
- **Dockerfile:** A text file with instructions on how to build a Docker image. It defines the base image, application code, dependencies, environment variables, and commands to run.
- **Volume:** Persistent storage mechanism for containers. Used when you need your data to persist, even if the container is removed.

---

### Common Docker Workflow (Quick steps)

1. **Write a Dockerfile** — Define how to build your application image.  
2. **Build the image** — `docker build -t myapp:latest .`  
3. **Run the container** — `docker run -d -p 8080:80 myapp:latest`  
4. **Publish the image** (optional) — Push to Docker Hub or another registry: `docker push myapp:latest`

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
