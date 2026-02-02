# Linux Commands Cheat Sheet – Day 03

This cheat sheet contains commonly used Linux commands for
process management, file system operations, and networking troubleshooting.
These are the commands I would use during real production incidents.

---

## 1. Process Management Commands

- `top`  
  View live CPU and memory usage of running processes.

- `ps aux`  
  List all running processes with CPU and memory usage.

- `ps aux | grep <process>`  
  Check whether a specific process is running.

- `htop`  
  Enhanced interactive process viewer (if installed).

- `kill <PID>`  
  Gracefully stop a process.

- `kill -9 <PID>`  
  Force stop an unresponsive process.

- `uptime`  
  Show system running time and load average.

- `who`  
  Show users currently logged into the system.

---

## 2. Service Management (systemd)

- `systemctl status <service>`  
  Check service health and status.

- `systemctl start <service>`  
  Start a service.

- `systemctl stop <service>`  
  Stop a service.

- `systemctl restart <service>`  
  Restart a service.

- `systemctl list-units --type=service`  
  List active system services.

---

## 3. File System Commands

- `pwd`  
  Show current working directory.

- `ls -l`  
  List files with permissions and ownership.

- `cd <directory>`  
  Change directory.

- `mkdir <dir>`  
  Create a directory.

- `touch <file>`  
  Create an empty file.

- `cat <file>`  
  View file contents.

- `less <file>`  
  View large files or logs safely.

- `grep <pattern> <file>`  
  Search text inside a file.

- `df -h`  
  Check disk space usage.

- `du -sh <dir>`  
  Check directory size.

---

## 4. Networking Commands

- `ip addr`  
  Display IP address and network interfaces.

- `ping <host>`  
  Test basic network connectivity.

- `curl <url>`  
  Test HTTP/HTTPS services and APIs.

- `ss -tulpn`  
  View listening ports and services.

---

## 5. Logs & Debugging

- `journalctl -u <service>`  
  View logs for a systemd service.

- `journalctl -xe`  
  View recent system errors.

- `history`  
  Show previously executed commands.

---

## Why These Commands Matter for DevOps

- Quickly identify performance issues
- Debug crashed or misbehaving services
- Inspect logs during incidents
- Validate network connectivity
- Reduce downtime and recovery time
