# 🧠 Linux Troubleshooting Cheat Sheet (DevOps / SRE)

A practical collection of commonly used Linux commands for debugging system, network, disk, and application issues.

---

## 🟢 1. System Health & Performance
Used when the server is slow, hanging, or overloaded.

- `top` → live CPU, memory, process usage
- `htop` → improved interactive version of top
- `uptime` → system load average + running time
- `free -m` → RAM and swap usage
- `vmstat 1` → CPU, memory, I/O stats in real time
- `iostat -xz 1` → disk I/O bottleneck analysis

---

## 📊 2. CPU / Memory / Process Troubleshooting
Used when applications are slow, stuck, or crashing.

- `ps aux | grep <process>` → find running process
- `pgrep <name>` → get process ID quickly
- `pidstat 1` → per-process CPU/memory usage
- `kill -9 <PID>` → force kill process
- `nice / renice` → adjust process priority

---

## 💾 3. Disk & Storage Issues
Used when disk is full or system is slow.

- `df -h` → disk space usage
- `du -sh *` → folder-wise size analysis
- `lsblk` → list disks and partitions
- `find / -size +500M` → find large files
- `iostat` → disk performance monitoring

---

## 🌐 4. Network Troubleshooting (VERY IMPORTANT)
Used in cloud, API, and connectivity issues.

- `ping <host>` → check connectivity
- `curl -I <url>` → check HTTP/API response
- `wget <url>` → test/download access
- `netstat -tulnp` → open ports (legacy)
- `ss -tulnp` → modern replacement for netstat
- `traceroute <host>` → network path tracing
- `dig <domain>` → DNS lookup
- `nslookup <domain>` → DNS resolution check

---

## 📄 5. Logs (MOST IMPORTANT IN REAL JOBS)
Used when something breaks — logs explain everything.

- `tail -f /var/log/syslog` → live system logs
- `tail -f /var/log/messages` → system logs
- `journalctl -u <service>` → systemd service logs
- `grep "error" file.log` → filter errors
- `less file.log` → scroll logs easily
- `zcat file.log.gz` → read compressed logs

---

## ⚙️ 6. Services & System Control
Used when services are down or failing.

- `systemctl status <service>` → check service status
- `systemctl start/stop/restart <service>` → manage service
- `systemctl enable <service>` → enable auto-start
- `service <name> status` → legacy systems

---

## 🔐 7. Permissions & Access Issues
Used for deployment and access-related failures.

- `ls -l` → check permissions
- `chmod 755 file` → change permissions
- `chown user:group file` → change ownership
- `id` → user identity details
- `whoami` → current user

---

## 📦 8. Package & Dependency Issues
Used when installation or updates fail.

- `apt update && apt install <pkg>` → Ubuntu/Debian
- `yum install <pkg>` → RHEL/CentOS
- `dpkg -l` → list installed packages
- `rpm -qa` → RPM package list

---

## 🔥 9. Quick Debugging Power Commands
Used for fast troubleshooting and investigation.

- `dmesg | tail` → kernel/hardware errors
- `env` → environment variables
- `export VAR=value` → set environment variable
- `watch -n 1 <command>` → repeat command every second
- `history | grep <cmd>` → search command history

---

## 🚀 10. Real-World DevOps Debug Flow
Typical production troubleshooting sequence:

```bash
top
df -h
free -m
systemctl status nginx
journalctl -u nginx -f
ss -tulnp
curl -I localhost
