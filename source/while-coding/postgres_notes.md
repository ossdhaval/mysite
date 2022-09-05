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

```
postgres=# CREATE USER crux_integ WITH PASSWORD 'secretpw';

```

```
ALTER USER crux_integ WITH SUPERUSER;
```
