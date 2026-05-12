# How subnet masks for /16, /24, /28 are calculated

Subnet mask is made of:
- `1s` for network bits
- `0s` for host bits

IPv4 has total `32 bits`.

---

# /24 Calculation

`/24` means:
- First 24 bits = network bits (`1s`)
- Remaining 8 bits = host bits (`0s`)

Binary:

```bash
11111111.11111111.11111111.00000000
```

Convert each 8-bit block to decimal:

```bash
11111111 = 255
00000000 = 0
```

Result:

```bash
255.255.255.0
```

---

# /16 Calculation

`/16` means:
- First 16 bits = network bits
- Remaining 16 bits = host bits

Binary:

```bash
11111111.11111111.00000000.00000000
```

Decimal:

```bash
255.255.0.0
```

---

# /28 Calculation

`/28` means:
- First 28 bits = network bits
- Remaining 4 bits = host bits

Binary:

```bash
11111111.11111111.11111111.11110000
```

Last octet conversion:

```bash
11110000
= 128 + 64 + 32 + 16
= 240
```

Result:

```bash
255.255.255.240
```

---

# Easy trick to remember

Common subnet masks:

| CIDR | Subnet Mask |
|---|---|
| /8 | 255.0.0.0 |
| /16 | 255.255.0.0 |
| /24 | 255.255.255.0 |
| /28 | 255.255.255.240 |
