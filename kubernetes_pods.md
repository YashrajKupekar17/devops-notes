
# Lecture 11 – Pods (Deep Dive)

## What is a Pod?

A Pod is the **smallest deployable unit** in Kubernetes.

A Pod:

* Runs one or more containers
* Shares network namespace (same IP, localhost)
* Shares volumes
* Is ephemeral

---

## Pod Lifecycle (High Level)

1. kubectl submits Pod YAML
2. API server validates & stores in etcd
3. Scheduler assigns node
4. kubelet creates containers
5. Pod becomes Running

---

## Pod Creation Flow (Detailed)

1. `kubectl apply -f pod.yaml`
2. API Server:

   * AuthN / AuthZ
   * Admission controllers
   * Writes Pod to etcd
3. Scheduler assigns node
4. kubelet:

   * Creates sandbox
   * Pulls images
   * Starts containers
   * Updates Pod status
5. Pod Ready after probes pass

---

## Pod States

* Pending
* Running
* Succeeded
* Failed
* Unknown

---

## Why Pods Are Not Self-Healing

If a Pod dies:

* Kubernetes does **nothing** by default

That’s why controllers like ReplicaSets exist.

---
