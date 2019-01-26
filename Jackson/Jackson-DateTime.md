# Jackson 

## Overview
- `Parameter names`: support for detecting constructor and factory method ("creator") parameters without having to use `@JsonProperty` annotation 
  - provides `com.fasterxml.jackson.module.paramnames.ParameterNamesModule`
- `Java 8 Date/time`: support for Java 8 date/time types (specified in JSR-310 specification) 
  - provides `com.fasterxml.jackson.datatype.jsr310.JavaTimeModule`
  - ALSO provides legacy variant `com.fasterxml.jackson.datatype.jsr310.JSR310TimeModule`
  -  difference between 2 modules is that of configuration defaults: use of `JavaTimeModule` strongly recommended for new code
- `Java 8 Datetypes`: support for other new Java 8 datatypes outside of date/time: most notably `Optional`, `OptionalLong`, `OptionalDouble`
  - provides `com.fasterxml.jackson.datatype.jdk8.Jdk8Module`

## Maven dependencies
```xml
<dependency>
    <groupId>com.fasterxml.jackson.module</groupId>
    <artifactId>jackson-module-parameter-names</artifactId>
</dependency>
<dependency>
    <groupId>com.fasterxml.jackson.datatype</groupId>
    <artifactId>jackson-datatype-jdk8</artifactId>
</dependency>
<dependency>
    <groupId>com.fasterxml.jackson.datatype</groupId>
    <artifactId>jackson-datatype-jsr310</artifactId>
</dependency>
```
## Registering modules
```java
ObjectMapper mapper = new ObjectMapper();

DateTimeFormatter dtf = DateTimeFormatter.ofPattern(pattern);
JavaTimeModule timeModule = new JavaTimeModule();

timeModule.addSerializer(LocalDate.class,new LocalDateSerializer(dtf));
timeModule.addDeserializer(LocalDate.class,new LocalDateDeserializer(dtf));

timeModule.addSerializer(LocalDateTime.class,new LocalDateTimeSerializer(dtf));
timeModule.addDeserializer(LocalDateTime.class,new LocalDateTimeDeserializer(dtf));

// Disable writing dates as timestamps
//方式一
mapper.configure(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS,false);
//方式二
mapper.disable(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS);

// https://github.com/FasterXML/jackson-modules-java8
//方式一
mapper.registerModule(new ParameterNamesModule())
    .registerModule(new Jdk8Module())
    .registerModule(timeModule)
    .registerModule(new JavaTimeModule());
//方式二
mapper.registerModules(new ParameterNamesModule(), new Jdk8Module(), timeModule, new JavaTimeModule());    
```