# What is an IP Address?

An IP is pretty much an uuid for devices, needed for communication. For typical home and office setups, there are two primary types:

- **Private IP (LAN):** Unique to each device _inside_ your local network (assigned by your router, usually `192.168.x.x` or `10.x.x.x`). Devices on the outside internet cannot route to or see this address directly.
    
- **Public IP (WAN):** The single, globally routable address assigned to your modem/router by your ISP. To the outside world, all devices on your local network share this public IP (handled via NAT — Network Address Translation).
    
### Quick Analogy to Remember It

- **Public IP:** The street address of an apartment building (the mail carrier only needs this to reach the building).
    
- **Private IP:** The individual apartment number inside (the lobby/router uses this to deliver the mail to the exact tenant).
# What is a DNS?
is what python is to machine code, a translation layer that makes ips readable, how 8.8.8.8 is google.com
user hits google -> DNS knows google = 8.8.8.8, hits it, and serves the result to the user

---

## Definitions
#### NAT
**NAT (Network Address Translation)** is a networking technique where a router or gateway modifies the IP address information in packet headers while they are in transit.

Its primary job is mapping one IP address realm into another so traffic can flow between networks that don't know how to reach each other directly.

### Is NAT Used Only for Public IPs?

**No.** While connecting private home networks to the public internet is the most famous use case, NAT is not exclusive to public IPs. It operates wherever two distinct network address spaces need to communicate.

Common non-public / internal uses include:

- **Overlapping Private Networks:** If Company A (`10.0.0.0/16`) merges with or connects via VPN to Company B (also using `10.0.0.0/16`), packets cannot route normally due to identical IP spaces. Network engineers place NAT between them to translate one side to a dummy subnet (e.g., `172.16.0.0/16`).
    
- **Container & Virtual Machine Networks:** Docker, Kubernetes, and virtualization hypervisors (KVM/QEMU, VirtualBox) create internal software bridges (like `172.17.0.0/16`). When a container talks to another subnet or the host OS, the host performs NAT (specifically iptables/nftables masquerading) completely within private internal ranges.
    
- **Carrier-Grade NAT (CGNAT):** ISPs often route customer traffic through an intermediate shared private block (`100.64.0.0/10`) before it ever hits a true public IPv4 address.
