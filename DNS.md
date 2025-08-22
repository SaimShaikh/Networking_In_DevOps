# Domain Name System (DNS)
- The Domain Name System (DNS) is a hierarchical, distributed naming system for the Internet
- In practice, DNS acts like the Internet’s phonebook: it maps easy-to-remember domain names (like www.youtube.com) to machine-readable IP addresses (like 93.184.216.34)
- Every Internet-connected device has a numeric IP address, but humans think in names. DNS automates the translation so users can type names and browsers still locate the right server. In other words, DNS lets you use human-friendly domain names instead of memorizing complex number strings

---

## Historical Background
- Originally, early networks used a single hosts file to map names to IPs. In the ARPANET era (1960s–70s), SRI International maintained a global “HOSTS.TXT” listing of every host’s name and address
- As the network grew, this centralized file became unmanageable. In 1983-84 Paul Mockapetris proposed the DNS architecture to replace the static hosts file
- The IETF released the first DNS specifications (RFC 882/883) in 1983, updated in RFC 973 (1986)
- In 1984 the first DNS server software (BIND, the Berkeley Internet Name Domain) was written, and by 1985 DNS was in production use
- DNS automated and decentralized name resolution: instead of a single file, DNS uses a hierarchy of name servers worldwide (Today most operating systems still include a local hosts file as a fallback, but it is rarely used except for custom overrides.)

---

# How does DNS work?
When you enter a website URL, DNS resolution happens “behind the scenes” to find the site’s server. Think of your browser’s DNS resolver as a librarian, root servers as the library’s index, and the domain’s name servers as the specific book. In this analogy, the resolver (librarian) checks first if it already “knows” the address (cache); otherwise it asks higher authorities. For example, the root server acts like a library index pointing to the right bookshelf (the Top-Level Domain servers), which in turn point to the specific book (the authoritative nameserver) that contains the exact address

## DNS Architecture
<img width="1981" height="1477" alt="image" src="https://github.com/user-attachments/assets/f5a8a985-85f0-4ed4-a886-3bd1a52e400b" />

1. Local query: The user’s computer (browser/OS) generates a DNS query for the domain (e.g. www.youtube.com)
   The system first checks its own cache (and then the ISP’s or configured resolver’s cache).

2. Recursive resolver: If uncached, the query goes to a recursive DNS resolver (often run by the ISP or a public DNS service). The resolver is like the librarian tasked with finding the address. If it doesn’t have the answer cached, it proceeds to query the global DNS hierarchy

3. Root name server: The resolver first asks a root name server. There are 13 root server addresses worldwide. A root server doesn’t know the domain’s IP, but it knows where to find the TLD server. It responds with a referral to the appropriate Top-Level Domain server for “.com,” “.org,” etc

4. TLD name server: Next, the resolver queries the TLD server (for example, the .com nameserver). The TLD server likewise does not have the final IP, but it knows which authoritative server holds records for the specific domain. It replies with the names (and IP addresses) of the authoritative name servers for example.com

5. Authoritative name server: The resolver then asks the domain’s authoritative name server (the one managed by the domain owner or hosting provider). This server has the DNS records (A, AAAA, etc.) for the domain and returns the requested IP address

6. Returning the answer: The resolver receives the IP and may cache it for the Time-To-Live (TTL) duration. It returns the IP address to the user’s computerFinally, the browser can connect directly to the web server at that IP and load the website.

## Benefits of DNS

1. Human-friendly navigation: Users can access sites with memorable names instead of numeric IPs .This drastically simplifies using the Internet.

2. Flexibility for businesses: DNS decouples names from IP addresses. A company can change web hosts or servers (and hence IP addresses) without disrupting users; only the DNS record is updated For example, if a site moves to a new server, updating its A record in DNS automatically directs visitors to the new IP. This makes migrations, load balancing, and failover much easier.

3. Branding and identity: Businesses can choose custom domain names (brandable, easy to advertise) and change underlying infrastructure transparently. E‑mail addresses also use the company’s domain, helping recognition. DNS enables all these conveniences.

4. Simplified network administration: Administrators manage mappings in one place (DNS) rather than reconfiguring every device. Adding or moving a server requires only a DNS record update, not manual changes on all clients. This centralized management reduces errors and administration effort

# Disadvantages and Vulnerabilities of DNS

1. Performance (latency): Resolving a name can require multiple network hops (resolver → root → TLD → authoritative → back), which takes time. If a name is not cached, lookups add delay .Poorly performing DNS servers or missing cache can slow down browsing.

2. DNS cache poisoning/spoofing: Attackers can inject false records into a resolver’s cache. This “poisoning” causes users to be redirected to malicious IPs without their knowledge
   For example, a poisoned cache could send users typing bank.com to a fake phishing site. (DNSSEC can help prevent this by cryptographically validating records, but DNSSEC is not universally adopted.)

3. No built-in privacy (unencrypted): By default DNS queries and responses are in plaintext. Eavesdroppers on the network can see which domains a user is looking up, posing privacy concerns. Man-in-the-middle attackers can intercept or alter DNS traffic if they control a router (e.g. public Wi‑Fi). Protocols like DNS-over-HTTPS/TLS exist to encrypt queries, but they are optional

4. Denial-of-service (DDoS) attacks: Because DNS is critical, attackers often flood DNS servers with bogus requests. In particular, DNS amplification attacks exploit open DNS resolvers to overwhelm targets with large DNS reply traffic . A targeted DDoS on root or authoritative servers could disrupt name resolution for many users.

5. Human error and misconfiguration: DNS depends on correct records. A typo or outdated entry can break access to a website or email. For instance, failing to update an A record after a server move will make the site unreachable. DNSSEC misconfigurations can even make a domain unreachable. Such errors are a significant source of outages
