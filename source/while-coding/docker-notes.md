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

```
 docker pull <image>           : copies images to docker host
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
