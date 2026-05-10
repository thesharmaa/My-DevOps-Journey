````md
# Linux Practice Notes (Deep Version)

---

## 1) Linux Architecture Mindset (How to Think)

Linux troubleshooting is easier when you map issues into layers:

- Application layer: app code, configs, dependencies  
- Process layer: running/stuck/zombie processes, scheduling  
- OS layer: memory, CPU, filesystem, permissions, users/groups  
- Service layer: systemd, startup order, service failures  
- Network layer: DNS, ports, routes, firewall, connectivity  
- Storage layer: disk full vs disk slow, mount issues, I/O waits  

**Rule:** Don’t jump to random commands. Always narrow down layer by layer.

---

## 2) Kernel, User Space, and System Calls (Core Theory)

Kernel is the core of OS: manages CPU, memory, devices, filesystems.  
User space is where apps run with limited privileges.  

Apps request privileged operations using system calls (open file, create process, network sockets).

This separation provides stability + security (app crash != kernel crash).

**Why DevOps cares:**

- High CPU? kernel scheduling involved.  
- Slow app? maybe blocked syscall waiting on disk/network.  
- Permission denied? kernel permission model rejected request.  

---

## 3) Process Lifecycle + Scheduling (Interview Depth)

### States:
- R → running/runnable  
- S → interruptible sleep (waiting for event)  
- D → uninterruptible sleep (I/O wait)  
- Z → zombie  
- T → stopped  

### Commands:
```bash
ps aux
ps -ef
ps -eo pid,ppid,stat,%cpu,%mem,cmd --sort=-%cpu | head
top
htop
pidstat 1
````

### Key insights:

* D state processes cannot be killed with kill -9 immediately
* Load average includes I/O wait, not just CPU usage
* Nice value range: -20 (highest priority) to 19 (lowest)

---

## 4) Boot + Init + systemd (Operationally Important)

### Boot flow:

BIOS/UEFI → Bootloader → Kernel → systemd (PID 1) → Services

### Commands:

```bash
systemctl status <service>
systemctl restart <service>
systemctl is-enabled <service>
journalctl -u <service>
journalctl -b
journalctl -b -1
```

### Troubleshooting:

* Check service enable status
* Check dependencies
* Validate config before restart

---

## 5) Linux Filesystem Hierarchy (Practical Use)

* `/etc` → configurations
* `/var/log` → logs
* `/var/lib` → runtime data
* `/usr/bin` → binaries
* `/tmp` → temporary files
* `/proc` → live system info
* `/dev` → devices

**Debug flow:**

* config → `/etc`
* logs → `/var/log`
* runtime → `/var/lib`

---

## 6) Permissions Model (Beyond chmod)

Each file:

* Owner (u)
* Group (g)
* Others (o)

### Permissions:

* r = read
* w = write
* x = execute

### Directories:

* r → list files
* w → create/delete
* x → access directory

### Commands:

```bash
chmod u+x script.sh
chmod g-w file
chmod o-rwx secret.txt
```

### Numeric:

* 7 = rwx
* 6 = rw-
* 5 = r-x
* 4 = r--
* 0 = ---

---

## 7) Ownership and Group Strategy

```bash
chown user file
chown user:group file
chown -R user:group dir
chgrp group file
usermod -aG group user
```

**Real-world pattern:**

* Owner → service/app account
* Group → team access
* Principle → least privilege

---

## 8) CPU & Memory Troubleshooting

### Commands:

```bash
uptime
top
vmstat 1
free -m
pidstat 1
```

### Interpretation:

* High %us → user app load
* High %sy → kernel overhead
* High %wa → I/O wait
* swap activity → memory pressure

Linux uses free memory as cache → focus on **available memory**, not free.

---

## 9) CPU Blocked Tasks & I/O Wait Framework

* b high + %wa high → disk I/O bottleneck
* b high + %wa low → lock/network stall
* b low + %wa high → slow storage latency
* all low but slow → app/network issue

Check:

```bash
iostat -xz 1
```

---

## 10) Disk Troubleshooting

### Capacity:

```bash
df -h
du -sh *
find / -size +1G
```

### Performance:

```bash
iostat -xz 1
```

Key metrics:

* %util → disk saturation
* await → latency
* queue → backlog

⚠️ Deleting files may not free space if process still holds file handle.

---

## 11) Logs (Most Important Debug Tool)

### Sources:

* App logs
* System logs
* Service logs

### Commands:

```bash
journalctl -u service
journalctl -f
journalctl -p err
```

### Workflow:

1. Check service status
2. Pull logs
3. Follow live logs
4. Filter errors

---

## 12) Networking Commands

```bash
ping host
curl -I http://host
ss -tulnp
dig domain
nslookup domain
traceroute host
```

### Triage:

* DNS issue → resolution fails
* Port issue → service not listening
* Firewall issue → blocked externally

---

## 13) Script Execution Issues

If permission denied:

```bash
chmod +x script.sh
```

Check:

* shebang (#!/bin/bash)
* directory execute permission
* line endings (CRLF issue)

---

## 14) Cloud Deployment Learnings (EC2 + NGINX)

Common issues:

* SSH key permissions wrong
* File ownership mismatch
* NGINX 403 errors

### 403 checklist:

* index.html exists
* directory has execute permission
* correct ownership
* nginx config valid
* port open (80/443)

---

## 15) Golden Troubleshooting Playbook

When server is slow/down:

### 1. Scope

What is affected?

### 2. System health

```bash
uptime
top
free -m
df -h
```

### 3. Process

```bash
ps aux
systemctl status service
```

### 4. Logs

```bash
journalctl -u service -n 100
```

### 5. Disk/I/O

```bash
vmstat 1
iostat -xz 1
```

### 6. Network

```bash
ss -tulnp
curl
dig
```

### 7. Fix + verify

Apply minimal safe fix → validate

### 8. Prevent

Document + monitoring + alerts

---

```
```
