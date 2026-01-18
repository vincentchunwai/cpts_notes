## Simple Network Management Protocol (SNMP)

## Summary

1. [SNMP Daemon Config](#snmp-daemon-config)
2. [Dangerous Settings](#dangerous-settings)
3. [Footprinting the Service](#footprinting-the-service)
4. [Tools Overview](#tools-overview)

SNMP Daemon Config:

cat /etc/snmp/snmpd.conf | grep -v "#" | sed -r '/^\s*$/d'

sysLocation    Sitting on the Dock of the Bay
sysContact     Me <me@example.org>
sysServices    72
master  agentx
agentaddress  127.0.0.1,[::1]
view   systemonly  included   .1.3.6.1.2.1.1
view   systemonly  included   .1.3.6.1.2.1.25.1
rocommunity  public default -V systemonly
rocommunity6 public default -V systemonly
rouser authPrivUser authpriv -V systemonly

# Dangerous Settings:

rwuser noauth ->  Provide access to full OID tree without authentication

rwcommunity <community string> <IPv4 address> -> Provide access to full OID tree regardless of where the request comes from

rwcommunity6 <community string> <IPv6 address> -> Same access as with rwcommunity with difference of using IPv6 address

# Footprinting the Service:

1. snmpwalk 
   -v2c: SNMP version 2c
   -c: community string (e.g. public)
   <ip address>: target IP address

   Example: snmpwalk -v2c -c public

2. onesixtyone e.g. onesixtyone -c /opt/useful/seclists/Discovery/SNMP/snmp.txt 10.129.14.128
3. braa.Snmpwalk e.g. braa <community string>@<IP>:.1.3.6.*


# Tools Overview

| Tool Name | Purpose | Use Case |
|-----------|---------|----------|
| snmpwalk  | Retrieve SNMP data from a device | Enumerate OIDs, gather system/network details |
| onesixtyone | SNMP brute-forcing tool | Guess community strings for SNMPv1/v2c |
| braa | Bulk SNMP queries against multiple devices | Efficient for large networks |


Current version: SNMPv3

Transmit control commands using agents over UDP port 161

[Trap] Notify manager about an event over UDP Port 162

SNMP client and server must have unique addresses known as OIDs (Object Identifiers)

[MIB] Management Information Base:

- Independent format for storing device information

- text file

- tree structure 

- Written in ASN.1 (Abstract Syntax Notation One)

[OID] Object Identifier:

Example:

1.3.6.1.2.1.1.1.0: Device description.
1.3.6.1.2.1.2.2.1.10: Incoming traffic on an interface.

[SNMPv1] Simple Network Management Protocol version 1:

- no built-in authentication or encryption

[SNMPv2c] Simple Network Management Protocol version 2c (Community):

- uses community strings for authentication (plaintext passwords used for authentication)

- community strings can be intercepted and read
[SNMPv3] Simple Network Management Protocol version 3:

- provides authentication and encryption (pre-shared keys or certificates)



