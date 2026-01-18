# Windows Remote Management Protocols

## Summary

1. [Remote Desktop Protocol (RDP)](#remote-desktop-protocol-rdp)
2. [Footprinting RDP](#footprinting-rdp)
3. [RDP Security Check - Installation](#rdp-security-check---installation)
4. [Connecting to RDP on Linux](#connecting-to-rdp-on-linux)
5. [WinRM (Windows Remote Management)](#winrm-windows-remote-management)
6. [Footprinting WinRM](#footprinting-winrm)
7. [WMI (Windows Management Instrumentation)](#wmi-windows-management-instrumentation)
8. [Footprinting WMI](#footprinting-wmi)

## Remote Desktop Protocol (RDP)

* Network Level Authentication (NLA) is a security feature that requires authentication before a session is established.


## Footprinting RDP

```bash

nmap -sV -sC <ip> -p 3389 --script rdp*

nmap -sV -sC <ip> -p 3389 --packet-trace --disable-arp-ping -n

```

## RDP Security Check - Installation

``` bash

sudo cpan

git clone https://github.com/CiscoCXSecurity/rdp-sec-check.git && cd rdp-sec-check

./rdp-sec-check.pl <ip>

```

## Connecting to RDP on Linux

- xfreerdp
- rdesktop
- Remmina

```bash

xfreerdp /v:<ip> /u:<user> /p:<password>

```

## WinRM (Windows Remote Management)

* Uses Simple Object Access Protocol (SOAP) over HTTP or HTTPS.

* Uses ports 5985 (HTTP) and 5986 (HTTPS).

## Footprinting WinRM

```bash

nmap -sV -sC <ip> -p 5985,5986 disable-arp-ping -n

evil-winrm -i <ip> -u <user> -p <password>

```

## WMI (Windows Management Instrumentation)

* Extension of Common Information Model (CIM) for managing Windows systems.

* WMI typically accessed via PowerShell, VBScript or Windows Management Instrumentation Command-line (WMIC).

## Footprinting WMI

```bash

./wmiexec <user>:<password>@<ip> "hostname"

```



