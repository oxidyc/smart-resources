# Jackson

## Introduce
Home: https://github.com/FasterXML/jackson

## Settings
https://github.com/FasterXML/jackson-databind
- jackson-core-2.9.7.jar（核心jar包）
- jackson-annotations-2.9.7.jar（注解支持）
- jackson-databind-2.9.7.jar

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.9.7</version>
</dependency>
```

## Annotation
```java
@JsonSerialize(using = UserSerializer.class) //使用自定义序列化器
@JsonIgnoreProperties({"id","name"}) //序列化时忽略指定的属性，与 @JsonIgnore冲突时，以此处为准
@JsonIgnoreProperties(ignoreUnknown=true) //忽略类中不存在的字段
public class User{
    @JsonIgnore //默认是true，与@JsonIgnore(true)同义，序列化时忽略该属性
    private Long id;

    @JsonIgnore(value=false) //序列化时不忽略该属性
    private String name;

    @JsonProperty("sex") //把该属性名称序列化为另外一个名称
    private String gender;

    @JsonFormat(pattern="yyyy-MM-dd HH:mm:ss")//日期序列化时转化为该格式
    private LocalDateTime birthday;
}

//自定义序列化器JsonSerializer
public class UserSerializer extends JsonSerializer<User>{
    @Override
    public void serializer(User user, JsonGenerator gen, SerializerProvider serializers) throws IOException, JsonProcessingException{
        gen.writeStartObject();
        gen.writeNumberField("id", user.getId());
        gen.writeStringField("name", user.getName());
        gen.writeEndObject();
    }
}

ObjectMapper mapper = new ObjectMapper();
String json = mapper.writeValueAsString(users); //序列化
String json = "{\"name\":\"zhangsan\",\"age\":20,\"birthday\":844099200000,\"email\":\"zhangsan@163.com\"}";
User user = mapper.readValue(json, User.class); //反序列化
String json = "[{\"name\":\"zhangsan\",\"age\":20,\"birthday\":844099200000,\"email\":\"zhangsan@163.com\"}]";
List<User> beanList = mapper.readValue(json, new TypeReference<List<User>>() {});//反序列化
```

```java
@JsonInclude(Include.NON_NULL) //该标记放在属性上，如果该属性为NULL则不参与序列化，如果放在类上，则对此类的全部属性起作用。
Include.ALWAYS //默认
Include.NON_DEFAULT //属性为默认值不序列化
Include.NON_EMPTY //属性为空("") 或者为NULL都不序列化
Include.NON_NULL //属性为NULL 不序列化
```