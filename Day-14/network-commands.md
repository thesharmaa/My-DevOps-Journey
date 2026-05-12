# Hands-on Checklist

## Identity: hostname -I (or ip addr show) — note your IP.

```bash
ubuntu@ip-172-31-47-21:~$ hostname -I
172.31.47.21
```

---

## 2, Reachability: ping — mention latency and packet loss.

```bash
ubuntu@ip-172-31-47-21:~$ ping google.com

PING google.com (142.251.179.113) 56(84) bytes of data.
64 bytes from pd-in-f113.1e100.net (142.251.179.113): icmp_seq=1 ttl=106 time=2.17 ms
64 bytes from pd-in-f113.1e100.net (142.251.179.113): icmp_seq=2 ttl=106 time=2.17 ms
64 bytes from pd-in-f113.1e100.net (142.251.179.113): icmp_seq=3 ttl=106 time=1.99 ms
```

Latency = The time taken for a packet to travel from your system to the destination and back. Lower latency = faster response.

Packet Loss = When some packets sent over the network never reach the destination or never return. Example: Sent 10 packets, received 10 → 0% packet loss Sent 10 packets, received 8 → 20% packet loss

Your output currently shows replies for every sequence icmp_seq=1 icmp_seq=2 icmp_seq=3 So there is no packet loss in the shown packets.

---

## Path: traceroute (or tracepath) — note any long hops/timeouts.

```bash
ubuntu@ip-172-31-47-21:~$ traceroute google.com

traceroute to google.com (192.178.155.113), 30 hops max, 60 byte packets
1 240.64.220.131 (240.64.220.131) 1.323 ms 240.64.220.128 (240.64.220.128) 1.125 ms 240.64.220.129 (240.64.220.129) 1.107 ms
2 99.82.14.76 (99.82.14.76) 1.456 ms 1.935 ms 99.82.14.178 (99.82.14.178) 1.426 ms
3 99.82.14.179 (99.82.14.179) 1.116 ms 99.82.14.79 (99.82.14.79) 1.102 ms 99.82.14.77 (99.82.14.77) 1.147 ms
4 192.178.105.219 (192.178.105.219) 1.994 ms 216.239.63.169 (216.239.63.169) 1.302 ms 216.239.40.107 (216.239.40.107) 1.239 ms
5 192.178.242.26 (192.178.242.26) 4.019 ms 192.178.248.40 (192.178.248.40) 1.249 ms 192.178.248.38 (192.178.248.38) 1.765 ms
6 142.251.49.155 (142.251.49.155) 1.751 ms 142.251.49.160 (142.251.49.160) 1.576 ms 216.239.47.127 (216.239.47.127) 1.704 ms
7 192.178.74.83 (192.178.74.83) 3.187 ms 172.253.50.55 (172.253.50.55) 2.258 ms 192.178.74.83 (192.178.74.83) 3.314 ms
8 142.251.228.193 (142.251.228.193) 8.664 ms 142.251.241.239 (142.251.241.239) 2.339 ms 72.14.237.35 (72.14.237.35) 16.862 ms
9 142.250.210.193 (142.250.210.193) 2.075 ms 142.251.229.155 (142.251.229.155) 3.151 ms 216.239.59.67 (216.239.59.67) 2.067 ms
10 * * *
11 * * *
12 * * *
13 * * *
14 * * *
15 * * *
16 * * *
17 * * *
18 * * *
19 yuiadrs-in-f113.1e100.net (192.178.155.113) 2.122 ms 2.137 ms *
```

traceroute shows the path packets take to reach a destination hop-by-hop. Each numbered line = one router/hop. ms = latency to that hop.

= router did not reply (usually firewall/rate limit, not always an issue). One packet can work, but sending multiple probe packets helps because networks are not always stable. If only one packet was sent, you might miss these network fluctuations. One packet delayed and one lost yuiadrs-in-f113.1e100.net - Google server reached

---

## Ports: ss -tulpn (or netstat -tulpn) — list one listening service and its port.

```bash
ubuntu@ip-172-31-47-21:~$ ss -tulpn

Netid State Recv-Q Send-Q Local Address:Port Peer Address:Port Process
udp UNCONN 0 0 127.0.0.54:53 0.0.0.0:*
udp UNCONN 0 0 127.0.0.53%lo:53 0.0.0.0:*
udp UNCONN 0 0 172.31.47.21%ens5:68 0.0.0.0:*
udp UNCONN 0 0 127.0.0.1:323 0.0.0.0:*
udp UNCONN 0 0 [::1]:323 [::]:*
tcp LISTEN 0 4096 0.0.0.0:22 0.0.0.0:*
tcp LISTEN 0 4096 127.0.0.54:53 0.0.0.0:*
tcp LISTEN 0 4096 127.0.0.53%lo:53 0.0.0.0:*
tcp LISTEN 0 4096 [::]:22 [::]:*
```

tcp LISTEN 0 4096 0.0.0.0:22 → SSH server listening on port 22 from all IPv4 addresses.

tcp LISTEN 0 4096 [::]:22 → SSH also listening on IPv6.

127.0.0.53:53 → Local DNS resolver running on port 53.

ss -tulpn shows listening TCP/UDP ports and the services using them.

---

## Name resolution: dig or nslookup — record the resolved IP.

```bash
ubuntu@ip-172-31-47-21:~$ dig google.com

; <<>> DiG 9.20.18-1ubuntu2-Ubuntu <<>> google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 33403
;; flags: qr rd ra; QUERY: 1, ANSWER: 6, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;google.com. IN A

;; ANSWER SECTION:
google.com. 256 IN A 172.253.139.139
google.com. 256 IN A 172.253.139.113
google.com. 256 IN A 172.253.139.102
google.com. 256 IN A 172.253.139.138
google.com. 256 IN A 172.253.139.101
google.com. 256 IN A 172.253.139.100

;; Query time: 1 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue May 12 15:12:41 UTC 2026
;; MSG SIZE rcvd: 135
```

Multiple IPs are returned for: Load balancing High availability Faster routing

status: NOERROR

→ DNS query was successful. TTL (Time To Live) in DNS tells how long a DNS response can be cached before asking the DNS server again.

Suppose your system asks DNS: What is the IP of google.com? DNS replies: google.com = 172.253.139.139 TTL = 256 seconds Now your computer stores (caches) this answer for 256 seconds. So if you open Google again within 256 seconds: Your system uses the saved IP It does NOT ask DNS server again This makes browsing faster. After 256 seconds: Cache expires Your system asks DNS again for a fresh IP Because sometimes websites change their IP addresses.

---

## HTTP check: curl -I <http/https-url> — note the HTTP status code.

```bash
ubuntu@ip-172-31-47-21:~$ curl -I google.com

HTTP/1.1 301 Moved Permanently
```
