# Quarkus notes

Reference:
quick start: https://developers.redhat.com/blog/2021/05/11/building-an-api-using-quarkus-from-the-ground-up#exception_handling

## how to create fresh quarkus REST API project

- run the command below:

```
mvn io.quarkus.platform:quarkus-maven-plugin:3.5.3:create     -DprojectGroupId=com.trial.quarkus     -DprojectArtifactId=member-service     -DjavaVersion=11     -DclassName=MemberController     -Dpath=members     -Dextensions=io.quarkus:quarkus-jsonb,io.quarkus:quarkus-flyway,io.quarkus:quarkus-rest-client,io.quarkus:quarkus-hibernate-orm-panache,io.quarkus:quarkus-resteasy,io.quarkus:quarkus-jdbc-postgresql,io.quarkus:quarkus-smallrye-openapi,io.quarkus:quarkus-arc,io.quarkus:quarkus-hibernate-orm,io.quarkus:quarkus-rest-client-jackson,io.quarkus:quarkus-jacoco,io.rest-assured:rest-assured,org.projectlombok:lombok
```

- Open intellij and `file -> open -> select project folder`
- project will open in intellij. Now right click on pom.xml and select `add as maven project`
- now run `./mvnw quarkus:dev`

Also, note that because you have added db related things like `quarkus-jdbc-postgresql`, when you do `./mvnw quarkus:dev`, the quarkus creates a postgre db in a docker container. This is evident from log messages like `Dev Services for default datasource (postgresql) started - container ID is e0fea71aa704`. Note the container ID in this message. The db user is `quarkus`. You can also enter this docker container and access db using below command sequence:

```
docker exec -ti e0fea71aa704 bash
<prompt will change>
psql -U quarkus
<again prompt will change>
```

Now you can run `\dt` to see all the available tables.

you can also connect to this db using pgadmin by configuring db as below. Here the password is `quarkus`:

![image](https://github.com/ossdhaval/mysite/assets/343411/c55c6196-adde-435c-83db-31267d4b72c3)

While performing operations in pgadmin on Ubutu, it is throwing errors but still working.

