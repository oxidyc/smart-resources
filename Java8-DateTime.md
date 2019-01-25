# Java 8 Date & Time API


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