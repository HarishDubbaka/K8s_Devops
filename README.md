# K8s_Devops
Kubernetes (K8s) + DevOps overview that you can use for learning, interviews, projects.

Introduction to Docker 🐳
This document provides a foundational understanding of Docker, why it's essential, and how it works.

The Problem with Traditional Deployments
Before containers, deploying applications was often a challenging process. Let's consider a typical workflow with development, testing, and production environments.

A developer writes code for a new feature on their local machine. After testing, they push it to a version control system like Git. A build is created and deployed to the development environment, and it works perfectly. The team then promotes this build to the testing environment, and again, everything works as expected.

However, when the same build is promoted to the production environment, it fails. 💥

This common scenario, often called the "it works on my machine" problem, can happen for many reasons:

Environment Misconfiguration: Subtle differences in configuration files between environments.
Missing Dependencies: A library or package is present in the dev/test environments but was never installed in production.
Version Mismatches: The version of a programming language, library, or OS-level package is different in production.
This leads to friction between Development and Operations teams, lengthy troubleshooting sessions, and delays in releasing new features. There was no easy way to package an application's code along with its specific dependencies, libraries, and configurations to ensure it ran consistently everywhere.

How Docker Solves This: The Power of Containers
Containers solve this problem by packaging an application's code with everything it needs to run, including:

Specific versions of libraries and frameworks
System tools and binaries
Runtime and configuration files
This package, called a container image, is a single, self-contained unit. Because the container includes its own environment, what works in development will work exactly the same in testing and production. It guarantees environment consistency, eliminating the primary cause of deployment failures.

What is a Container?
A container is a lightweight, standalone, and executable package of software that includes everything needed to run an application.

Isolated: Containers run in isolated environments (sometimes called a "sandbox"). One container cannot interfere with another or with the host machine.
Lightweight: Unlike a virtual machine, a container doesn't bundle a full operating system. It shares the host machine's OS kernel, only including the specific libraries and packages needed by the application. This makes container images much smaller and faster to start.
Portable: A container can run on any machine that has a container engine (like Docker) installed, regardless of the underlying OS (Ubuntu, CentOS, Windows, etc.).
The goal of a container is simple: Build, Ship, and Run any application, anywhere.

Docker vs. Container: People often use these terms interchangeably. A container is the running instance of an application. Docker is the platform or tool that helps you build, ship, and run those containers. While Docker is the most popular, other alternatives like Podman also exist.

