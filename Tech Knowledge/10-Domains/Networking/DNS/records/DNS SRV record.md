# DNS SRV record

An **SRV record** (Service record) defines the **hostname and port** for specific services (e.g., `_sip._tcp.example.com → sipserver.example.com:5060`). It includes **priority** and **weight** for load balancing and failover. SRV records are used by protocols like SIP, LDAP, XMPP, and Active Directory to discover service endpoints dynamically.

---

#flashcards/networking/dns
What two extra fields does an SRV record include beyond a hostname?::Port and protocol (plus priority and weight for load balancing)
Name two protocols that use SRV records for service discovery.::SIP, LDAP (also XMPP, Active Directory)
