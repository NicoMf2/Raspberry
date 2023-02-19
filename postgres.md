
# Installation Postgres [^1]

## Installation product
```
sudo apt update
sudo apt full-upgrade
sudo apt install postgresql
sudo apt autoremove
```
> you need to postgres user

```
sudo su postgres
createuser <userName> -P --interactive
```
> enter the password postgres

> Give superuser 

> Create database User

```
psql
CREATE DATABASE <userName>;
exit
exit
```

## Play with postgres

```
sudo systemctl status postgresql
psql
CREATE DATABASE exampledb;
\connect exampledb;
CREATE TABLE authors (name text, website text);
INSERT INTO authors VALUES ('Emmet', 'pimylifeup.com');
SELECT * FROM authors;
COMMIT;
```

## Remote access : port 5432

```
sudo su - postgres
nano /etc/postgresql/13/main/pg_hba.conf 
host all all 192.168.100.1/24 trust
```
> Change
```
nano /etc/postgresql/13/main/postgresql.conf 
listen_addresses='localhost' by
listen_addresses='*'
exit
sudo systemctl restart postgresql
```

[^1]: source Internet 2023