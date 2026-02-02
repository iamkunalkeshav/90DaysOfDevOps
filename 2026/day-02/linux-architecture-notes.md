# Linux Architecture – Notes (Day 02)

## 1. Core Components of Linux

### Kernel
- Core of the OS
- Directly interacts with hardware
- Manages:
  - CPU scheduling
  - Memory management
  - Process management
  - Device drivers
- Runs in **kernel space**

### User Space
- Where user applications run
- Examples:
  - Shell (bash)
  - System utilities (ls, ps, top)
  - Applications (nginx, docker)
- Cannot directly access hardware

### Init System (systemd)
- First process started after boot (PID 1)
- Responsible for:
  - Starting services
  - Restarting failed services
  - Managing system state

---

## 2. Process Creation & Management

### How a Process is Created
1. A parent process calls `fork()`
2. A child process is created
3. Child may call `exec()` to run a new program

Each process has:
- PID (Process ID)
- PPID (Parent Process ID)
- State
- Memory & CPU usage

---

## 3. Process States

- **Running (R)** – Process is executing on CPU
- **Sleeping (S)** – Waiting for an event (I/O, timer)
- **Uninterruptible Sleep (D)** – Waiting for disk/network
- **Stopped (T)** – Paused manually (Ctrl+Z)
- **Zombie (Z)** – Process finished but not cleaned by parent

Zombie processes indicate bad process handling.

---

## 4. systemd & Why It Matters

- systemd is the default init system in modern Linux
- Uses **units** to manage system resources

Common unit types:
- service (.service)
- target (.target)
- socket (.socket)

Why systemd is important:
- Automatic service restart
- Faster boot time
- Centralized logging (journald)

---

## 5. Daily Linux Commands (DevOps Use)

- `ps aux` → View running processes
- `top` / `htop` → Monitor CPU & memory usage
- `systemctl status <service>` → Check service health
- `journalctl -u <service>` → View service logs
- `kill / kill -9` → Stop problematic processes

---

## 6. Why This Matters for DevOps

- Helps debug crashed services
- Identify CPU/memory bottlenecks
- Understand why services fail or restart
- Essential for incident response
