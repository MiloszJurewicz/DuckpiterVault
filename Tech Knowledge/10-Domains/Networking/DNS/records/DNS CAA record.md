# DNS CAA record

A **CAA record** (Certification Authority Authorization) specifies which **Certificate Authorities (CAs)** are allowed to issue TLS/SSL certificates for a domain (e.g., `example.com → letsencrypt.org`). It helps prevent unauthorized certificate issuance. Each CAA record can include a **tag** (issue, issuewild, iodef) that controls issuance for the base domain, wildcards, or specifies a reporting URL for violations.

---

#flashcards/networking/dns
What security issue do CAA records prevent?::Unauthorized TLS/SSL certificate issuance
What are the three CAA record tags?::issue, issuewild, iodef
Can a CAA record specify which CAs are allowed to issue wildcard certificates?::Yes, using the issuewild tag
