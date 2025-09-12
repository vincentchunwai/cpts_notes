
## PowerShell Remoting (WinRM)


```powershell

PS C:\htb> Test-NetConnection -ComputerName DATABASE01 -Port 5985

ComputerName     : DATABASE01
RemoteAddress    : 192.168.1.101
RemotePort       : 5985
InterfaceAlias   : Ethernet0
SourceAddress    : 192.168.1.100
TcpTestSucceeded : True

```

## Create a PowerShell Remoting Session to DATABASE01

```PowerShell

PS C:\htb> $Session = New-PSSession -ComputerName DATABASE01

```

## Copy samplefile.txt from our Localhost to the DATABASE01 Session

```powershell

PS C:\htb> Copy-Item -Path C:\samplefile.txt -ToSession $Session -Destination C:\Users\Administrator\Desktop\

```

## Copy DATABASE.txt from DATABASE01 Session to our Localhost

```powershell

PS C:\htb> Copy-Item -Path "C:\Users\Administrator\Desktop\DATABASE.txt" -Destination C:\ -FromSession $Session

```
