# What is an IPv4 address?

An IPv4 address is a unique address used to identify a device on a network.  
It helps devices communicate with each other over the internet or local network.

Example:

```bash
192.168.1.10
```

Structure:

- IPv4 is made of 4 numbers separated by dots
- Each number ranges from 0–255
- Each part is called an octet

Example breakdown:

```bash
192 . 168 . 1 . 10
```

Laymen example:

Like a house address used to locate a specific home in a city.

---

# Difference between public and private IPs

## Public IP

A public IP is reachable over the internet and is assigned by an ISP.

Example:

```bash
8.8.8.8
```

Laymen example:

Like your home's full address visible to the outside world.

---

## Private IP

A private IP is used inside local/private networks and is not directly reachable from the internet.

Example:

```bash
192.168.1.10
```

Laymen example:

Like apartment room numbers used only inside a building.

---

# What are the private IP ranges?

```bash
10.x.x.x
172.16.x.x – 172.31.x.x
192.168.x.x
```

These ranges are reserved for private/internal networks.

---

# Run: ip addr show — identify which of your IPs are private

Example:

```bash
172.31.47.21
```

This is a private IP because it falls under:

```bash
172.16.x.x – 172.31.x.x
```
