
# Lecture 13 – Deployment

## What is a Deployment?

A Deployment is the **recommended controller** for stateless applications.

It provides:

* Rolling updates
* Rollbacks
* Replica management
* Declarative updates

---

## Deployment → ReplicaSet → Pod

Deployment creates:

* ReplicaSets
* ReplicaSets create Pods

---

## Deployment Rollout Strategies

### RollingUpdate (default)

* Gradual replacement
* Zero downtime

### Recreate

* Stop all old Pods
* Start new Pods

---

## Deployment Commands

```bash
kubectl rollout status deployment/app
kubectl rollout history deployment/app
kubectl rollout undo deployment/app
kubectl scale deployment app --replicas=5
```

---

## How Deployments Are Stored

* /registry/deployments/
* /registry/replicasets/
* /registry/pods/

Each rollout creates a new ReplicaSet.
