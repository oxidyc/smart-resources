# Jackson @JsonTypeInfo

## 解决多态反序列化问题
@JsonTypeInfo 作用于`类/接口`，被用来开启多态类型处理，对`基类/接口` 和 `子类/实现类` 都有效
```java
@JsonTypeInfo(use = JsonTypeInfo.Id.CLASS, include = JsonTypeInfo.As.PROPERTY, property="@Clazz")
public abstract class IdEntity{}
```
- **use**: 定义使用哪一种类型识别码，有如下可选值：
    1. `JsonTypeInfo.Id.CLASS`：使用完全限定类名做识别
    2. `JsonTypeInfo.Id.MINIMAL_CLASS`：若基类和子类在同一包类，使用类名(忽略包名)作为识别码
    3. `JsonTypeInfo.Id.NAME`：一个合乎逻辑的指定名称
    4. `JsonTypeInfo.Id.CUSTOM`：自定义识别码，由@JsonTypeIdResolver对应，稍后解释
    5. `JsonTypeInfo.Id.NONE`：不使用识别码
- **include（可选）**: 指定识别码是如何被包含进去的，有如下可选值：
    1. `JsonTypeInfo.As.PROPERTY`：作为数据的兄弟属性
    2. `JsonTypeInfo.As.EXISTING_PROPERTY`：作为POJO中已经存在的属性
    3. `JsonTypeInfo.As.EXTERNAL_PROPERTY`：作为扩展属性
    4. `JsonTypeInfo.As.WRAPPER_OBJECT`：作为一个包装的对象
    5. `JsonTypeInfo.As.WRAPPER_ARRAY`：作为一个包装的数组
- **property（可选）**: 制定识别码的属性名称。此属性在以下情况中才有效：
    1. 当use=JsonTypeInfo.Id.CLASS时，若不指定property则默认为`@class`
    2. 当use=JsonTypeInfo.Id.MINIMAL_CLASS时，若不指定property则默认为`@c`
    3. 当use=JsonTypeInfo.Id.NAME时，若不指定property则默认为`@type`
    4. 满足以上三点中的任意一点的同时Include为JsonTypeInfo.As.PROPERTY、JsonTypeInfo.As.EXISTING_PROPERTY、JsonTypeInfo.As.EXTERNAL_PROPERTY时才有效
- **defaultImpl（可选）**: 如果类型识别码不存在或者无效，可以使用该属性来制定反序列化时使用的默认类型
- **visible（可选，默认为false）**: 是否可见。 属性定义了类型标识符的值是否会通过JSON流成为反序列化器的一部分，默认为fale,也就是说,jackson会从JSON内容中处理和删除类型标识符再传递给JsonDeserializer。


## Resource
- https://blog.csdn.net/u012326462/article/details/83019954
- https://www.cnblogs.com/lknny/p/5757784.html
- https://itwenti.com/?p=239
- https://blog.csdn.net/bruce128/article/details/80298808