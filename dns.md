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
