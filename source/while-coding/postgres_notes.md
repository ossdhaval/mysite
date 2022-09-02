# Postgres Notes

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
