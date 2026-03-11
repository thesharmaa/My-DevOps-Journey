## Subnet

### What is a Subnet

A **Subnet (Subnetwork)** is a smaller network created by dividing a larger network.  
Subnetting helps organize networks, improve security, and manage traffic efficiently.

Example:

Network: `192.168.1.0/24`

Devices in this subnet:

192.168.1.1  
192.168.1.2  
192.168.1.3  
...  
192.168.1.254

All these devices belong to the **same subnet** where 192.168.1 define the network portion, and the last octet (.1 to .254) identifies individual devices within that network.

---
### How Subnet is Created

Subnets are created using a **Subnet Mask**.

Example

IP Address: `192.168.1.10`  
Subnet Mask: `255.255.255.0`

Here:

Network Portion → `192.168.1`  
Host Portion → `10`

So:

Network = `192.168.1.0`  
Devices = `.1` to `.254`

We use 255 in a subnet mask because it represents 8 binary ones (11111111), which tells the computer that all bits in this octet belong to the network portion.

---

### Types of Subnets

**Public Subnet**

A subnet that has direct access to the internet.

Used for:
- Load balancers
- Web servers

---

**Private Subnet**

A subnet that does not have direct internet access.

Used for:
- Application servers
- Databases

---

### Uses of Subnet

- Organizes large networks
- Improves security
- Reduces network congestion
- Separates application layers
- Required in cloud networking

---

## CIDR (Classless Inter-Domain Routing)

CIDR is a method used to represent IP address ranges using **prefix notation**.  
The number after the slash (`/`) indicates how many bits belong to the **network portion** of the IP address.

**Example**

`192.168.1.0/24`

**Meaning**

- IPv4 addresses have **32 bits**
- `/24` means **24 bits are used for the network**
- Remaining **8 bits are used for hosts**

**Host Calculation**

- Total addresses → `2^8 = 256`
- Usable hosts → `254`

**Address Range**

- Network Address → `192.168.1.0`
- Usable Hosts → `192.168.1.1 – 192.168.1.254`
- Broadcast Address → `192.168.1.255`

**Uses**

- Efficient IP address allocation
- Network segmentation
- Used in cloud networking
- Defines VPC and subnet ranges
