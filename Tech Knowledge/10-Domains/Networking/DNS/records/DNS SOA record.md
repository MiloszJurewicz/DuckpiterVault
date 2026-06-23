# DNS SOA record

An **SOA record** (Start of Authority) is the **mandatory** record at the top of every DNS zone. It contains administrative metadata: the primary name server, the zone administrator's email, a **serial number** (incremented on each zone update to trigger zone transfers), and timing values — **refresh**, **retry**, **expire**, and **minimum TTL** — that control how secondary servers and resolvers cache the zone.

---

#flashcards/networking/dns
What field in an SOA record must be incremented on each zone update?::Serial number
What are the four timing values in an SOA record?::Refresh, retry, expire, and minimum TTL
Is an SOA record mandatory for a DNS zone?::Yes, every zone must have exactly one SOA record at its apex
