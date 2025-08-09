# Linux Remote Management Protocols

## SSH

* SSH-1 is vulnerable to MITM (Man in the Middle) attacks

## OpenSSH authentication methods

1. Password authentication
2. Public-key authentication
3. Host-based authentication
4. Keyboard authentication
5. Challenge-response authentication
6. GSSAPI authentication

## Dangerous Settings

|Settings|Description|
|PasswordAuthentication yes|Allows password authentication, which is less secure than public key authentication.|
|PermitEmptyPasswords yes|Allows login with empty passwords, which is insecure.|
|PermitRootLogin yes|Allows root login, which is a security risk.|
|Protocol 1|Uses the older and less secure SSH-1 protocol.|
|X11Forwarding yes|Allows X11 forwarding, which can be a security risk if not properly configured.|
|AllowTcpForwarding yes|Allows TCP forwarding, which can be a security risk if not properly configured.|
|PermitTunnel yes|Allows tunneling, which can be a security risk if not properly configured.|
|DebianBanner yes|Enables the display of the Debian banner, which can reveal information about the system.|


## Footprinting SSH

* SSH-Audit

```bash

git clone https://github.com/jtesta/ssh-audit.git && cd ssh-audit

./ssh-audit.py <ip>

```

## Change Authentication Methods

```bash

ssh -v <user>@<ip> -o PreferredAuthentications=password

```

## Rsync

* Rsync is a file transfer protocol that can be used over SSH or as a standalone service.

```bash

nc -nv <ip> 873

rsync -av --list-only rsync://<ip>/path/to/directory

```

## R-Services

R-commands:

- `rcp`: Remote copy command
- `rlogin`: Remote login command
- `rsh`: Remote shell command
- `rexec`: Remote execution command
- `rusers`: Remote users command
- `rwho`: Remote who command
- `rstat`: Remote status command
- `rwall`: Remote wall command
- `rfs`: Remote file system command
- `rmt`: Remote tape command
- `rquota`: Remote quota command
- `rfsck`: Remote file system check command
- `ruptime`: Remote uptime command

## Scanning for R-Services

```bash

sudo nmap -sV -p 512,513,514 <ip>

```




