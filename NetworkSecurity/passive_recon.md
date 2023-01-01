# Passive recon

> Passive recon: Info gained via public knowledge, without direct engagement with target

**Examples:**

- Looking for DNS records from public DNS server
- Looking up org info on public forums
  - Org's website
  - Social media pages
  - News & articles around the org 
  - Advertisement links and pages
- 

**Tools for querying DIRECTLY publically available networkelements**

- `whois`: WHOIS servers
- `nslookup`: DNS servers
- `dig`: DNS servers

**Tools for querying INDIRECTLY publically available network elements**

- `DNSDumpster`: WHOIS servers
- `Shodan.io`: DNS servers
- `dig`: DNS servers

### `whois` lookup

- **WHOIS** is a req/res protocol. 
- It uses `TCP port:43` for incoming requests
- Maintained by domain registrar
- Info gained
  - ⭐️ Registrar details
  - Contact info of registrant(privacy settings can make these hidden)
    - email and phone details are more often hidden to prevent abuse by web-crawlers and bots
  - Creation, updation and expiration dates
  - ⭐️ DNS used for domain name resolution 

```shell
whois tryhackme.com
whois everrover.com
```

### `nslookup`: Name Server Lookup

```shell
# Format: nslookup OPTIONS everrover.com SERVER
nslookup everrover.com
nslookup -type=A everrover.com 1.1.1.1
```

`-type` is the kind of DNS records. A few of those listed below:
| RECORD | Desc
|---|---|
|⭐️`A`|IPv4 address|
|⭐️`AAAA`|IPv6 address|
|CNAME|Canonical Name|
|MX|Mail exchange servers|
|SOA|Start of Authority|
|NS|Nameserver|
|TXT|TXT records|

`server` is the DNS server to be queried. `1.1.1.1` and `1.0.0.1` for **Cloudflare**. `8.8.8.8` and `8.8.4.4` for **Google**. Others to be looked up on the net.

All obtained IPs and MX servers can be looked up for vulnerabilities.

### `dig`: Domain Information Groper

Used for advanced DNS lookup ops

```shell
# Format: dig @SERVER everrover.com TYPE
dig tryhackme.com
dig @1.1.1.1 tryhackme.com MX 
dig tryhackme.com MX
```

## Finding sub-domains for root domain: *Sub-domain enumeration*

*The way: Using **search-engines**. Not one, but many!* This is used by **DNSDumpster**. It also lists IP addresses for listed sub-domains.

Publically available tools:
- [DNSDumpster](https://dnsdumpster.com/) :: sub-domain enumeration
- [Shodan.IO](https://shiodan.io/) :: **sub-domain IP tracking.**

IP tracking via [Shodan.IO](https://shiodan.io/) reveals key pieces of information such as
- IP addresses
- Hosting org
- Geography and location
- Server type and version
- Open ports used for DNS services

### Links

- [Shodan room at THM](https://tryhackme.com/room/shodan)
- [Shodan Help](https://help.shodan.io/the-basics/search-query-fundamentals)

### Other sub-domain enumeration tools

- 