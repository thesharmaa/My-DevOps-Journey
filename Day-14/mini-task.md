# Mini Task: Port Probe & Interpret

## Identify one listening port from ss -tulpn (e.g., SSH on 22 or a local web app).

```bash
tcp LISTEN 0 4096 0.0.0.0:22
```

## From the same machine, test it:

```bash
nc -zv localhost 22
```

## Example output:

```bash
Connection to localhost 22 port [tcp/ssh] succeeded!
```

```bash
Connection to localhost (127.0.0.1) 22 port [tcp/ssh] succeeded!
```

## Meaning

- `localhost (127.0.0.1)` → Your own machine
- `22` → SSH port
- `[tcp/ssh]` → TCP service running for SSH
- `succeeded!` → Connection to port 22 was successful

## This confirms

- SSH service is running
- Port 22 is open
- The service is reachable locally on your machine

## Write one line: is it reachable? If not, what’s the next check? (e.g., service status, firewall).

SSH on port 22 is reachable. If not reachable, next checks would be service status (`systemctl status ssh`) and firewall rules.

---

# Reflection

## Which command gives you the fastest signal when something is broken?

`ping` gives the fastest signal to quickly check basic network connectivity, latency, and packet loss.

---

## What layer (OSI/TCP-IP) would you inspect next if DNS fails? If HTTP 500 shows up?

### If DNS fails

- Application Layer (DNS)
- Then Transport Layer (UDP/TCP port 53)
- Then Internet Layer/IP connectivity

### If HTTP 500 shows up

- Application Layer
- Check web server logs, backend application, database connectivity, and server status

---

# Two follow-up checks you’d run in a real incident

## Check service status and logs

```bash
systemctl status <service>
journalctl -xe
```

## Check connectivity and open ports

```bash
ping
ss -tulpn
curl -I
traceroute
```
