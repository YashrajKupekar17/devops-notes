


# Lecture 14 – Kubernetes Services

## Why Services?

Pods are ephemeral:

* IPs change
* Pods restart

Services provide **stable networking**.

---

## What is a Service?

A Service provides:

* Stable virtual IP
* DNS name
* Load balancing

---

## Service Types

| Type         | Purpose                |
| ------------ | ---------------------- |
| ClusterIP    | Internal communication |
| NodePort     | Expose on node IP      |
| LoadBalancer | Cloud external access  |
| Headless     | Stateful apps          |

---

## Service Traffic Flow

Client → Service IP → kube-proxy → Pod IP

---

## DNS Format

```
<service>.<namespace>.svc.cluster.local
```

---
