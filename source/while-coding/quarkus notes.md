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


