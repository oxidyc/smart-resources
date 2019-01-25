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

## enum枚举类型
- @JsonValue 序列化时枚举对应生成的值 ，作用在enum的属性上
- @JsonCreator 反序列化时的初始化函数，入参为 对应该枚举的json值
- @JsonFormat(shape = JsonFormat.Shape.OBJECT) 作用在enum Class上，将enum转化为对象，该对象有get和set方法的属性会被序列化。

总结: 
1. jackson会优先使用@JsonCreator注解标注的构造方法构造枚举值
2. jackson会通过@JsonValue注解标注的方法作为value值构建value与枚举值的map映射
3. jackson会通过枚举值的ordinal值与枚举值构建map映射
```java
import com.fasterxml.jackson.annotation.JsonCreator;
import com.fasterxml.jackson.annotation.JsonValue;

@JsonFormat(shape = JsonFormat.Shape.OBJECT)
public enum Gender{
    SECRET(9,"保密"),
    MALE(1,"男"),
    FEMALE(2,"女");

    private final int value;
    private final String desc;
    Gender(int value,String desc){
        this.value=value;
        this.desc=desc;
    }

    @JsonCreator
    public static Gender valueOf(int genderCode){
        for (Gender gender:values()){
            if (gender.value== genderCode){
                return gender;
            }
        }
        throw new IllegalArgumentException("No matching constant for ["+genderCode+"]");
    }

    @JsonValue
    public int value(){
        return this.value;
    }

    public String getDesc() {
        return this.desc;
    }
}
```
```json
{
    "gender":{"desc":"男"}
}
//如果需要输出value，则需要增加getValue方法
{
    "gender":{"value":1,"desc":"男"}
}

//使用@JsonValue 直接输出值，此时@JsonFormat不起作用
{
    "gender": 1
}
```

## 配置SerializationFeature
- `WRAP_ROOT_VALUE`: 是否环绕根元素，默认false，如果为true，则默认以类名作为根元素，你也可以通过@JsonRootName来自定义根元素名称
- `INDENT_OUTPUT`: 是否缩放排列输出，默认false，有些场合为了便于排版阅读则需要对输出做缩放排列
- `WRITE_DATES_AS_TIMESTAMPS`: 序列化日期时以timestamps输出，默认true
- `WRITE_ENUMS_USING_TO_STRING`: 序列化枚举是以toString()来输出，默认false，即默认以name()来输出
- `WRITE_ENUMS_USING_INDEX`: 序列化枚举是以ordinal()来输出，默认false
- `WRITE_SINGLE_ELEM_ARRAYS_UNWRAPPED`: 序列化单元素数组时不以数组来输出，默认false
- `ORDER_MAP_ENTRIES_BY_KEYS`: 序列化Map时对key进行排序操作，默认false
- `WRITE_CHAR_ARRAYS_AS_JSON_ARRAYS`: 序列化char[]时以json数组输出，默认false
- `WRITE_BIGDECIMAL_AS_PLAIN`: 序列化BigDecimal时之间输出原始数字还是科学计数，默认false，即是否以toPlainString()科学计数方式来输出

## 配置DeserializationFeature
- `FAIL_ON_UNKNOWN_PROPERTIES`: json中多余的参数不报错，默认


## 类型转换
生成json时，将所有Long转换成String
```java
SimpleModule simpleModule = new SimpleModule(); 
simpleModule.addSerializer(Long.class, ToStringSerializer.instance); 
simpleModule.addSerializer(Long.TYPE, ToStringSerializer.instance); 
objectMapper.registerModule(simpleModule);
```

## Resources
- https://blog.csdn.net/my_flash/article/details/50802961
- https://www.jianshu.com/p/d29b9f32e5fe
- https://www.baeldung.com/jackson-serialize-enums
- [Serializing enums with Jackson](https://stackoverflow.com/questions/7766791/serializing-enums-with-jackson)
- [自定义Jackson序列化 @JsonSerialize](https://blog.csdn.net/u012326462/article/details/83019881)
- [jackson中自定义处理序列化和反序列化](https://blog.csdn.net/zhao1949/article/details/79281967)
- [jackson annotations注解详解](https://blog.csdn.net/sdyy321/article/details/40298081)
- [spring学习笔记---Jackson的使用和定制](https://www.cnblogs.com/mumuxinfei/p/4761374.html)
