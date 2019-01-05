# Google Gson

## Introduce

Home：https://github.com/google/gson

## Download
```xml
<dependency>
  <groupId>com.google.code.gson</groupId>
  <artifactId>gson</artifactId>
  <version>2.8.5</version>
</dependency>
```

## 常见用法
- 序列化与反序列化
```java
Data obj = new Gson().fromJson(dataStr,Data.class);
String  dataStr = new Gson().toJson(obj);
```
- 日期格式化
```java
Gson gson = new GsonBuilder().setDateFormat("yyyy-MM-dd HH:mm:ss").create();
```
- 注册序列化适配器
```java
Gson gson = new GsonBuilder().registerTypeAdapter(LocalDateTime.class, new JsonSerializer<LocalDateTime>(
    @Override
    public JsonElement serializer(LocalDateTime src, Type typeOfStr, JsonSerializationContext context){
        return new JsonPrimitive(src.format(DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss")));
    }
)).retisterTypeAdapter(LocalDate.class, new JsonSerializer<LocalDate>(
    @Override
    public JsonElement serializer(LocalDate src, Type typeOfStr, JsonSerializationContext context){
        return new JsonPrimitive(src.format(DateTimeFormatter.ofPattern("yyyy-MM-dd")));
    }
)).create();

//jdk 8 lambda
Gson gson = new GsonBuilder().registerTypeAdapter(LocalDateTime.class, (JsonSerializer<LocalDateTime>) (src, typeOfSrc, context) ->{
        new JsonPrimitive(src.format(DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss")));
}).retisterTypeAdapter(LocalDate.class, (JsonSerializer<LocalDate>)(src, typeOfStr, context)->{
        new JsonPrimitive(src.format(DateTimeFormatter.ofPattern("yyyy-MM-dd")));
    }
)).create();
```
- 注册反序列化适配器
```java
Gson gson = new GsonBuilder().registerTypeAdapter(LocalDateTime.class, new JsonDeserializer<LocalDateTime>(
    @Override
    public LocalDateTime deserialize(JsonElement json, Type type, JsonDeserializationContext  context) throws JsonParseException{
        String datetime = json.getAsJsonPrimitive().getAsString(); 
        return LocalDateTime.parse(datetime, DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss"));
    }
)).retisterTypeAdapter(LocalDate.class, new JsonDeserializer<LocalDate>(
    @Override
    public LocalDate  deserialize(JsonElement json, Type type, JsonDeserializationContext  context) throws JsonParseException{
         String datetime = json.getAsJsonPrimitive().getAsString();
         return LocalDate.parse(datetime, DateTimeFormatter.ofPattern("yyyy-MM-dd"));
    }
)).create();
```

## Resource 
- https://blog.csdn.net/IamOceanKing/article/details/54312504
- https://github.com/google/gson/blob/master/UserGuide.md