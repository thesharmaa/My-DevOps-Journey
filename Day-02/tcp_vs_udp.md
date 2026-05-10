# TCP vs UDP

TCP and UDP are communication protocols that operate at the **Transport Layer** of the networking model.  
They are used to send data between devices over a network.

---

## TCP (Transmission Control Protocol)

TCP is a **connection-oriented protocol** that ensures reliable data transmission.

### Features
- Establishes a connection before sending data
- Guarantees data delivery
- Maintains correct order of packets
- Performs error checking and retransmission

### How TCP Works
1. Connection established using **3-way handshake** as SYN, SYN-ACK and ACK
2. Data is sent in **segments** with port and sequence number 
3. Receiver acknowledges received data

### Examples of TCP Usage
- Web browsing (HTTP / HTTPS)
- Email (SMTP)
- File transfer (FTP)
- SSH connections

---

## UDP (User Datagram Protocol)

UDP is a **connectionless protocol** designed for fast data transmission.

### Features
- No connection establishment
- Faster than TCP
- No guarantee of delivery
- No packet ordering
- Minimal error checking

### Examples of UDP Usage
- Video streaming
- Online gaming
- Voice calls (VoIP)
- DNS queries

---

## Key Point

Use **TCP when reliability is important**.  
Use **UDP when speed is more important than reliability**.
