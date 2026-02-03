# Linux Practice – Day 04 (Processes & Services)

This note documents hands-on Linux practice focused on
process inspection, systemd services, and basic log troubleshooting.
All commands were executed on a live Linux server.

---

## 1. Process Checks

- `ps aux`  
  Lists all running processes with CPU, memory usage, and ownership.

- `ps aux | head`  
  Quickly view top processes and identify PID 1 (systemd).

- `ps aux | grep ssh`  
  Confirms whether the SSH process is running and shows active SSH sessions.

- `top`  
  Displays live CPU and memory usage to identify performance issues.

---

## 2. Service Checks (systemd)

- `systemctl status ssh`  
  Checks SSH service health, uptime, PID, resource usage, and recent logs.

- `systemctl list-units --type=service --state=running`  
  Lists all currently running services managed by systemd.

- `systemctl restart ssh`  
  Restarts the SSH service if it becomes unresponsive.

---

## 3. Log Checks

- `journalctl -u ssh`  
  Displays logs related to the SSH service, including login attempts.

- `journalctl -u ssh --no-pager | tail`  
  Shows the most recent SSH log entries for quick debugging.

- `tail -n 20 /var/log/syslog`  
  Displays recent system-wide log messages.

---

## 4. Mini Troubleshooting Flow (SSH Example)

- Check if SSH process is running  
  Use `ps aux | grep ssh`

- Verify SSH service status  
  Use `systemctl status ssh`

- Inspect recent SSH logs  
  Use `journalctl -u ssh --no-pager | tail`

---

## Why This Practice Matters

- Helps debug service and access issues faster
- Improves understanding of systemd and logs
- Strengthens fundamentals required for DevOps work
