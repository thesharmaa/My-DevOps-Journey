# TCP/IP Model (Transmission Control Protocol / Internet Protocol)

The **TCP/IP Model** is the networking model used on the internet.  
It explains how data moves between devices across a network.

Unlike the OSI model (7 layers), the **TCP/IP model has 4 layers**.

---

## 1. Application Layer
The **Application Layer** allows applications to communicate over the network.  
It combines the **Application, Presentation, and Session layers** of the OSI model.

**Functions**
- User interaction with network services
- Data formatting
- Encryption
- Session management

**Protocols**
- HTTP / HTTPS – Web browsing
- FTP – File transfer
- SMTP – Email
- DNS – Domain name resolution
- SSH – Secure remote login

---

## 2. Transport Layer
The **Transport Layer** ensures reliable communication between devices.

**Functions**
- End-to-end communication
- Segmentation of data
- Port numbers
- Flow control
- Error detection

**Protocols**
- TCP – Reliable, connection-oriented communication
- UDP – Faster, connectionless communication

**Examples**
- Web traffic uses TCP
- Video streaming and gaming often use UDP

---

## 3. Internet Layer
The **Internet Layer** is responsible for logical addressing and routing packets between networks.

**Functions**
- Assigns IP addresses
- Determines the best path for data
- Packet routing across networks

**Protocols**
- IP (Internet Protocol)
- ICMP (Internet Control Message Protocol)
- ARP (Address Resolution Protocol)

**Devices**
- Routers

---

## 4. Network Access Layer
The **Network Access Layer** handles communication within the local network and physical transmission of data.

It combines the **Data Link and Physical layers** of the OSI model.

**Functions**
- Frame creation
- MAC addressing
- Physical data transmission

**Examples**
- Ethernet
- Wi-Fi
- Fiber optics

**Devices**
- Switches
- Network Interface Cards (NIC)

---


## OSI vs TCP/IP Mapping

| OSI Model | TCP/IP Model |
|-----------|-------------|
| Application | Application |
| Presentation | Application |
| Session | Application |
| Transport | Transport |
| Network | Internet |
| Data Link | Network Access |
| Physical | Network Access |

---

## Key Point

The **TCP/IP model is the practical model used in real-world networking and the internet**, while the **OSI model is mainly used for understanding networking concepts**.
