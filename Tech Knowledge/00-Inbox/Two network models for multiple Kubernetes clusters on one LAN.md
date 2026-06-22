## A. Everything flat network model

This is the simplest and most common homelab approach.

### Structure

- All Proxmox VMs/nodes are connected to a single bridge (`vmbr0`)
- Everything is in one subnet (e.g. `192.168.1.0/24`)
- No VLAN separation
- All clusters coexist on the same Layer 2 network

### How clusters are exposed

- Each cluster exposes Traefik ingress via:
    - Node IP + NodePort, or
    - MetalLB LoadBalancer IP (still inside same LAN)
- DNS (own DNS server or ExternalDNS) maps names directly to those IPs

Example:

```
app.cluster1.home → 192.168.1.10app.cluster2.home → 192.168.1.11
```

### Key characteristics

- No network isolation between clusters
- All nodes can communicate freely unless restricted by firewall rules
- DNS is purely a mapping layer (name → IP)
- ExternalDNS only publishes records; it does not influence routing or topology

### What this model optimizes for

- Simplicity
- Low operational overhead
- Fast iteration
- Easy troubleshooting

### What it does NOT provide

- Security boundaries between clusters
- Traffic isolation
- Failure/domain separation

### Core takeaway

> In a flat network, Kubernetes clusters are separated logically, not physically. DNS points directly to stable ingress IPs, and the underlying LAN handles all connectivity.

---

## B. VLAN-based model

This introduces real network segmentation at Layer 2.

### Structure

- Each cluster is placed in its own VLAN
- Each VLAN has its own subnet:
    - VLAN 10 → 192.168.10.0/24
    - VLAN 20 → 192.168.20.0/24
    - VLAN 30 → 192.168.30.0/24
- Proxmox bridges carry VLAN tags to VMs
- Router or firewall performs inter-VLAN routing if enabled

### How clusters are exposed

- Each cluster exposes a stable ingress IP inside its VLAN:
    - Node IP + NodePort, or
    - MetalLB IP inside VLAN subnet
- DNS maps names to those VLAN-scoped IPs

Example:

```
app.cluster1.home → 192.168.10.50app.cluster2.home → 192.168.20.50
```

### Key characteristics

- True L2 network isolation between clusters
- Traffic between clusters is blocked by default unless routed
- Communication between VLANs requires a router/firewall (inter-VLAN routing)
- DNS remains unaware of VLANs and only maps names to IPs

### What this model optimizes for

- Isolation between clusters
- Security boundaries (VPC-like behavior)
- Controlled inter-cluster communication

### What it does NOT provide automatically

- Service-level routing logic
- Automatic “correct VLAN selection”
- Simplified configuration (more infrastructure required)

### Core takeaway

> VLANs create real network boundaries. DNS still only maps names to IPs, while routing and firewall rules determine whether traffic can cross between clusters.

---

As side not, I could also explore automatic provisioning of vLan using ansible or terraform +  openWRT 