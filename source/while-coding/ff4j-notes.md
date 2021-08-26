# FF4J notes:

- **feature store**: For distributed architecture, `feature store` works as central repo for all feature toggles which all the microservices can refer.
- **permission based feature toggles**: 
- **conditional feature toggles**:


- FF4J works using strategies.You can create your own strategies too.


## trying out jdbc sample

- sample we are trying out is `https://github.com/ff4j/ff4j-samples/tree/master/webapp-jetty/ff4j-sample-simplejdbc`
- Notable changes:
  - change the Jersey class name in `web.xml` 
    - from ` <servlet-class>com.sun.jersey.spi.container.servlet.ServletContainer</servlet-class>` to `<servlet-class>org.glassfish.jersey.servlet.ServletContainer</servlet-class>`
    - got error `UnsatisfiedLinkError: Can't load library: /usr/lib/jvm/java-11-openjdk-amd64/lib/libawt_xawt.so` : 
      - this was resolved when I set JAVA_HOME to amazon corretto instead of `/usr/lib/jvm/java-11-openjdk-amd64`
