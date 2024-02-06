# keycloak

## install
Ref: https://www.keycloak.org/getting-started/getting-started-docker

run the command below to install using docker
```
docker run -p 8080:8080 -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:23.0.6 start-dev
```

then access
```
http://localhost:8080/admin
```

User: admin, password: admin


## Local start:

```
cd ./IdeaProjects/others/oidc-with-quarkus/
sudo sh keycloak-up.sh
```

This starts a docker instance of Keycloak. You can check that using

```
docker ps
```

You can access keycloak at

```
http://localhost:8180/auth/
```

signin to the admin console using user `admin` and password `admin`.

