# DNS TXT record

A **TXT record** (Text record) stores arbitrary **text data** in DNS. While originally designed for human-readable notes, it is now critical infrastructure for **domain verification** (proving ownership to services like Google Workspace), **email security** (SPF — authorizing which servers can send mail from the domain; DKIM — cryptographic email signing; DMARC — policy for handling unauthenticated mail), and other machine-readable protocols.

---

#flashcards/networking/dns
Name three email security protocols that use TXT records.::SPF, DKIM, and DMARC
What does SPF do?::Authorizes which mail servers are allowed to send email on behalf of a domain
What is a common non-email use of TXT records?::Domain ownership verification (e.g., for Google Workspace or other services)
