# Terraform in Action – Important & Practical Topics

These notes focus on **how Terraform is actually used in real projects**, beyond basics like `init/plan/apply`.

---

## 1. Terraform Providers (How Terraform Talks to Clouds)

A **provider** is a plugin that lets Terraform talk to an external API (AWS, Azure, GCP, Kubernetes, GitHub, etc.).

Example:

```hcl
provider "aws" {
  region = "ap-south-1"
}
```

### Key Points

* Providers are downloaded during `terraform init`
* Providers are versioned (important for stability)
* One Terraform project can use **multiple providers**

Best practice:

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}
```

Why this matters:

* Prevents breaking changes
* Ensures reproducible builds

---

## 2. Terraform State (terraform.tfstate) – Deep Reality

Terraform state is **the brain of Terraform**.

It stores:

* What resources exist
* Their IDs (EC2 ID, subnet ID, etc.)
* Metadata and dependencies

### Why State Is Critical

Terraform does NOT query cloud APIs for everything every time.
Instead:

* It reads state
* Compares desired vs actual
* Decides what to create/update/delete

---

## 3. Remote State (Production Mandatory)

Never keep `terraform.tfstate` locally in teams.

### Remote State Using S3 + DynamoDB (AWS)

```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-state"
    key            = "prod/terraform.tfstate"
    region         = "ap-south-1"
    dynamodb_table = "terraform-locks"
    encrypt        = true
  }
}
```

### Why Remote State?

* Team collaboration
* Prevents state corruption
* Enables state locking

DynamoDB:

* Prevents **two engineers applying at the same time**

---

## 4. State Locking & Race Conditions

Problem:

* Two people run `terraform apply` simultaneously
* Infrastructure corruption

Solution:

* State locking (DynamoDB, Terraform Cloud)

Terraform behavior:

* Acquires lock before apply
* Releases lock after completion
* If lock exists → operation fails

---

## 5. Variables – Real Usage Patterns

### Input Variables

Used to parameterize infrastructure.

```hcl
variable "instance_type" {
  type    = string
  default = "t3.micro"
}
```

Usage:

```hcl
instance_type = var.instance_type
```

### tfvars Files (Environment-based)

```text
prod.tfvars
dev.tfvars
```

```bash
terraform apply -var-file=prod.tfvars
```

Used for:

* dev / staging / prod separation

---

## 6. Locals (Clean & DRY Terraform)

Locals help reduce repetition.

```hcl
locals {
  common_tags = {
    Project = "webapp"
    Owner   = "devops"
    Env     = var.environment
  }
}
```

Usage:

```hcl
tags = local.common_tags
```

---

## 7. Outputs (Terraform → Other Systems)

Outputs expose values after apply.

```hcl
output "instance_ip" {
  value = aws_instance.web.public_ip
}
```

Used for:

* CI/CD pipelines
* Passing infra data to scripts
* Debugging

---

## 8. Resource Dependencies (Implicit vs Explicit)

### Implicit Dependencies (Recommended)

```hcl
subnet_id = aws_subnet.public.id
```

Terraform understands order automatically.

### Explicit Dependencies (Rare)

```hcl
depends_on = [aws_internet_gateway.igw]
```

Use only when implicit dependency is not detectable.

---

## 9. Terraform Modules (Most Important in Real Projects)

Modules = reusable Terraform components.

### Folder Structure

```text
modules/
  vpc/
  ec2/
main.tf
```

### Module Definition

```hcl
module "vpc" {
  source = "./modules/vpc"
  cidr   = "10.0.0.0/16"
}
```

### Why Modules Matter

* Reusability
* Standardization
* Team scalability

Real companies:

* Have internal module registries

---

## 10. Count vs for_each (Very Important Interview Topic)

### count

```hcl
count = 3
```

Creates indexed resources: `[0], [1], [2]`

Problems:

* Index shift when deleting

### for_each (Preferred)

```hcl
for_each = { web = "t3.micro", api = "t3.small" }
```

Advantages:

* Stable resource identity
* Safer changes

---

## 11. Lifecycle Rules (Prevent Accidental Destruction)

```hcl
lifecycle {
  prevent_destroy = true
}
```

Other lifecycle options:

* create_before_destroy
* ignore_changes

Used for:

* Databases
* Critical resources

---

## 12. Terraform Plan as a Safety Gate

Never run `apply` blindly.

```bash
terraform plan -out=tfplan
terraform apply tfplan
```

Why?

* Review infra changes
* Required in CI pipelines

---

## 13. Terraform in CI/CD Pipelines

Typical flow:

```text
PR → terraform plan → approval → terraform apply
```

Best practices:

* Run plan on PR
* Apply only on main branch
* Use read-only credentials for plan

---

## 14. Handling Secrets (Do NOT Hardcode)

❌ Bad:

```hcl
password = "admin123"
```

✅ Good:

* Environment variables
* AWS Secrets Manager
* Terraform Cloud variables

Terraform automatically reads:

```text
TF_VAR_db_password
```

---

## 15. Terraform Destroy (Danger Zone)

```bash
terraform destroy
```

What it does:

* Deletes everything in state

Best practices:

* Never allow destroy in prod CI
* Use separate workspaces/accounts

---

## Final Mental Model

Terraform works by:

1. Reading configuration (desired state)
2. Reading state (known reality)
3. Creating an execution plan
4. Reconciling differences safely

> Terraform is not just a tool — it is a **controlled infrastructure change engine**.
