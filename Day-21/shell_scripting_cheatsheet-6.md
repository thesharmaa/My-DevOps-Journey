# Useful Bash Patterns and One-Liners

These are practical one-liners commonly used in Linux, DevOps, and SRE work.

---

## 1. Find and Delete Files Older Than N Days

Delete `.log` files older than 30 days.

```bash
find /var/log -name "*.log" -type f -mtime +30 -delete
```

### Explanation

- `find` → search files
- `-name "*.log"` → only log files
- `-type f` → regular files
- `-mtime +30` → older than 30 days
- `-delete` → remove files

### Safe Version (Preview First)

```bash
find /var/log -name "*.log" -type f -mtime +30
```

---

## 2. Count Lines in All `.log` Files

```bash
wc -l *.log
```

### Example Output

```text
100 app.log
250 server.log
350 total
```

---

## 3. Replace a String Across Multiple Files

Replace `localhost` with `prod-db`.

```bash
sed -i 's/localhost/prod-db/g' *.conf
```

### Verify Changes

```bash
grep -r "prod-db" .
```

---

## 4. Check If a Service Is Running

### Using systemctl

```bash
systemctl is-active nginx
```

Output:

```text
active
```

### Script-Friendly

```bash
systemctl is-active --quiet nginx && echo "Running" || echo "Stopped"
```

---

## 5. Monitor Disk Usage with Alerts

Alert when usage exceeds 80%.

```bash
df -h / | awk 'NR==2 {gsub("%","",$5); if($5>80) print "Disk Alert: "$5"% used"}'
```

### Example Output

```text
Disk Alert: 85% used
```

---

## 6. Parse CSV From Command Line

### Sample CSV

```text
name,role
aman,devops
john,developer
```

### Extract First Column

```bash
cut -d',' -f1 users.csv
```

Output:

```text
name
aman
john
```

---

## 7. Parse JSON From Command Line

Using `jq`.

### Sample JSON

```json
{
  "name": "Aman",
  "role": "DevOps"
}
```

### Extract Value

```bash
jq -r '.name' user.json
```

Output:

```text
Aman
```

### Extract Multiple Fields

```bash
jq -r '.name, .role' user.json
```

---

## 8. Tail a Log and Filter Errors in Real Time

```bash
tail -f app.log | grep -i error
```

Shows only new log lines containing "error".

---

## 9. Find Top 10 Largest Files

```bash
find . -type f -exec du -h {} + | sort -hr | head -10
```

Useful when disk space is running low.

---

## 10. Count Occurrences of IP Addresses in Logs

```bash
awk '{print $1}' access.log | sort | uniq -c | sort -nr
```

### Example Output

```text
120 192.168.1.10
95 192.168.1.20
50 192.168.1.30
```

Useful for traffic analysis.

---

## 11. Find Failed Login Attempts

```bash
grep "Failed password" /var/log/auth.log
```

Count them:

```bash
grep -c "Failed password" /var/log/auth.log
```

---

## 12. Kill a Process by Name

```bash
pkill nginx
```

Or:

```bash
ps -ef | grep nginx
kill -9 <PID>
```

---

## 13. Check Open Ports

```bash
ss -tulnp
```

Alternative:

```bash
netstat -tulnp
```

---

## 14. Monitor CPU and Memory Usage

Top 5 memory-consuming processes:

```bash
ps aux --sort=-%mem | head -5
```

Top 5 CPU-consuming processes:

```bash
ps aux --sort=-%cpu | head -5
```

---

## 15. Find Empty Files

```bash
find . -type f -empty
```

---

# DevOps Interview Favorites

### Check Service Status

```bash
systemctl is-active nginx
```

### Monitor Logs

```bash
tail -f app.log
```

### Monitor Only Errors

```bash
tail -f app.log | grep -i error
```

### Check Disk Usage

```bash
df -h
```

### Find Large Files

```bash
find . -type f -exec du -h {} + | sort -hr | head
```

### Count Errors in Logs

```bash
grep -c "ERROR" app.log
```

### Replace Text in Multiple Files

```bash
sed -i 's/old/new/g' *.conf
```

### Parse JSON

```bash
jq -r '.name' file.json
```

### Top IP Addresses

```bash
awk '{print $1}' access.log | sort | uniq -c | sort -nr
```

### Delete Old Files

```bash
find /path -mtime +30 -delete
```
