

# Lecture 17 – GitHub Actions (Introduction)

## What is GitHub Actions?

GitHub Actions allows you to **automate workflows** triggered by repository events.

Examples:

* Push → build
* PR → test

Workflows are written in **YAML**.

---

## Core Components

| Term     | Meaning               |
| -------- | --------------------- |
| Workflow | Entire automation     |
| Job      | Group of steps        |
| Step     | Single command/action |
| Runner   | Machine executing job |
| Action   | Reusable logic        |

---

## Basic Workflow Structure

```yaml
name: Java Build
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-java@v4
      - run: mvn clean package
```

---

## What Happens on Push

1. GitHub detects push
2. Runner VM is created
3. Code is checked out
4. Build runs
5. Result shown in Actions tab

---

## Common Mistakes

* Wrong indentation
* Missing `.github/workflows`
* Java version mismatch

---
