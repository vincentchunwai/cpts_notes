# DNS


## Footprinting DNS

```bash

dig version.bind CHAOS TXT @<ip> # Get the version of the DNS server

```

## Zone Transfer

```bash

dig axfr @<ip> <domain> # Zone transfer

dig @<ip> <domain> ANY # Get all records for a domain

```

## Metasploit Modules and Nmap Scripts

```bash

msfconsole
use auxiliary/gather/enum_dns
nmap -n --script "(default and *dns*) or fcrdns or dns-srv-enum or dns-random-txid or dns-random-srcport" <IP>

```

| **DNS Concept**            | **Description**                                                                 | **Example**                                      |
|-----------------------------|---------------------------------------------------------------------------------|--------------------------------------------------|
| Domain Name                 | A human-readable label for a website or other internet resource.                | www.example.com                                  |
| IP Address                  | A unique numerical identifier assigned to each device connected to the internet.| 192.0.2.1                                       |
| DNS Resolver                | A server that translates domain names into IP addresses.                        | Your ISP's DNS server or public resolvers like Google DNS (8.8.8.8) |
| Root Name Server            | The top-level servers in the DNS hierarchy.                                     | There are 13 root servers worldwide, named A-M: a.root-servers.net |
| TLD Name Server             | Servers responsible for specific top-level domains (e.g., .com, .org).          | Verisign for .com, PIR for .org                  |
| Authoritative Name Server   | The server that holds the actual IP address for a domain.                       | Often managed by hosting providers or domain registrars. |
| DNS Record Types            | Different types of information stored in DNS.                                   | A, AAAA, CNAME, MX, NS, TXT, etc.                |


## Virtual Host

```bash

gobuster vhost -u http://<target_ip> -w <wordlist> --append-domain

```

