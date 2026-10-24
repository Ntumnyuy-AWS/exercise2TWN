# Day 6: Networking Fundamentals

## Learning Objectives

Understand the basic networking concepts used in Linux administration,
DevOps, cloud infrastructure, and application deployment.

Topics covered:

- Local Area Network (LAN)
- Subnets and CIDR notation
- Network Address Translation (NAT)
- Firewalls
- Network ports
- Domain Name System (DNS)

---

## 1. Local Area Network (LAN)

A Local Area Network connects devices within a limited area, such as
a home, office, laboratory, or data centre.

### Example

Devices on a home network may include:

- A laptop connected through Wi-Fi
- A desktop connected through Ethernet
- A printer
- A development server

Devices on the same LAN can communicate when their IP configuration,
routing, and security rules allow it.

### DevOps relevance

A LAN provides connectivity between development machines, virtual
machines, servers, and other networked devices.

---

## 2. Subnets and CIDR

A subnet divides an IP address range into smaller logical networks.

### Example

`192.168.1.0/24`

The `/24` is CIDR notation. It means that 24 bits identify the network
portion of the IPv4 address.

A conventional IPv4 `/24` subnet contains 256 addresses, typically
254 usable host addresses.

Example addresses:

| Device | Example IP address |
|---|---|
| Router | `192.168.1.1` |
| Laptop | `192.168.1.10` |
| Desktop | `192.168.1.20` |
| Development server | `192.168.1.30` |

### DevOps relevance

Subnets help organize networks and determine how traffic is routed.
In AWS, a Virtual Private Cloud (VPC) can be divided into multiple
subnets to organize workloads and control connectivity.

---

## 3. Network Address Translation (NAT)

NAT translates IP address information as traffic passes through a
network device.

A common use is allowing several devices with private IPv4 addresses
to share a public IPv4 address when accessing the internet.

### Example

A laptop might have a private address such as:

`192.168.1.10`

A home router may translate outbound connections so that multiple
devices can share the router's public address.

Port Address Translation (PAT/NAPT) can also translate source port
numbers to distinguish simultaneous connections.

### DevOps relevance

NAT is commonly used in private networks to provide outbound internet
connectivity without assigning every workload a public IPv4 address.

NAT is not the same as a firewall: NAT translates address information,
while a firewall applies traffic-control rules.

---

## 4. Firewalls

A firewall allows or blocks network traffic according to configured
security rules.

Rules may consider:

- Source IP address
- Destination IP address
- Network protocol
- Destination port
- Connection state, depending on the firewall

### Example

| Port | Common purpose |
|---|---|
| TCP 22 | SSH administration |
| TCP 80 | HTTP |
| TCP 443 | HTTPS |
| TCP 3000 | Common development server port |

A firewall rule permitting traffic does not guarantee a successful
connection. The destination must also be reachable, and the intended
application must be listening.

### Linux example

Ubuntu's Uncomplicated Firewall (UFW) can be inspected with:

```bash
sudo ufw status
```

Do not enable or change firewall rules without understanding how they
might affect SSH access and other services.

### DevOps relevance

Firewalls help restrict access to servers and applications. In AWS,
security groups and network ACLs provide different layers of network
traffic control.

---

## 5. Network Ports

A port identifies a network service endpoint on a host. IP addresses
identify network destinations, while TCP or UDP port numbers help
identify the service receiving the traffic.

TCP and UDP port numbers range from 0 to 65535.

Common examples:

| Port | Typical use |
|---|---|
| 22/TCP | SSH |
| 53/TCP and UDP | DNS |
| 80/TCP | HTTP |
| 443/TCP | HTTPS |
| 3000/TCP | Common Node.js development port |
| 5432/TCP | PostgreSQL |
| 27017/TCP | MongoDB |

These are common defaults, not mandatory settings.

### Inspect listening TCP ports on Linux

```bash
ss -lnt
```

To include process details where permissions allow:

```bash
sudo ss -lntp
```

### Important distinction

- `127.0.0.1:3000` listens on the loopback interface.
- `0.0.0.0:3000` listens on all IPv4 interfaces in that network
  namespace.

Network routing, firewall rules, and VirtualBox port forwarding may
also affect whether another machine can reach an application.

---

## 6. Domain Name System (DNS)

DNS resolves domain names to records containing information such as
IP addresses.

For example, a DNS A record can provide an IPv4 address, while an
AAAA record can provide an IPv6 address.

### Example

A user enters:

`app.example.com`

A DNS resolver looks up the relevant record and can return an IP
address for the client to connect to.

DNS resolution does not normally specify the application port.
For example, a typical HTTPS connection uses TCP port 443 unless
another port or transport arrangement is specified.

### Linux example

```bash
getent hosts example.com
```

This asks the system's name service configuration to resolve the name.

### DevOps relevance

DNS allows users and services to use domain names instead of
remembering IP addresses. Cloud applications commonly use DNS to
direct clients to websites, load balancers, and other services.

---

## 7. How the Concepts Work Together

When a user accesses a deployed application:

1. DNS resolves the domain name to an address.
2. The client sends traffic toward the destination.
3. Routing determines how the traffic reaches its network.
4. NAT may translate address information along the path.
5. Firewalls evaluate whether traffic is permitted.
6. The destination port identifies the relevant network service.
7. The application processes the request if it is reachable and ready.

These components perform different jobs. DNS resolves names, routing
chooses paths, NAT translates addresses, firewalls enforce rules, and
ports identify service endpoints.

---

## 8. Practical Commands to Remember

| Command | Purpose |
|---|---|
| `ip addr` | Display network interfaces and IP addresses |
| `ip route` | Display the IP routing table |
| `getent hosts example.com` | Resolve a hostname using system name services |
| `ss -lnt` | Display listening TCP sockets |
| `ss -lun` | Display listening UDP sockets |
| `ping example.com` | Test reachability using ICMP, if permitted |
| `sudo ufw status` | Inspect UFW firewall status |

A failed ping does not necessarily mean a host is unreachable. ICMP
traffic may be blocked while other protocols remain available.

---

## Key Takeaways

- A LAN connects devices within a local network.
- A subnet divides an IP address range into logical networks.
- NAT translates address information as traffic passes through a device.
- A firewall controls traffic according to security rules.
- Ports identify service endpoints on a host.
- DNS resolves domain names to records such as IP addresses.

Understanding these concepts is foundational for Linux administration,
troubleshooting application connectivity, and designing cloud networks.
