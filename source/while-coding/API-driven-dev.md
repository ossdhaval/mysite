# API driven development


There is a popular saying in the API world: "An API is as good as its documentation." Hence, API documentation is one of the tasks that should be done with utmost clarity.

When using swagger (and in general too) for API drive development, Remember there are two approaches:

### Code-first
1. Code your API implementation.
2. Automatically generate the API definition from the source code, for example, using [Swagger Core](https://github.com/swagger-api/swagger-core) [annotations](https://github.com/swagger-api/swagger-core/wiki/Swagger-2.X---Annotations) and [Swagger Maven plugin](https://github.com/swagger-api/swagger-core/tree/master/modules/swagger-maven-plugin). See the [Swagger Core wiki](https://github.com/swagger-api/swagger-core/wiki/Swagger-2.X---Getting-started) to learn more.
3. Upload the generated API definition to SwaggerHub using the SwaggerHub Maven plugin.

### Design-first
1. Write your API definition on SwaggerHub.
2. Download the API definition using the SwaggerHub Maven plugin.
3. Pass the API definition to another Swagger tool, for example:
    - Use [Swagger Codegen Maven plugin](https://github.com/swagger-api/swagger-codegen/tree/master/modules/swagger-codegen-maven-plugin) to generate API server and client code.
    - Use [Swagger Inflector](https://github.com/swagger-api/swagger-inflector) to automatically wire up the API definition to the implementation and provide out-of-the-box mocking.


## Design first approach: How to use swagger for api driven development and integrate it with Spring boot app :

### Working with editor.swagger.io

In the swagger yaml, there are four basic sections :

1) info : it has general info about API documentation like title, description, version etc
2) basepath : version info

3) tags : main category sections of api

4) schemes : http, https

5) paths : actual api details that will be categorised by tags

6) definitions : contains model information

There are many other sections but above have the main contents.

### Now you need to use this yaml in your project to do two things :

1) generate code if you want to (https://reflectoring.io/spring-boot-openapi/)

2) generate documents ( https://songrgg.github.io/operation/host-swagger-documentation-with-yaml-json-files/ )

steps below are derived from above two pages :

once your yaml file is ready then put in under src->main->resources in your project.

Let's start with step 1, code generation :

Now put below in your pom.xml

in the dependency :

```
<dependency>
  <groupId>io.springfox</groupId>
  <artifactId>springfox-boot-starter</artifactId>
  <version>3.0.0</version>
</dependency>
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
<dependency>
  <groupId>org.openapitools</groupId>
  <artifactId>jackson-databind-nullable</artifactId>
  <version>0.2.1</version>
</dependency>
```

And in plug-ins :

```
<plugin>
  <groupId>org.openapitools</groupId>
  <artifactId>openapi-generator-maven-plugin</artifactId>
  <version>4.3.1</version>
  <executions>
    <execution>
      <goals>
        <goal>generate</goal>
      </goals>
      <configuration>
        <inputSpec>${project.basedir}/src/main/resources/api.yaml</inputSpec>
        <generatorName>java</generatorName>
        <configOptions>
          <sourceFolder>src/gen/java/main</sourceFolder>
        </configOptions>
      </configuration>
    </execution>
  </executions>
</plugin>
```

now if you compile, it'll generate code for model etc

### Let's now look at generating document :

Add below to file which is having @SpringbootApplication

```
@Bean
public Docket swagger() {
    return new Docket(SWAGGER_2)
            .select()
            .apis(RequestHandlerSelectors.any())
            .paths(PathSelectors.any())
            .build();
}
```

then create a new class under ( preferably in a new package called 'com.xyz.config' ) as below :

```
package com.gsg.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Primary;
import springfox.documentation.swagger.web.InMemorySwaggerResourcesProvider;
import springfox.documentation.swagger.web.SwaggerResource;
import springfox.documentation.swagger.web.SwaggerResourcesProvider;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

@Configuration
public class SwaggerSpecConfig {

    @Primary
    @Bean
    public SwaggerResourcesProvider swaggerResourcesProvider(
            InMemorySwaggerResourcesProvider defaultResourcesProvider) {
        return () -> {
            List<SwaggerResource> resources = new ArrayList<>();
            Arrays.asList("gsg")
                    .forEach(resourceName -> resources.add(loadResource(resourceName)));
            return resources;
        };
    }

    private SwaggerResource loadResource(String resource) {
        SwaggerResource wsResource = new SwaggerResource();
        wsResource.setName(resource);
        wsResource.setSwaggerVersion("1.0");
        wsResource.setLocation("/resources/gsg-event-service-v1.yaml");
        return wsResource;
    }
}
```

Make appropriate changes to point to where your yaml files are stored in the project.


## code first approach:

 - Write code and annotate it
 - generate model from annotations ( start from : https://github.com/swagger-api/swagger-core/wiki/Swagger-2.X---Getting-started )
 - then use model to generate documentation and client library if needed


### API versioning :

A good video : https://www.youtube.com/watch?v=M2KCu0Oq3JE

## Install and Use swagger-ui locally on linux

You need to have port 80 free.

```
sudo docker run -p 80:8080 swaggerapi/swagger-ui
```

Now if you want to browse a swagger specification (json or yaml) file using swagger UI Then 

```
sudo docker run -p 80:8080 -e SWAGGER_JSON=/jans/jans-config-api/docs/jans-config-api-swagger.yaml -v /home/dhaval/IdeaProjects/Janssen/jans:/jans swaggerapi/swagger-ui
```

Now hit `http://localhost:80` and see your yaml or json swagger spec rendered using swagger UI. This is especially useful because now you can point the local copy of the spec file to locally installed REST api server and test your apis. For this you need to edit the `server` element in your local yaml. Just save the file after change and refresh the browser.



### References:

- https://dzone.com/articles/abcs-of-api-driven-development
- https://dzone.com/articles/the-api-life-cycle#:~:text=The%20API%20lifecycle%20involves%20a,designing%2C%20authentication%2C%20and%20creation.&text=In%20the%20API%20lifecycle%2C%20there,Manages%20and%20monetizes%20the%20API.
- famous apis : https://developer.paypal.com/docs/api/overview/
- twitter
