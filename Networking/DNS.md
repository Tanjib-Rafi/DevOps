# How DNS Root Servers Work

## 1. Role of DNS Root Servers

- DNS uses a **hierarchical system**:

- Root → TLD → Authoritative DNS → IP address

- Root servers sit at the **top of this hierarchy** and know how to reach **TLD (Top-Level Domain) servers** such as `.com`, `.org`, `.net`, `.bd`, etc.
- They **don’t know the IP for every domain**, only which servers handle each TLD.

---

## 2. How a DNS Query Reaches the Root

Example: Resolving `www.example.com`

1. **Client** asks its **recursive resolver** (ISP DNS or local resolver):
2. The **resolver** checks its cache. If not found:
- It asks a **root server**: “Which server handles the `.com` TLD?”
3. The root server responds with the **IP addresses of `.com` TLD servers**.
4. The resolver then queries a **`.com` TLD server**: “Which server is authoritative for `example.com`?”
5. The TLD server responds with the **authoritative DNS server** for `example.com`.
6. Finally, the resolver queries the authoritative server to get the **IP address of `www.example.com`**.

---

## 3. Facts About Root Servers

- There are **13 logical root server addresses**, named `A` through `M`.  
- Each “server” is actually a **cluster of servers** distributed worldwide using **Anycast** to improve speed and reliability.  
- Operated by different organizations, including ICANN, Verisign, RIPE NCC, and others.  
- Root servers only handle **referrals** to TLD servers, not individual domain queries.

---

## 4. Why Root Servers Are Critical

- Without root servers, DNS resolution would fail, and users could not reach websites using domain names.  
- They **do not store every IP** — they act as a **directory of directories**.

---

