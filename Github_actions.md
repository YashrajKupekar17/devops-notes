
# Lecture 18 – CI with GitHub Actions (DevSecOps)

## What This Pipeline Does

* Build Java app
* Run tests
* Perform SAST & SCA
* Build Docker image
* Scan container
* Test container
* Push trusted image

---

## DevSecOps Philosophy

Security is applied **before** software is shipped.

---

## Key Pipeline Stages

| Stage        | Purpose            |
| ------------ | ------------------ |
| Checkout     | Fetch code         |
| Build        | Compile            |
| Lint         | Code quality       |
| SAST         | Source security    |
| SCA          | Dependency scan    |
| Docker Build | Immutable image    |
| Image Scan   | CVE detection      |
| Runtime Test | Smoke test         |
| Push         | Artifact promotion |

---

## Security Tools Used

* CodeQL (SAST)
* OWASP Dependency Check (SCA)
* Trivy (Container scan)

---

## Why Secrets Are Used

* Secure credentials
* Prevent leaks
* Zero-trust approach

---

## Industry-Grade Features

* Shift-left security
* Quality gates
* Immutable artifacts
* Centralized vulnerability reporting

---
