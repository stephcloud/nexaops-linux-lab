# NexaOps Linux Lab — NXOPS-001B

A hands-on Linux fundamentals lab simulating day one on a real server. Part of the NexaOps DevOps Bootcamp, Module 1 Foundations Track.

---

## Prerequisites

```bash
# Verify git is installed
git --version

# Install tree and htop
sudo apt-get install -y tree htop
```

> Windows users: you need WSL2 running Ubuntu. Open PowerShell as Administrator and run `wsl --install`, then restart.

---

## Repo structure
nexaops-linux-lab/

├── commands.md        # Every command run in this lab with explanations

├── deploy.sh          # Script demonstrating chmod 755 permissions

├── check_log.sh       # Bash script that checks if app.log exists and creates it if not

├── docs/

│   └── screenshots/   # Terminal screenshots for acceptance criteria

└── .gitignore

---

## How to reproduce this lab

### 1. Clone and set up

```bash
git clone https://github.com/stephcloud/nexaops-linux-lab.git
cd nexaops-linux-lab
mkdir -p docs/screenshots
```

### 2. Set up deploy.sh

```bash
cat > deploy.sh << 'DEPLOYEOF'
echo "NexaOps deploy script running"
DEPLOYEOF

chmod 755 deploy.sh
./deploy.sh
```

Expected output:
NexaOps deploy script running

### 3. Set up check_log.sh

```bash
cat > check_log.sh << 'CHECKEOF'
#!/usr/bin/env bash
set -e

# NexaOps log file check
# Checks if app.log exists. Creates it if not.

LOG_FILE="app.log"

if [ -f "$LOG_FILE" ]; then
  echo "File exists: $LOG_FILE"
else
  touch "$LOG_FILE"
  echo "File created: $LOG_FILE"
fi
CHECKEOF

chmod +x check_log.sh
```

Test both branches:
```bash
# Test when file exists
./check_log.sh

# Test when file does not exist
rm app.log
./check_log.sh

# Run again to confirm it detects the file
./check_log.sh
```

Expected output:
File exists: app.log

File created: app.log

File exists: app.log

### 4. Generate app.log with test data

```bash
cat > app.log << 'LOGEOF'
2024-01-15 07:00:01 INFO  App started successfully
2024-01-15 07:01:03 INFO  Connected to database
2024-01-15 07:02:11 WARN  Response time above threshold: 850ms
2024-01-15 07:03:44 ERROR Failed to write to disk: permission denied
2024-01-15 07:04:02 INFO  Retry attempt 1 of 3
2024-01-15 07:04:30 INFO  Retry attempt 2 of 3
2024-01-15 07:05:18 ERROR Database connection lost: timeout after 30s
2024-01-15 07:06:30 ERROR Timeout on payment service: no response
2024-01-15 07:07:01 WARN  Falling back to cached data
2024-01-15 07:07:45 INFO  Service partially recovered
2024-01-15 07:08:12 INFO  All systems nominal
LOGEOF
```

### 5. Generate the error report

```bash
grep "ERROR" app.log > error_report.txt
cat error_report.txt
wc -l error_report.txt
```

Expected output:
2024-01-15 07:03:44 ERROR Failed to write to disk: permission denied

2024-01-15 07:05:18 ERROR Database connection lost: timeout after 30s

2024-01-15 07:06:30 ERROR Timeout on payment service: no response

3 error_report.txt

### 6. Verify permissions

```bash
ls -la
```

You should see `-rwxr-xr-x` on both `deploy.sh` and `check_log.sh`.

---

## Key concepts covered

| Topic | Commands |
|---|---|
| Navigation | `pwd`, `cd`, `ls -la`, `mkdir`, `touch`, `tree` |
| Permissions | `chmod +x`, `chmod 755`, reading `rwx` notation |
| Processes | `top`, `htop`, `ps aux`, `pgrep`, `kill`, `kill -9` |
| Shell scripting | shebang, `set -e`, `if/else`, `-f` file test |
| Text processing | `grep`, `grep -c`, `grep -v`, `wc -l`, `>`, `>>`, pipes |

---

> `error_report.txt` and `app.log` are excluded from git via `.gitignore`. Follow the steps above to regenerate them.

---

## Ticket reference

| Field | Value |
|---|---|
| Ticket ID | NXOPS-001B |
| Module | M1 — Linux & Shell Scripting |
| Track | Foundations |
| Estimate | 4–6 hours |

