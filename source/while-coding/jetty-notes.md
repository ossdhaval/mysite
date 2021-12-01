# Jetty notes

### Imp commands

`java -jar $JETTY_HOME/start.jar --list-config`
- lists current configuration of the server

- location for jetty logs : `vim $JETTY_BASE/logs/`

#### Enable jetty logging:

```
> cd $JETTY_BASE
> java -jar $JETTY_HOME/start.jar --add-to-start=logging-jetty
```

above will create 

```
$JETTY_BASE/resources/jetty-logging.properties
```

You can edit this file to enable logging levels for different packages. Commented examples are given in default generated file itself. For example, if you want to enable debug level for Jetty itself, then uncomment line below and set logging level to`DEBUG`.

```
org.eclipse.jetty.LEVEL=DEBUG
```

Log file will be created at `$JETTY_BASE/logs/`

### How Jetty configuration properties work

Every module has xml and corresponding one or more ini files. Mapping is given at home/modules/http.mod
base/start.d/http.ini -> home/etc/jetty-http.xml

users will change values in ini files to configure module properties

if you look at xmls, they are like bean configurations for various jetty classes. Like spring beans. Jetty actually uses an IoC container to inject these beans created using these xmls.

You can also give property values in jetty start.jar command line argument also if you don't want to modify ini file.

like

```
java -jar start.jar jetty.http.port=8080
```

### Jetty default configuration files can be downloaded from 
- jetty.xml: https://github.com/eclipse/jetty.project/blob/jetty-9.4.x/jetty-server/src/main/config/etc/jetty.xml
- jetty-http.xml: https://github.com/eclipse/jetty.project/blob/jetty-9.4.x/jetty-server/src/main/config/etc/jetty-http.xml
- jetty-ssl.xml: https://github.com/eclipse/jetty.project/blob/jetty-9.4.x/jetty-server/src/main/config/etc/jetty-ssl.xml 
- jetty-ssl-context.xml: https://github.com/eclipse/jetty.project/blob/jetty-9.4.x/jetty-server/src/main/config/etc/jetty-ssl-context.xml
- jetty-https.xml: https://github.com/eclipse/jetty.project/blob/jetty-9.4.x/jetty-server/src/main/config/etc/jetty-https.xml

### Jetty SSL self signed certificate can be downloaded from 
- https://github.com/eclipse/jetty.project/blob/jetty-9.4.x/jetty-server/src/main/config/modules/ssl/keystore
- default password is `storepwd`
