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

start PGadmin:

```
docker run --rm -p 5050:5050 thajeztah/pgadmin4
```

## without docker direct install on Machine

Good referece : https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-20-04

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

Create new user

```
postgres=# CREATE USER crux_integ WITH PASSWORD 'secretpw';

```

Make him super user:

```
postgres=# ALTER USER crux_integ WITH SUPERUSER;
```

Create db

```
sudo -u postgres createdb sammy
```

connect using new user to new db

```
sudo -u sammy psql
psql -d postgres
```

To exit psql prompt:

```
postgres=# \q
```

List all available users:

```
postgres=# \du
```

