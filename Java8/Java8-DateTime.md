# Java 8 Date & Time API


时间统一使用ISO-8601日历系统，也就是`yyyy-MM-dd'T'HH:mm:ss:SSSZZ`格式

java.time包目录结构:
- time：父级基础包，常用的时间相关类都在这里，如LocalDate、LocalDateTime、Instant等
- chrono：日历系统包，日历相关的接口（类似Calendar）也包括提供对其他日历系统的API
- format：格式化和解析包，主要类时DateTimeFormatter
- temporal：扩展功能包，提供细粒度的时间控制field、unit，如weeks、months、month-of-year等
- zone：时区包，时区规则、本地时区等

* LocalDate -> ISO-8601下的date对象，2007-12-03
* LocalDateTime -> ISO-8601下的date-time对象，2007-12-03T10:15:30
* LocalTime -> time对象，10:15:30
* Instant -> 一个瞬时的时间点值对象，从1970-01-01T00:00:00Z点毫秒计算的
* Clock -> 基于Instant生成的时钟对象，遵守UTC时区规则可以去生成Date和time
* Duration -> 一个time范围值对象，单位也可以时分钟或小时
* Period -> 一个date范围值对象，单位可以是年、月、日，和Duration正好是两个粒度对象
* OffsetDateTime -> 从UTC/Greenwich格式时间偏移成ISO-8061的date-time对象，2007-12-03T10:15:30+01:00
* OffsetTime -> 和OffsetDateTime类似，粒度是到time的UTC时间格式对象，10:15:30+01:00
* ZonedDateTime -> 带时区的ISO-8601日历系统的date-time对象，2007-12-03T10:15:30+01:00 Europe/Paris
* ZonedOffset -> 一个带时区的从Greenwich/UTC的偏移量范围中对象，+02:00

新旧类对比
| Java.time ISO Calendar | Java.util Calendar |
| --- | --- |
| Instant | Date |
| LocalDate、LocalTime、LocalDateTime | Calendar |
| ZonedDateTime | Calendar |
| OffsetDateTie, OffsetTime | Calendar |
| ZoneId、ZoneOffset、ZoneRules | TimeZone |
| Week Starts on Monday(1..7)  enum MONDAY, TUESDAY, ... SUNDAY | Week Starts on Sunday(1..7)  int values SUNDAY, MONDAY, ... SATURDAY |
| 12 Months(1...12) enum JANUARY, FEBRUARY, ..., DECEMBER| 12 Months(0...11) int values JANUARY, FEBRUARY, ... DECEMBER |


## Date类
LocalDate、LocalDateTime、
SimpleDateFormat


## Util
Java8的时间转为时间戳的大概的思路就是LocalDateTime先转为Instant，设置时区，然后转timestamp。

将timestamp转为LocalDateTime
```java
public LocalDateTime timestamToDatetime(long timestamp){ 
    Instant instant = Instant.ofEpochMilli(timestamp); 
    return LocalDateTime.ofInstant(instant, ZoneId.systemDefault()); 
}
```
将LocalDataTime转为timestamp
```java
public long datatimeToTimestamp(LocalDateTime ldt){
        long timestamp = ldt.toInstant(ZoneOffset.of("+8")).toEpochMilli();
        return timestamp;
    }
```


## Resource
- https://my.oschina.net/timestorm/blog/3007039
- https://www.cnblogs.com/woshimrf/p/java8-date-api.html