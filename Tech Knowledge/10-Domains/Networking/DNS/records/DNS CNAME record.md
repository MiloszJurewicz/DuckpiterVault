# DNS CNAME record

A **CNAME record** (Canonical Name record) creates an **alias** from one domain name to another (e.g., `www.example.com → example.com`). All DNS lookups on the alias are redirected to the canonical domain. Important restrictions: a CNAME cannot coexist with other records at the same name, and you cannot use a CNAME at the zone apex (root domain).

---

#flashcards/networking/dns
Can a CNAME record be used at the zone apex (root domain)?::No, it cannot coexist with other records at the same name
What happens to DNS lookups on a CNAME alias?::They are redirected to the canonical domain
