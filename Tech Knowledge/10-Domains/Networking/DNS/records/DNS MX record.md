# DNS MX record

An **MX record** (Mail Exchange record) specifies the **mail server** responsible for accepting email on behalf of a domain (e.g., `example.com → mail.example.com`). Each MX record includes a **priority** value — lower numbers are tried first. MX records must point to a hostname (A/AAAA record), never to an IP address directly.

---

#flashcards/networking/dns
What extra field does an MX record include beyond a hostname?::Priority (lower numbers are tried first)
Can an MX record point directly to an IP address?::No, it must point to a hostname (A/AAAA record)
What type of server does an MX record specify?::Mail server
