
# Lecture 12 – ReplicaSet (RS)

## What is a ReplicaSet?

A ReplicaSet ensures **a fixed number of Pod replicas** are always running.

It continuously compares:

* Desired replicas
* Actual Pods

---

## ReplicaSet YAML

```yaml
apiVersion: apps/v1
kind: ReplicaSet
spec:
  replicas: 3
```

---

## ReplicaSet Internal Workflow

1. RS object stored in etcd
2. ReplicaSet controller detects mismatch
3. Creates or deletes Pods
4. Scheduler assigns Pods
5. kubelet runs containers

---

## Failure Handling

| Failure           | Action                   |
| ----------------- | ------------------------ |
| Pod crash         | New Pod created          |
| Node failure      | Pods recreated elsewhere |
| Manual Pod delete | Replacement Pod          |

---

## Important Note

ReplicaSets **do not handle rolling updates**.

They are usually managed by Deployments.

---
