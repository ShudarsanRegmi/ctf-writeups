# General Networking Notes Needed for CTF


### MDNS

mDNS, or Multicast DNS, is a protocol used to resolve hostnames to IP addresses within small networks that do not include a local name server. It is particularly useful in environments where devices need to discover each other and communicate without a central directory service.
Key Points about mDNS:

## Local Network Resolution:

mDNS operates on the local network segment. When a device needs to find another device on the same local network, it uses mDNS to resolve the hostname to an IP address.
Multicast Traffic:

Instead of sending a query to a specific DNS server, mDNS uses multicast traffic to broadcast its queries to all devices on the local network. This is usually done on the reserved multicast address 224.0.0.251 for IPv4 and ff02::fb for IPv6, both on port 5353.

When a device joins the network, it uses mDNS to announce its hostname. If no other device responds with a conflicting hostname, the device claims that hostname and uses it.
To resolve a hostname, a device sends an mDNS query to the multicast address. All devices on the local network receive this query, and if a device recognizes the hostname, it replies with its IP address.

## Comparison with Traditional DNS:

Traditional DNS relies on hierarchical and centralized servers for name resolution, making it suitable for large and distributed networks, including the internet.
mDNS, on the other hand, is decentralized and designed for small local networks without a central DNS server.


