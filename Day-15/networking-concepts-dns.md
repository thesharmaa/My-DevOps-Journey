# Task 1: DNS – How Names Become IPs

## Explain in 3–4 lines: what happens when you type google.com in a browser?

When you type `google.com` in a browser, your system first asks a DNS server for the IP address of Google.  
DNS works like a phonebook that converts names into IP addresses.  
After getting the IP, the browser connects to Google’s server using that IP address.  
Then Google sends back the webpage data and the browser displays the website.

---

# What are these record types?

## A Record
Maps a domain name to an IPv4 address.  
Example: `google.com → 172.253.139.139`

Laymen example: Like saving a person's home address in your phone contacts.

---

## AAAA Record
Maps a domain name to an IPv6 address.

Laymen example: Same as A record, but using a newer and bigger address format.

---

## CNAME Record
Points one domain name to another domain name.

Laymen example: Like a nickname redirecting to the real person's name.

Example:
`www.google.com → google.com`

---

## MX Record
Tells where emails for a domain should go.

Laymen example: Like identifying which post office handles your mail.

---

## NS Record
Tells which DNS servers are responsible for a domain.

Laymen example: Like knowing which office maintains the official phonebook records.

---

# Run: dig google.com — identify the A record and TTL from the output

Example:

```bash
google.com. 256 IN A 172.253.139.139
```

- `A record` → `172.253.139.139`
- `TTL` → `256 seconds`

TTL means how long the IP can stay cached before asking DNS again.
