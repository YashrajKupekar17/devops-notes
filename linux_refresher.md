
# Lecture 3 – AWS & Linux Fundamentals

## 1. AWS Global Infrastructure

### Regions
- Geographically isolated
- Independent resources
- Example: ap-south-1

### Availability Zones
- Multiple AZs per region
- Fault tolerance

---

## 2. VPC Basics

A VPC is a **private virtual network**.

You define:
- CIDR blocks
- Subnets
- Route tables
- Gateways
- Security rules

---

## 3. Subnets

- Each subnet belongs to one AZ
- Public vs Private subnets

Best Practices:
- Multi-AZ
- NAT for private subnets
- Proper CIDR planning

---

## 4. EC2 Key Configuration Fields

- AMI – OS image
- Instance type – CPU/RAM
- Key pair – SSH access
- Network settings – VPC, subnet, SG
- Storage – EBS volumes
- IAM Role – permissions
- User data – bootstrapping

---

## 5. Linux Basics

### Linux Architecture
- Kernel manages CPU, memory, devices
- Shell is the user interface

---

### Basic Commands
- pwd, cd, mkdir, touch, cat, echo

### File Management
- ls, cp, mv, rm, find, df, du

### Process Management
- ps, top, htop, kill, jobs, fg, bg

---

## 6. Permissions & Ownership

- chmod – permissions
- chown – owner
- chgrp – group

---
