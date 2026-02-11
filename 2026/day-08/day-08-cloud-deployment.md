# Day 08 – Cloud Server Setup: Docker, Nginx & Web Deployment

## Objective

Deploy a real web server on AWS EC2 and understand:

- Cloud server provisioning
- SSH access
- Nginx installation
- Security group configuration
- Docker container deployment
- Log extraction and analysis
- Difference between OS-level service vs containerized service

---

# Part 1 – Launch EC2 & SSH Access

## Connected to Server via SSH

```bash
ssh -i my-key.pem ubuntu@<public-ip>
```

Verified connection:

```bash
uname -a
```

Confirmed Ubuntu 24.04 running on AWS.

---

# Part 2 – Install & Run Nginx (OS Level)

## Step 1 – Update System

```bash
sudo apt update
```

## Step 2 – Install Nginx

```bash
sudo apt install nginx -y
```

## Step 3 – Verify Service Status

```bash
systemctl status nginx
```

Output showed:

- Active: running
- Enabled: yes
- Listening on port 80

Check open ports:

```bash
ss -tulpn | grep 80
```

Observed:

```
0.0.0.0:80 LISTEN
```

## Test in Browser

Visited:

```
http://<public-ip>
```

Nginx welcome page loaded successfully.

---

# Part 3 – Security Group Configuration

Configured inbound rules:

| Type | Port | Source    |
| ---- | ---- | --------- |
| HTTP | 80   | 0.0.0.0/0 |
| SSH  | 22   | 0.0.0.0/0 |

Why needed?

Security groups act as firewall.
Even if service is running, traffic is blocked unless allowed here.

---

# Part 4 – Extract Nginx Logs

## View Logs

```bash
sudo tail -n 20 /var/log/nginx/access.log
```

Observed real browser requests:

```
GET / HTTP/1.1 200
GET /favicon.ico 404
```

## Save Logs to File

```bash
sudo tail -n 50 /var/log/nginx/access.log > ~/nginx-logs.txt
```

Explanation:

- `tail -n 50` → last 50 log lines
- `>` → redirect output
- `~/nginx-logs.txt` → save in home directory

Verified:

```bash
cat ~/nginx-logs.txt
```

---

# Part 5 – Install & Run Nginx Using Docker

## Verify Docker

```bash
systemctl status docker
docker --version
```

Docker was running.

## Run Nginx Container

```bash
sudo docker run -d -p 8080:80 nginx
```

Explanation:

- `-d` → detached mode
- `-p 8080:80` → map EC2 port 8080 to container port 80
- `nginx` → image name

Verify container:

```bash
sudo docker ps
```

Output showed:

```
0.0.0.0:8080->80/tcp
```

Meaning:

Public port 8080 forwards traffic to container's port 80.

---

# Open Security Group for Docker

Added inbound rule:

| Type       | Port | Source    |
| ---------- | ---- | --------- |
| Custom TCP | 8080 | 0.0.0.0/0 |

Now accessed:

```
http://<public-ip>:8080
```

Docker Nginx welcome page loaded successfully.

---

# Architecture Understanding

## OS-Level Nginx

- Installed directly on EC2
- Runs on port 80
- Managed by systemd
- Affects host OS

Access:

```
http://<public-ip>
```

---

## Docker Nginx

- Runs inside isolated container
- Internal port 80
- Exposed externally via 8080
- Does NOT affect host OS packages

Access:

```
http://<public-ip>:8080
```

---

# Logs Observed

Example log entry:

```
36.255.xx.xx - - [11/Feb/2026] "GET / HTTP/1.1" 200
```

Meaning:

- External IP accessed server
- Request successful (200)
- Nginx serving traffic correctly

---

# Commands Used

```bash
sudo apt update
sudo apt install nginx -y
systemctl status nginx
ss -tulpn | grep 80
sudo tail -n 50 /var/log/nginx/access.log
sudo docker run -d -p 8080:80 nginx
sudo docker ps
sudo systemctl enable nginx
```

---

# Challenges Faced

- Port 8080 initially not accessible
- Fixed by updating Security Group
- Understood difference between localhost vs public IP
- Learned that cloud firewall blocks traffic even if service runs

---

# Key Learnings

- Security Groups act as cloud firewall
- Same public IP can serve multiple services via different ports
- Docker isolates applications from host OS
- Port mapping controls external access
- Logs confirm real traffic and help debugging
- Always verify with `ss`, `systemctl`, `docker ps`

---

# Production Insight

In real DevOps environments:

- Applications run inside containers
- Nginx often runs as reverse proxy
- Logs are critical for debugging
- Firewall rules must align with service ports
- Port conflicts must be managed carefully

---

# Final Result

✅ EC2 Nginx running on port 80  
✅ Docker Nginx running on port 8080  
✅ Logs extracted successfully  
✅ Security groups configured correctly  
✅ Public access verified

---

# What I Built Today

A real cloud server with:

- Infrastructure
- Web server
- Containerized deployment
- Network security configuration
- Log analysis

This is foundational DevOps work.

---

# Hashtags

#90DaysOfDevOps
#DevOpsKaJosh
#TrainWithShubham
#AWS
#Docker
#Nginx
