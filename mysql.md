# Mysql

Scanning MySQL Servers:

```bash

sudo nmap 10.129.14.128 -sV -sC -p 3306 --script mysql*

```

## Interaction with MySQL Server

```bash

mysql -u root -p <password> -h <server_ip>

```

## MySQL Commands

```sql
SHOW DATABASES;

USE <database_name>;

SHOW TABLES;

SELECT * FROM <table_name>;
SHOW COLUMNS FROM <table_name>;

```


