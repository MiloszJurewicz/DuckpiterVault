DHCP (Dynamic Host Configuration Protocol) is a network protocol used to automatically assign IP configuration parameters to devices on a network.

When a device connects to a network, it typically needs:
- IP address
- Subnet mask
- Default gateway
- DNS server(s)

DHCP handles this via a client–server model:
1. **DHCP Discover**: The client broadcasts a request looking for a DHCP server.
2. **DHCP Offer**: A server responds with an available IP configuration.
3. **DHCP Request**: The client requests to use the offered configuration.
4. **DHCP Acknowledge**: The server confirms and assigns the lease.

Key properties:
- **Lease-based allocation**: IPs are assigned for a limited time (lease time), not permanently.
- **Dynamic reuse**: IPs are returned to a pool when leases expire.
- **Centralized management**: avoids manual IP configuration on each device.
- Typically runs over **UDP** (ports 67 for server, 68 for client).

If you want, I can also explain how DHCP differs from static IP configuration or what happens during lease renewal.