# DNS PTR record

A **PTR record** (Pointer record) performs **reverse DNS lookup** — it maps an IP address back to a domain name (e.g., `34.216.184.93.in-addr.arpa → example.com`). It is the inverse of an A/AAAA record. PTR records are commonly used for email spam validation (checking that a sending server's IP resolves to its claimed domain) and network diagnostics.

---

#flashcards/networking/dns
What does a PTR record do that A/AAAA records do not?::Maps an IP address back to a domain name (reverse DNS lookup)
What special domain is used for IPv4 reverse DNS lookups?::in-addr.arpa
What common use case relies on PTR records for validation?::Email spam prevention (checking sending server's IP resolves to its claimed domain)
