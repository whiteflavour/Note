# 报错信息如下：

```
log4j:WARN No appenders could be found for logger (io.netty.util.internal.logging.InternalLoggerFactory).
log4j:WARN Please initialize the log4j system properly.
log4j:WARN See http://logging.apache.org/log4j/1.2/faq.html#noconfig for more info.
```

# 解决方法：

在`main`方法中加入：

1. `BasicConfigurator.configure()`
2. 添加`log4j.properties`配置文件，详细配置如下。

# log4j.properties 文件简单配置：

```properties
# Set root logger level to DEBUG and its only appender to A1.
log4j.rootLogger=DEBUG, A1

# A1 is set to be a ConsoleAppender.
log4j.appender.A1=org.apache.log4j.ConsoleAppender

# A1 uses PatternLayout.
log4j.appender.A1.layout=org.apache.log4j.PatternLayout
log4j.appender.A1.layout.ConversionPattern=%-4r [%t] %-5p %c %x - %m%n
```

(from: https://stackoverflow.com/questions/12532339/no-appenders-could-be-found-for-loggerlog4j)