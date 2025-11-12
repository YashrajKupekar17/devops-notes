

# Lecture 7 – Dockerfile Deep Dive

## 1. Dockerfile Basics

```Dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

---

## 2. Key Instructions

| Instruction | Purpose                |
| ----------- | ---------------------- |
| FROM        | Base image             |
| RUN         | Execute build commands |
| COPY        | Copy files             |
| ADD         | Copy + extract + URL   |
| CMD         | Default command        |
| ENTRYPOINT  | Fixed command          |
| ENV         | Environment variables  |

---

## 3. ENTRYPOINT vs CMD

* ENTRYPOINT → fixed executable
* CMD → default arguments

---

## 4. Best Practices

* Use slim/alpine images
* Combine RUN commands
* Clean cache
* Use non-root user
* Pin versions
* Scan images

---

## 5. Build & Run

```bash
docker build -t flask-app .
docker run -p 8080:8080 flask-app
```
