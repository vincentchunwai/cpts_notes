## Footprinting Lab Hard

## Summary

1. [Check ports without service banner](#check-ports-without-service-banner)
2. [Scanning](#scanning)
3. [Connecting to imap service](#connecting-to-imap-service)
4. [Footprinting SNMP](#footprinting-snmp)
5. [Imaps Commands](#imaps-commands)

# Check ports without service banner

```bash

nc -nv <ip> <port>

```

# Scanning

```bash

nmap -sV -sC <ip> -Pn -oA target

nmap -sV --top-port 100 -sU <ip>

```

# Connecting to imap service

```bash

openssl s_client <ip>:imaps

1 LOGIN <username> <password>

```

# Footprinting SNMP

```bash

onesixtyone -c /opt/useful/seclists/Discovery/SNMP/snmp.txt <ip>

snmpwalk -v2c -c <community string> <ip>

```

# Imaps Commands

```bash

1 LIST "" *

1 SELECT <mailbox name>

1 FETCH 1 BODY[]
```



