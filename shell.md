
# Lecture 4 – Shell Scripting

## 1. Shell Script Basics

Shebang:
```bash
#!/bin/bash
```
Defines the interpreter.

---

## 2. Common Scripts

- Print date/time
- Disk usage
- File existence check
- Add numbers
- Backup directories
- Internet connectivity check

---

## 3. Bash Variables & Expansion

- ${var} – value
- ${#var} – length
- ${var^^} – uppercase
- ${var,,} – lowercase

Bash-only features will **not work in /bin/sh**.

---

## 4. /bin/sh vs /bin/bash

| Feature | sh | bash |
|-----|----|-----|
| Portability | High | Medium |
| Features | Minimal | Rich |
| Arrays | ❌ | ✅ |
| [[ ]] | ❌ | ✅ |

---

## 5. Writing Standard Shell Scripts

Best Practices:
- Use comments
- Validate arguments
- Use set -e
- Check root privileges
- Handle errors gracefully

---

## 6. Reusable Scripts with Functions

- Write functions in utils.sh
- Import using source
- Pass arguments
- Use timestamps for uniqueness

---

## 7. ACLs (Access Control Lists)

ACLs allow **fine-grained permissions** beyond owner/group/others.

Key Commands:
- getfacl – view ACLs
- setfacl – set/remove ACLs

Use cases:
- Shared team directories
- Multi-user access control

---

## Final Outcome
By mastering these topics, you gain:
- Strong Linux foundation
- Shell automation skills
- Cloud & AWS basics
- DevOps & microservices understanding

These skills are essential for real-world DevOps and cloud engineering roles.

