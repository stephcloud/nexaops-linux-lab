# NexaOps Linux Lab — Commands Reference
## NXOPS-001B | Module 1 Foundations

---

## Task 1 — Navigation & files

| Command | What it does |
|---|---|
| `pwd` | Print current working directory |
| `ls -la` | List all files including hidden, with full details |
| `cd logs` | Move into the logs directory |
| `cd ..` | Go up one directory level |
| `cd ~` | Go to home directory from anywhere |
| `mkdir nexaops` | Create a directory called nexaops |
| `touch app.log` | Create an empty file called app.log |
| `tree .` | Show folder structure visually |

## Task 2 — Permissions

| Command | What it does |
|---|---|
| `ls -l deploy.sh` | Show permissions of deploy.sh |
| `chmod +x deploy.sh` | Add execute permission to deploy.sh |
| `chmod 755 deploy.sh` | Set permissions to rwxr-xr-x exactly |
| `./deploy.sh` | Run the deploy script |

## Task 3 — Processes

| Command | What it does |
|---|---|
| `top` | Live view of running processes sorted by CPU |
| `htop` | Cleaner colour version of top |
| `ps aux` | List all running processes with details |
| `ps aux | wc -l` | Count total number of running processes |
| `echo $$` | Print PID of current bash session |
| `pgrep bash` | Find PID of processes named bash |
| `kill <PID>` | Send SIGTERM — politely stop a process |
| `kill -9 <PID>` | Send SIGKILL — force stop a process immediately |
| `pkill <name>` | Kill a process by name |

## Task 4 — Shell scripting

| Command | What it does |
|---|---|
| `chmod +x check_log.sh` | Make check_log.sh executable |
| `./check_log.sh` | Run the check_log script |
| `bash -x check_log.sh` | Run in debug mode — prints every command as it executes |

## Task 5 — Pipes, grep & redirection

| Command | What it does |
|---|---|
| `grep "ERROR" app.log` | Print all lines containing ERROR |
| `grep -c "ERROR" app.log` | Count lines containing ERROR |
| `grep "ERROR" app.log > error_report.txt` | Save ERROR lines to a file |
| `grep "ERROR" app.log >> error_report.txt` | Append ERROR lines to a file |
| `grep -v "timeout" app.log` | Show lines that do NOT contain timeout |
| `cat app.log | grep "ERROR" | wc -l` | Count ERROR lines via pipeline |
| `wc -l error_report.txt` | Count lines in error_report.txt |
