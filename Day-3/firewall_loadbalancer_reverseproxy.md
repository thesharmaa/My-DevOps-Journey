## Firewall, Load Balancer, and Reverse Proxy

### Firewall
A firewall filters **incoming and outgoing network traffic** based on security rules.

**Types:**
- Network firewall
- Host firewall
- Application firewall

**Uses:**
- Provides network security
- Prevents unauthorized access

**Example Diagram:**
Internet
↓
Firewall
↓
Internal Network

---

### Load Balancer
A load balancer distributes **incoming traffic** across multiple servers to improve performance and availability.

**Types:**
- **Layer 4:** IP / Port based
- **Layer 7:** HTTP / URL based

**Uses:**
- High availability
- Scalability
- Prevents server overload

**Example Diagram:**
Users
↓
Load Balancer
↓
Server1 Server2 Server3

---

### Reverse Proxy
A reverse proxy is a server that sits between clients (users) and backend servers.
Clients never communicate directly with the backend servers.
The reverse proxy forwards requests to one or more backend servers and returns the response to the client.

**Examples:**
- Nginx
- HAProxy
- Apache

**Uses:**
- Security
- SSL/TLS termination
- Caching
- Load balancing

**Example Diagram:**
User → Reverse Proxy → Backend Server(s)
