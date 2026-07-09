# Linux Networking Interview Notes

## `ip addr`
Used to display network interfaces and their IP addresses. It helps verify whether the server has an IP address, whether the interface is UP, and whether DHCP has assigned an address. Think of it as answering: **"Who am I on the network?"**

## `ip route`
Displays the routing table and shows how the server sends traffic to other networks. It helps verify the default gateway, outgoing interface, and routing configuration. Think of it as answering: **"Where should I send packets?"**

## `ping`
Checks whether a remote host is reachable and measures network latency (round-trip time). It's commonly used to verify connectivity and basic DNS resolution. If `ping 8.8.8.8` works but `ping google.com` fails, the issue is likely DNS.

## `ss -tulnp`
Shows listening TCP and UDP ports along with the services using them. It helps verify whether applications like SSH, Nginx, or databases are actually listening on the expected ports. Think of it as answering: **"What services are accepting network connections?"**

## `curl`
A command-line tool for testing HTTP/HTTPS endpoints and APIs. It is commonly used to verify whether a web server or API is reachable, check HTTP responses, and troubleshoot application connectivity.

## `nslookup`
A DNS lookup tool that resolves domain names into IP addresses. It helps verify whether DNS is working, which DNS server responded, and what IP address is returned for a domain.

## `dig`
An advanced DNS troubleshooting tool that provides detailed information such as query status, TTL, DNS records, query time, and the responding DNS server. It is preferred over `nslookup` for in-depth DNS debugging.

## `tcpdump`
A packet capture tool that displays live network traffic entering and leaving a network interface. It is used to verify whether packets are reaching the server and troubleshoot issues related to DNS, SSH, HTTP, HTTPS, and other network protocols.

## `traceroute`
Shows the path (hops) that packets take from the source to the destination while displaying the latency at each hop. It helps identify where network delays or packet drops occur during the journey.

## `iptables -L`
Displays the Linux firewall rules. It helps verify whether incoming, outgoing, or forwarded traffic is being allowed or blocked. The three main chains are **INPUT** (incoming traffic), **OUTPUT** (outgoing traffic), and **FORWARD** (traffic passing through the server).
