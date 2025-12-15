# Lecture 16 – Kubernetes Horizontal Pod Autoscaler (HPA)

## What is HPA?

Horizontal Pod Autoscaler (HPA) automatically adjusts the **number of pod replicas** in a Deployment based on metrics such as:

* CPU utilization
* Memory utilization
* Custom / external metrics

In this lecture:

* Metric: CPU
* Trigger: > 50% CPU
* Scaling type: Horizontal (pods)

---

## HPA Architecture (Conceptual Flow)

User Load → Service → Pods → Metrics Server → HPA Controller → Replica scaling

---

## Step 1: Metrics Server (Mandatory)

HPA **cannot work without Metrics Server**.

Why?

* HPA needs live CPU/memory metrics
* Without it, CPU shows 0%

Install:

```bash
kubectl apply -f https://github.com/vilasvarghese/docker-k8s/blob/master/yaml/metricServer/metric-server.yaml
```

Verify:

```bash
kubectl get pods -n kube-system | grep metrics-server
kubectl top nodes
```

---

## Step 2: Deployment for HPA

CPU-intensive sample app.

Key requirement:

> **CPU requests MUST be defined**

HPA formula:

```
CPU Utilization = Current CPU Usage / CPU Request
```

Without requests → no scaling.

---

## Step 3: Service

Why Service?

* Provides stable endpoint
* Used for load generation

---

## Step 4: HPA Resource

Key fields:

* minReplicas
* maxReplicas
* targetCPUUtilizationPercentage

Monitor:

```bash
kubectl get hpa -w
```

---

## Step 5: Generate Load

```bash
kubectl run -i --tty load-generator --rm \
--image=busybox --restart=Never -- \
/bin/sh -c "while sleep 0.01; do wget -q -O- http://hpa-demo-deployment; done"
```

Expected behavior:

* CPU crosses threshold
* Replicas increase

---

## Scale Down Behavior

* Load removed
* HPA waits (cooldown)
* Gradual scale-down

---

## Common Issues

| Issue      | Cause                  | Fix              |
| ---------- | ---------------------- | ---------------- |
| CPU = 0%   | Metrics Server missing | Install it       |
| No scaling | CPU request missing    | Add requests.cpu |
| No pods    | Label mismatch         | Fix selector     |

---

## Interview Summary

HPA uses Metrics Server to monitor average pod CPU utilization and dynamically adjusts replicas to maintain desired thresholds.

---