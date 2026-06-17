ARP (Address Resolution Protocol) is a **[[Layer]] 2 (Data Link layer)** protocol used to map an **IP address ([[Layer 3]])** to a **MAC address (Layer 2)** on a local network.
### How it works:
1. Your device wants to send data to an IP (e.g. `192.168.1.20`).
2. It checks its **ARP cache** for a known MAC address.
3. If missing, it sends an **ARP request as a Layer 2 broadcast frame**:
    - Destination MAC: `FF:FF:FF:FF:FF:FF`
    - Meaning: “Who has this IP?”
4. The **switch (Layer 2 device)** floods this broadcast to all ports in the same LAN/VLAN.
5. The device with that IP replies with its MAC address (unicast).
6. Your device stores the mapping in the ARP table and sends frames directly to that MAC.
### Key points:
- ARP works at **Layer 2 (not Layer 3 routing)**.
- It relies on **switch-level broadcasting inside the local network**.
- It does **not cross routers**.
- It’s only used to resolve addresses **within the same LAN/broadcast domain**.