# DNS NS record

An **NS record** (Name Server record) **delegates** a DNS zone to a specific authoritative name server (e.g., `example.com → ns1.dnsprovider.com`). It tells resolvers which server to query for that domain's records. Every zone must have at least one NS record, and NS records are typically configured at both the parent zone (for delegation) and the zone itself.

---

#flashcards/networking/dns
What does an NS record delegate?::A DNS zone to a specific authoritative name server
Where are NS records typically configured?::At both the parent zone (for delegation) and the zone itself
