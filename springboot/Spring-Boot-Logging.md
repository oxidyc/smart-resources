# Spring Boot Logging

Spring内部日志系统使用的是`Apache Commons Logging`，并提供对 `Java Util Logging`，`Log4j2`，`Logback`的支持，如使用Spring Boot `Starters` 那么默认使用`Logback`。

### 日志输出内容元素
- 时间日期：精确到毫秒
- 日志级别：INFO、WARN、ERROR、DEBUG、TRACE
- 进程ID：
- 分隔符：- 标识实际日志的开始
- 线程名：方括号括起来（可能会截断控制台输出）
- Logger名：通常使用源代码的类名
- 日志内容：
### 控制台输出
Logging配置的级别有7个（从低到高）：
`TRACE`、`DEBUG`、`INFO`、`WARN`、`ERROR`、`FATAL`、`OFF`

如设置为WARN，则低于WARN的信息都不会输出。

Spring Boot 中默认配置ERROR、WARN、INFO级别的日志输出到控制台

### 文件输出
默认情况，Spring Boot将日志输出到控制台，不会写到日志文件。

使用`application.properties` 或 `application.yml`配置：

- `logging.file`：设置文件，可以是绝对路径也可以是相对路径。如：logging.file=my.log
- `logging.path`：设置目录，会在该目录下创建spring.log文件，并写入日志内容。如：logging.path=/var/log
> 二者不能同时使用，如若同时使用，则只有logging.file生效 \
> 默认情况，日志文件的大小达到10MB时会切分一次，产生新的日志文件，默认级别为：ERROR、WARN、INFO
### 级别控制
- `logging.level`：日志级别控制前缀，* 为包名或Logger名。格式为`logging.level.* = LEVEL`

举例：
```
logging.level.root=WARN
logging.level.io.smart=INFO
```
## 自定义日志配置
- Logback： `logback-spring.xml`, `logback-spring.groovy`, `logback.xml`, `logback.groovy`
- Log4j：`log4j-spring.properties`, `log4j-spring.xml`, `log4j.properties`, `log4j.xml`
- Log4j2：`log4j2-spring.xml`, `log4j2.xml`
- JDK：`logging.properties`

Spring Boot 推荐优先使用带有 `-spring` 的文件名作为你的日志配置。默认的命名规则，并且放在`src/main/resources`下面即可。

如想完全掌控日志配置，并自定义文件名称，则在application.yml中通过设置logging.config属性。
```
logging.config=classpath:logging-config.xml
```

## Resource
- https://blog.csdn.net/inke88/article/details/75007649
- https://www.cnblogs.com/zhangzhen894095789/p/6640808.html
- https://www.codesheep.cn/2018/03/29/Boot日志框架实践/