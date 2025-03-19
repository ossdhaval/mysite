# Postgres Notes

## Using docker

install postgres using docker:

```
sudo docker run --name postgresql-container -p 5432:5432 -e POSTGRES_PASSWORD=secretpw -d postgres
```

If you have already created the container above, then just start it

```
sudo docker start postgresql-container
```

start PGadmin (but this was not able to query the db and giving internal server errors):

```
docker run --rm -p 5050:5050 thajeztah/pgadmin4
```

login to the postgres container shell:
```
sudo docker exec -ti p1 bash
```

then switch to default user
```
su postgres
```

start psql
```
psql
```

Now you can do `\dt` to see all the tables. And execute select queries.

## without docker direct install on Machine

Good referece : https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-20-04

once installed you can start and stop postgres using command like below:

```
sudo systemctl start postgresql.service
```



## creating user and db

During installation, postgres has created a new **linux** user called `postgres` you can use this login:

```
sudo -u postgres psql
```

### create a different user

first create a linux user: 

```
sudo adduser crux_integ
```

Create new db user with same name as linux user

```
sudo -u postgres

createuser --interactive

```

## Navigating Postgres

In PostgreSQL, a database is a self-contained unit of data storage, while a schema is a logical namespace within a database that groups related objects like tables, views, and functions, enabling better organization and security

Create db

```
sudo -i -u postgres

createdb crux_db
```

connect using new user to new db

```
sudo -i -u crux_user

psql -d crux_db
or
\c crux_db

```

Set the password for db user

```
crux_db=#  ALTER USER crux_user PASSWORD 'secretpw';
```

List all available users:

```
crux_db=#  \du
```

List all available db:

```
crux_db=#  \l
```

List all available tables:

```
crux_db=#  \dt
```

Describe a table and know the columns

```
\d <table-name>
```

To exit psql prompt:

```
crux_db=#  \q
```



## Install PGAdmin

```
// to add PGadmin repository to your system
curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo apt-key add
sudo sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'

// actually installs PGAdmin
sudo apt install pgadmin4
```
