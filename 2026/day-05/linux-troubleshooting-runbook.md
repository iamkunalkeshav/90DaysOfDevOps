# Linux Troubleshooting Runbook – Day 05

This runbook documents a basic Linux troubleshooting drill performed
on a live server. The target service for this drill is `ssh`.
The goal is to capture a quick system health snapshot and review logs
before taking any action.

---

## Target Service
- SSH (`sshd`)

---

## Environment Snapshot

- `uname -a`  
  Confirms kernel version, architecture, and that the system is running on AWS.

- `lsb_release -a`  
  Confirms the OS is Ubuntu 24.04 LTS.

---

## Filesystem Sanity Checks

- `mkdir /tmp/runbook-demo`  
  Verifies filesystem is writable.

- `cp /etc/hosts /tmp/runbook-demo/hosts-copy && ls -l /tmp/runbook-demo`  
  Confirms file creation and permissions work correctly.

---

## CPU & Memory Snapshot

- `top -b -n 1 | head`  
  Shows CPU usage, load average, memory usage, and running processes.
  CPU was mostly idle and no performance issues were observed.

- `free -h`  
  Confirms sufficient available memory and no swap usage.

---

## Disk Snapshot

- `df -h`  
  Confirms root disk has sufficient free space and no disk pressure.

---

## Network Snapshot

- `ss -tulpn | head`  
  Confirms services are listening on expected ports and networking is healthy.

---

## Logs Reviewed (SSH)

- `journalctl -u ssh -n 50 --no-pager`  
  Shows multiple failed SSH login attempts from external IPs.
  These were rejected successfully and indicate normal internet scan activity.

---

## Quick Findings

- System resources (CPU, memory, disk) are healthy
- SSH service is running correctly
- No critical errors found in logs
- Failed login attempts are expected and handled securely

---

## If This Worsens (Next Steps)

- Restart SSH service using `sudo systemctl restart ssh`
- Restrict SSH access using firewall or security groups
- Enable additional protections such as fail2ban
