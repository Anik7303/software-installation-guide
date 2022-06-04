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
SHOW VARIABLES LIKE %version%;

# create a user
CREATE USER 'USERNAME'@'HOST' IDENTIFIED BY 'PASSWORD';

# create database
CREATE `DATABASE_NAME`;

# grant priviledges
GRANT ALL PRIVILEDGES ON DATABASE_NAME.TABLE_NAMES TO 'USERNAME'@'HOST';

# or grant certain priviledges (CREATE, ALTER, DROP, SELECT, INSERT, UPDATE, DELETE, REFERENCES)
GRANT CREATE, DROP, SELECT, INSERT, UPDATE, DELETE ON DATABASE_NAME.TABLE_NAME TO 'USERNAME'@'HOST';

# flush priviledges
FLUSH PRIVILEDGES;

# show granted priviledges
SHOW GRANTS FOR 'USERNAME'@'HOST';

# exit repl
exit;
```

## Essential mysql plugin for django:

```bash
sudo apt update
sudo apt install libmysqlclient-dev
```
