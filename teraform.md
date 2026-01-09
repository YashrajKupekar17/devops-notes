
# Lecture 20 – Terraform Basics

## What is Terraform?

Terraform is an **Infrastructure as Code (IaC)** tool.

It lets you:

* Define infra in code
* Version control infra
* Reproduce environments

---

## Terraform Lifecycle

| Command | Purpose              |
| ------- | -------------------- |
| init    | Initialize providers |
| plan    | Preview changes      |
| apply   | Create/update infra  |
| destroy | Delete infra         |

---

## Benefits

* Consistency
* Speed
* Version control
* Multi-cloud

---

# Lecture 21 – AWS + Terraform Concepts

## VPC & Subnets

* VPC: Isolated network
* Public subnet: Internet access
* Private subnet: No direct internet

---

## Terraform State

* Tracks infrastructure
* Stored in terraform.tfstate

Best practice:

* Remote state (S3)
* Locking (DynamoDB)

---

## Implicit Dependencies

Terraform automatically determines resource order based on references.

---

## IP Types

| Type       | Usage             |
| ---------- | ----------------- |
| Private IP | Internal          |
| Public IP  | Internet          |
| Elastic IP | Persistent public |

---

## Variables in Terraform

* Input variables
* Output variables
* Local variables

---

## Final Takeaway

Terraform + Kubernetes + CI/CD form the backbone of modern DevOps automation.
