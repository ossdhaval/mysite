# Docker notes

To view all available images :
```
docker images
```

Build image :
```
docker build -t <image-name> <dir where Dockerfile is kept>
docker build -t event-service .
```

create a container using image :
```
docker create <image-name>
output is a container id
```

Start a container
```
docker start container-id
```

to create and start in one go ( more preferred then above two ):
```
docker run <image>           
docker container run -d --name event-service-cntnr -p 8080:8080 event-service
```

to see currently running containers
```
docker ps
```

to see all the containers available
```
docker ps -a
```

To stop a container
```
docker stop <container-name>
```

To operate on multiple containers. this will stop all the containers
```
docker stop $(docker ps -aq)
```

To remove a container
```
docker rm <container-name>
```

To remove all containers
```
docker rm $(docker ps -a -q)
```

to remove an image
```
docker rmi <imagename>
```

to remove all images

```
docker rmi -f $(docker images -aq)

```

To remove everything unused in docker. This removes unused images, networks etc.

```
docker system prune -a -f
```

copies images to docker host

```
 docker pull <image> 
```

get into shell of a running container :
```
docker exec -ti <container-id> bash
```

to come out of bash and keep the container running : 
```
ctrl P+Q
```

Access logs of a container 
```
docker logs <container-name>
```


#### Containerise a spring-boot app using docker :

create a Dockerfile in the root folder where the target folder resides. Dockerfile content

```
FROM openjdk:11
ARG JAR_FILE=target/gsg-event-service-1.0-SNAPSHOT.jar
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

Now use below command to build image. Here the tag could be anything :

```
docker build -t event-service .
```

Now use below command to create container using the image :

```
docker container run -d --name web1 -p 8080:8080 event-service
```

Now, hit localhost:8080 to access your app.


#### How to install and run jenkins using dockers :

```
docker pull jenkins/jenkins:lts

docker container run -p 8080:8080 jenkins/jenkins:lts
```

in the log that is printed on the screen while container is coming up, there will be a password string printed, keep that password. It is password for 'admin' user that is auto created.

then access
http://localhost:8080
or 
http://localhost:8080/


#### docker volumes :

Docker can store data in three different ways :

1) Volumes ( recommended )
2) Mounts
3) tmpfs ( in-memory )

volume is most preferred. And has many advantages over mounts.
Basic difference between a volume and mount is that with mount you can specify a directory on your local machine which docker should mount on the container's file system. You have control over this directory. While when you use a volume, a new directory is created within Docker’s storage directory (/var/lib/docker/volumes/) on the host machine and this directory is mounted on container's file system. Docker manages that directory’s contents.

ref :

- https://docs.docker.com/storage/volumes/
- https://docs.docker.com/storage/bind-mounts/

it is storage space on your hard disk which you ask docker container to use when you create a container. This is important when you are using docker to run software like jenkins, where you want to  persist state of software running in the container so that you don't have to recreate and reconfigure it when you restart the container.

```
docker container run -d -p 8080:8080 -v jenkinsvol1:/var/jenkins_home --name jenkins-local jenkins/jenkins:lts
```

In above case, a directory called 'jenkinsvol1' will be created under /var/lib/docker/volumes/
and mounted to container's file system under '/var/jenkins_home'

```
docker container run -d -p 8080:8080 -v /home/jenkinsvol1:/var/jenkins_home --name jenkins-local jenkins/jenkins:lts
```

commands for volume : 


create volume : 

```
docker volume create <name>
```

list volumes :

```
docker volume ls
```

details of a volume :

```
docker volume inspect <name>
```

remove a volume :

```
docker volume rm <name>
```

_**Note**_ : use volumes when you want to store data that is persisted even if you stop or remove container. Or if you want to share data across containers and machines. But if you want to store temporary data then you should use tmpfs if you are on linux. 
https://docs.docker.com/storage/tmpfs/


Pass environment variables at the start of the container with `-e`

```
sudo docker container run -d  -e KEYCLOAK_USER='admin' -e KEYCLOAK_PASSWORD='admin' --name custom-kc-container -p 8080:8080 custom-kc
```

### know if the image is new or same as old

you can use `inspect` command

```
sudo docker image ls
```

```
REPOSITORY                TAG         IMAGE ID       CREATED        SIZE
janssenproject/monolith   1.0.3_dev   0a32df8668fd   24 hours ago   370MB
janssenproject/monolith   <none>      548be1516b12   2 days ago     370MB
mysql                     8.0.30      43fcfca0776d   2 weeks ago    449MB
```

```
sudo docker image inspect 0a32df8668fd
```

```
[
    {
        "Id": "sha256:0a32df8668fd50e598e145d56f4e805417ad6062cdb18823dc2a97d72e304185",
        "RepoTags": [
            "janssenproject/monolith:1.0.3_dev"
        ],
        "RepoDigests": [],
        "Parent": "",
        "Comment": "buildkit.dockerfile.v0",
        "Created": "2022-09-29T14:05:20.136637609+05:30",
        "Container": "",
        "ContainerConfig": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": null,
            "Cmd": null,
            "Image": "",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": null
        },
        "DockerVersion": "",
        "Author": "",
        "Config": {
```

In above output, you can see the sha and creation date of the image.

### Notes:

- what is diff between `docker run` and `docker container run`

Reference:
  - very good quick turotial for using docker with intellij and quickly create containers, install db, and use docker compose:
  https://www.youtube.com/watch?v=ck6xQqSOlpw&t=1038s


## Install docker-engine, compose and desktop on Ubuntu 22.04

This worked perfectly :

https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository

## Docker compose build and redeploy code

```
sudo docker-compose ps
sudo docker-compose build
sudo docker-compose rm
sudo docker-compose up
```

Get list of docker compose projects running currently:

```
docker compose ls
```

Get list of containers running as part of a docker project

```
docker compose -f jans-mysql-compose.yml ps
```

Docker compose down doesn't completely remove everything. It will not remove the volumes or images for example. To remove everything use

```
docker compose down --rmi all --volumes
```

## know ip address of a docker container

`sudo docker inspect <container name or id> | grep IPAddress`

## copy files from docker container to host

```
docker cp <containerId>:/file/path/within/container /host/path/target
```

## docker compose networking

By default Compose sets up a single network for your app. Each container for a service joins the default network and is both reachable by other containers on that network, and discoverable by the service's name. Your app's network is given a name based on the "project name", which is based on the name of the directory it lives in. 

```
services:
  web:
    build: .
    ports:
      - "8000:8000"
  db:
    image: postgres
    ports:
      - "8001:5432"
```

When you run docker compose up, the following happens:

- A network called myapp_default is created.
- A container is created using web's configuration. It joins the network myapp_default under the name web.
- A container is created using db's configuration. It joins the network myapp_default under the name db.
  
Each container can now look up the service name web or db and get back the appropriate container's IP address. For example, web's application code could connect to the URL postgres://db:5432 and start using the Postgres database.

It is important to note the distinction between HOST_PORT and CONTAINER_PORT. In the above example, for db, the HOST_PORT is 8001 and the container port is 5432 (postgres default). Networked service-to-service communication uses the CONTAINER_PORT. When HOST_PORT is defined, the service is accessible outside the swarm as well.

Within the web container, your connection string to db would look like postgres://db:5432, and from the host machine, the connection string would look like postgres://{DOCKER_IP}:8001 for example postgres://localhost:8001 if your container is running locally.
