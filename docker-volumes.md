
# Lecture 9 – Docker Volumes

## 1. Why Volumes?

Containers are **stateless**.
Stopping container deletes writable layer.

Volumes persist data.

---

## 2. Volume Types

| Type       | Persistent | Use Case  |
| ---------- | ---------- | --------- |
| Anonymous  | Temporary  | Tests     |
| Named      | Yes        | Databases |
| Bind Mount | Host-based | Dev       |
| tmpfs      | RAM only   | Secrets   |

---

## 3. Named Volume Example

```bash
docker volume create mydata
docker run -v mydata:/var/lib/mysql mysql:8
```

---

## 4. Bind Mount Example

```bash
docker run -v $(pwd):/app nginx
```

---

## 5. tmpfs Example

```bash
docker run --tmpfs /cache nginx
```

---

## 6. Where Volumes Are Stored

```bash
/var/lib/docker/volumes/
```

---

## 7. Final Summary

* Containers are ephemeral
* Volumes persist data
* Use named volumes in production
* Use bind mounts for development
* Use tmpfs for sensitive data
