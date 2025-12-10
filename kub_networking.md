
# Lecture 15 – Kubernetes Networking Model

## Core Networking Rules

1. Pod-to-Pod without NAT
2. Node-to-Pod without NAT
3. Pod IP same everywhere

---

## Container-to-Container

* Same Pod
* Same network namespace
* Communicate via localhost

---

## Pod-to-Pod Networking

### Same Node

* veth pair
* Linux bridge

### Different Nodes

* Routed via Pod CIDR
* Handled by CNI

---

## CNI Plugins

* Calico
* Flannel
* Cilium
* AWS VPC CNI

---

## Pod-to-Service Networking

* Implemented via kube-proxy
* iptables or IPVS
* Uses DNAT

---

## Internet Access

### Egress

Pod → Node → Internet (SNAT)

### Ingress

* LoadBalancer Service
* Ingress Controller (L7 routing)

---

## Networking Summary Table

| Layer                 | Mechanism       |
| --------------------- | --------------- |
| Container → Container | localhost       |
| Pod → Pod             | veth + routing  |
| Pod → Service         | iptables / IPVS |
| DNS                   | CoreDNS         |
| Internet Ingress      | LB / Ingress    |

---

## Final Takeaway

Kubernetes networking is **simple in rules, complex in implementation**.
Understanding it is key to debugging and designing production clusters.
