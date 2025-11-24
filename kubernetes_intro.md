# Lecture 10 – Kubernetes Introduction & Architecture

## What is Kubernetes?

Kubernetes (K8s) is an open-source **container orchestration platform**.

Think of it as the **operating system for your data center**. It is responsible for:

* Deploying containers
* Scaling applications
* Self-healing (restart, replace failed containers)
* Networking containers
* Managing storage
* Rolling updates with zero downtime

Kubernetes works using **declarative state management**:

> You declare *what you want* → Kubernetes figures out *how to achieve it*.

---

## Kubernetes Architecture Overview

Kubernetes follows a **master–worker (control plane–data plane)** architecture.

### Control Plane (Brain)

Responsible for **decision-making and cluster state**.

Components:

* kube-apiserver
* etcd
* kube-scheduler
* kube-controller-manager
* cloud-controller-manager

### Worker Nodes (Muscle)

Where **applications actually run**.

Components:

* kubelet
* kube-proxy
* Container Runtime
* Pods

---

## Control Plane Components

### kube-apiserver

* Entry point for all cluster operations
* Exposes REST API
* Validates, authenticates, authorizes requests
* Writes/reads data from etcd
* Stateless → can scale horizontally

---

### etcd

* Distributed key-value store
* **Source of truth** for Kubernetes
* Stores:

  * Desired state
  * Pod specs
  * Secrets (encrypted)
  * Node & cluster metadata

> If etcd is lost → cluster is lost

---

### kube-scheduler

* Watches for unscheduled Pods
* Chooses the best node based on:

  * CPU & memory
  * Taints & tolerations
  * Affinity rules
  * Pod priority

---

### kube-controller-manager

Runs multiple **control loops**:

* ReplicaSet controller
* Deployment controller
* Node controller
* Job controller

Loop logic:

```
while true:
  compare desired vs actual state
  fix differences
```

---

### cloud-controller-manager

(Cloud environments only)

* Integrates with AWS, Azure, GCP
* Manages:

  * Load balancers
  * Cloud routes
  * Cloud disks

---

## Worker Node Components

### kubelet

* Node agent
* Watches API server for assigned Pods
* Pulls images
* Starts containers
* Reports Pod status

---

### kube-proxy

* Implements Service networking
* Uses iptables or IPVS
* Load balances traffic to Pods

---

### Container Runtime

* Runs containers via CRI
* Examples:

  * containerd (default)
  * CRI-O

---
