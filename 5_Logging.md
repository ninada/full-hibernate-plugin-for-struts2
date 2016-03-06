# Usage #

Full Hibernate Plugin uses Log4j framework for logging debug/warn/error messages. You can config this by log4j properties file or by using the **struts.devMode** property from Struts2. **By default**, the **WARN** level messages are always printed in the console (version 1.5+).

## Struts2 devMode configuration ##

If you set the **struts.devMode** property to **true**, all DEBUG level messages from Full Hibernate Plugin will be printed.


## Log4j configuration ##

All relevant Actions and Interceptors of Full Hibernate Plugin are at the package **com.googlecode.s2hibernate.struts2.plugin**, so, you can configura the logging usgin Log4j properties like this example:

```
log4j.rootLogger=DEBUG, stdout
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout

log4j.appender.stdout.layout.ConversionPattern=%d [%t] %-5p %c - %m%n

log4j.logger.com.googlecode.s2hibernate.struts2.plugin=DEBUG
```