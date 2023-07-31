# Setup MySQL Server in Linux

## Installing `mysql-server`:

```bash
sudo apt update
sudo apt install mysql-server
```

## Configure Security:

```bash
sudo mysql_secure_installation
```

## MySQL queries:

```bash
# lauch mysql repl
sudo mysql

# or
mysql -u USERNAME -p
```

```sql
# show all databases
SHOW DATABASES;

# select a database for querying
USE `DATABASE_NAME`;

# show status
STATUS;

# show mysql version
SHOW VARIABLES LIKE '%version%';
SHOW VARIABLES LIKE 'validate_password%';

# change password policy settings
SET GLOBAL validate_password.policy = "LOW";
SET GLOBAL validate_password.length = 8;
SET GLOBAL validate_password.number_count = 0;
SET GLOBAL validate_password.special_char_count = 0;

# show all users
SELECT USER, HOST FROM mysql.user;

# create a user
CREATE USER 'USERNAME'@'HOST' IDENTIFIED BY 'PASSWORD';

# create database
CREATE DATABASE `DATABASE_NAME`;

# grant priviledges
GRANT ALL PRIVILEGES ON DATABASE_NAME.TABLE_NAMES TO 'USERNAME'@'HOST';

# or grant certain priviledges (CREATE, ALTER, DROP, SELECT, INSERT, UPDATE, DELETE, REFERENCES)
GRANT CREATE, DROP, SELECT, INSERT, UPDATE, DELETE ON DATABASE_NAME.TABLE_NAME TO 'USERNAME'@'HOST';

# flush privileges
FLUSH PRIVILEGES;

# show granted priviledges
SHOW GRANTS FOR 'USERNAME'@'HOST';

# delete user
DROP USER 'USERNAME'@'HOST';
DROP USER IF EXISTS 'USERNAME'@'HOST';

# exit repl
exit;
```

## Essential mysql plugin for django:

```bash
sudo apt update
sudo apt install libmysqlclient-dev
```

## Essential mysql plugin for PHP:

```bash
sudo apt install php-mysql
```
