
---

# Lecture 8 – Docker Containers (Internals)

## 1. What is a Container Really?

A container is:

> **A Linux process + isolation**

Not a VM.

---

## 2. Why Containers Are Ephemeral

* Container writable layer exists only while running
* When PID 1 exits → container stops → data lost

---

## 3. Namespaces (Isolation)

| Namespace | Purpose              |
| --------- | -------------------- |
| PID       | Process isolation    |
| NET       | Network isolation    |
| MOUNT     | Filesystem isolation |
| UTS       | Hostname isolation   |
| IPC       | Shared memory        |
| USER      | UID mapping          |

---

## 4. Cgroups (Resource Control)

Limits:

* CPU
* Memory
* Disk I/O
* PIDs

---

## 5. Container Runtime Flow

```text
docker → containerd → shim → runc → process
```

---

## 6. Container vs VM

| Container     | VM              |
| ------------- | --------------- |
| Shares kernel | Separate kernel |
| Fast startup  | Slow            |
| Lightweight   | Heavy           |

---
