
# Lecture 6 – Docker Fundamentals

## 1. What is Docker?

Docker is a platform to **build, ship, and run applications** in containers.

A container packages:

* Application code
* Runtime
* Libraries
* Config

Result: **Runs the same everywhere**

---

## 2. Why Docker?

### Before Docker

* Dependency conflicts
* Manual setup
* Works on my machine problem

### With Docker

* Isolated environments
* Portable
* Fast startup

---

## 3. Core Docker Components

| Component      | Description           |
| -------------- | --------------------- |
| Image          | Blueprint (read-only) |
| Container      | Running image         |
| Dockerfile     | Build instructions    |
| Docker Engine  | Runtime               |
| Docker Hub     | Image registry        |
| Docker Compose | Multi-container apps  |

---

## 4. Docker Architecture

Client → Docker Daemon → Containers

Docker uses **client–server model**.

---

## 5. Basic Docker Commands

```bash
docker --version
docker run hello-world
docker ps
docker ps -a
docker images
docker pull nginx
docker stop <id>
docker rm <id>
docker rmi <image>
```

---

## 6. Docker Images & Layers

* Images are **layered**
* Each RUN / COPY creates a new layer
* Uses Union File System (OverlayFS)

Image layers stored at:

```bash
/var/lib/docker/overlay2/
```

---

## 7. Image Inspection

```bash
docker history <image>
docker inspect <image>
```

---