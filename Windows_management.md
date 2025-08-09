# Windows Remote Management Protocols

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



