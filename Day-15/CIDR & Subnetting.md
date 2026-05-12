# Task 3: CIDR & Subnetting

## What does /24 mean in 192.168.1.0/24?

`/24` means the first 24 bits are used for the network part and the remaining bits are used for hosts/devices.

Subnet mask for `/24`:

```bash
255.255.255.0
```

Laymen example:

Like the first part being the street name and the last part being individual house numbers.

---

# How many usable hosts in a /24? A /16? A /28?

| CIDR | Total IPs | Usable Hosts |
|---|---|---|
| /24 | 256 | 254 |
| /16 | 65,536 | 65,534 |
| /28 | 16 | 14 |

Why usable hosts are less by 2:
- One IP is reserved for Network Address
- One IP is reserved for Broadcast Address

---

# Explain in your own words: why do we subnet?

Subnetting helps divide a large network into smaller networks for:
- Better organization
- Improved security
- Reduced network traffic
- Easier management
- Efficient IP address usage

Laymen example:

Like dividing a large apartment building into separate floors or rooms for easier management.

---

# Quick exercise — fill in:

| CIDR | Subnet Mask | Total IPs | Usable Hosts |
|---|---|---|---|
| /24 | 255.255.255.0 | 256 | 254 |
| /16 | 255.255.0.0 | 65,536 | 65,534 |
| /28 | 255.255.255.240 | 16 | 14 |
