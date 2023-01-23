`sudo apt install wget ca-certificates`
`wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -`
`sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'`

Install
`sudo apt update`
`apt install postgresql postgresql-contrib`

Connect to db via default admin:
`sudo -u postgres psql`  

Create db, user, privs to user on created db:
postgres=# `create database testdb;`  
postgres=# `create user testuser with encrypted password '1qazXSW@CDE#'; ` 
postgres=# `grant all privileges on database testdb to testuser;`
```bash
GRANT ALL ON ALL TABLES IN SCHEMA public to db_user
```
```bash
GRANT ALL ON ALL SEQUENCES IN SCHEMA public to db_user;

```
```bash
GRANT ALL ON ALL FUNCTIONS IN SCHEMA public to db_user;
```

Allow connection to db from this or other hosts:

sudo nano /etc/postgresql/15/main/postgresql.conf
	`listen_addresses = '*'`
sudo nano /etc/postgresql/15/main/pg_hba.conf
	`local all all testuser md5`
	`host all all 0.0.0.0/0 md5`