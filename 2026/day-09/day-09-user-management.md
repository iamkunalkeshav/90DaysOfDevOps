# Day 09 – Linux User & Group Management Challenge

## Overview

Today I practiced real Linux system administration by:

- Creating users
- Creating groups
- Assigning users to multiple groups
- Creating shared directories
- Configuring proper permissions
- Using SetGID for group inheritance

This simulates real DevOps team collaboration environments.

---

# Task 1 – Create Users

## Users Created

- tokyo
- berlin
- professor
- nairobi

## Commands Used

```bash
sudo useradd -m tokyo
sudo useradd -m berlin
sudo useradd -m professor
sudo useradd -m nairobi
```

## Verification

```bash
awk -F: '$3 >= 1000 {print $1}' /etc/passwd
```

Confirmed home directories exist:

```bash
ls -l /home
```

---

# Task 2 – Create Groups

## Groups Created

- developers
- admins
- project-team

## Commands Used

```bash
sudo groupadd developers
sudo groupadd admins
sudo groupadd project-team
```

## Verification

```bash
grep -E 'developers|admins|project-team' /etc/group
```

---

# Task 3 – Assign Users to Groups

## Group Assignments

- tokyo → developers
- berlin → developers, admins
- professor → admins
- nairobi → project-team
- tokyo → project-team

## Commands Used

```bash
sudo usermod -aG developers tokyo
sudo usermod -aG developers berlin
sudo usermod -aG admins berlin
sudo usermod -aG admins professor
sudo usermod -aG project-team nairobi
sudo usermod -aG project-team tokyo
```

## Verification

```bash
groups tokyo
groups berlin
groups professor
groups nairobi
```

---

# Task 4 – Shared Developer Directory

## Step 1: Create Directory

```bash
sudo mkdir /opt/dev-project
```

## Step 2: Change Group Ownership

```bash
sudo chgrp developers /opt/dev-project
```

## Step 3: Set Permissions (775)

```bash
sudo chmod 775 /opt/dev-project
```

## Step 4: Enable SetGID (Important)

```bash
sudo chmod g+s /opt/dev-project
```

### Why SetGID?

This ensures any new file created inside inherits the directory’s group (`developers`) automatically.

---

## Testing Access

```bash
sudo -u tokyo touch /opt/dev-project/tokyo2.txt
sudo -u berlin touch /opt/dev-project/berlin2.txt
```

## Verification

```bash
ls -l /opt/dev-project
```

Result:

- Files owned by respective users
- Group automatically set to `developers`
- No manual group change required

---

# Task 5 – Team Workspace

## Step 1: Create Workspace Directory

```bash
sudo mkdir /opt/team-workspace
```

## Step 2: Assign Group

```bash
sudo chgrp project-team /opt/team-workspace
```

## Step 3: Set Permissions

```bash
sudo chmod 775 /opt/team-workspace
sudo chmod g+s /opt/team-workspace
```

## Step 4: Test File Creation

```bash
sudo -u nairobi touch /opt/team-workspace/nairobi.txt
sudo -u tokyo touch /opt/team-workspace/tokyo.txt
```

## Verification

```bash
ls -l /opt/team-workspace
```

Confirmed:
- Group = project-team
- Inheritance working properly

---

# Commands Used

- useradd
- userdel
- groupadd
- usermod
- groups
- chgrp
- chmod
- chmod g+s
- ls -l
- sudo -u

---

# What I Learned

- How Linux users and groups work internally
- How to assign users to multiple groups
- How to configure shared directories securely
- Why 775 permissions are useful in team environments
- How SetGID ensures group inheritance
- How to test permissions using `sudo -u`

---

# Real DevOps Use Case

This setup is commonly used for:

- Development team shared folders
- CI/CD build directories
- Log collection directories
- Project collaboration environments

Understanding user/group management is critical for secure server administration.

---

# Day 09 Completed ✅
