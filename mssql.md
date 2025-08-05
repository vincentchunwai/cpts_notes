# MSSQL

Default system database:

|Default System Database|Description|
|----------------------|-----------|
|master                |Contains system-level information, including server configuration and login accounts.|
|model                 |Template for new databases; defines the structure of new databases created on the server.|
|msdb                 |Used by SQL Server Agent for scheduling jobs, alerts, and operators.|
|tempdb               |Temporary workspace for storing intermediate results and temporary objects; recreated each time SQL Server starts.|
|resource              |Used for managing server resources and monitoring performance.|


# Default Configuration

When an admin initially installs and configures MSSQL to be network accessible, the SQL service will likely run as [NT SERVICE\MSSQLSERVER]. Connecting from the client-side is possible through Windows Authentication, and by default, encryption is not enforced when attempting to connect.


[Windows Authentication]

underlying Windows OS will process the login request and use either local SAM database or Active Directory to authenticate the user.


# Dangerous Settings

- MSSQL clients not using encryption to connect to the MSSQL server.
- The use of self-signed certificates when encryption is being used. It is possible to spoof self-signed certificates
- The use of [named pipes]
- Weak & default sa credentials. Admins may forget to disable this account.

# Commands

```bash

sudo nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 10.129.201.248

```

# Metasploit

```bash

use auxiliary/scanner/mssql/mssql_ping

set rhosts <ip>

run

```

# Connecting with Mssqlclient.py

```bash

curl -O https://raw.githubusercontent.com/SecureAuthCorp/impacket/master/examples/mssqlclient.py

python3 mssqlclient.py Administrator@10.129.201.248 -windows-auth

select name from sys.databases

```


