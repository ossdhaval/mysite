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

