# JPA Primary Key（PK，主键）

## 主键 @Id
```java
@Entity
public Class User{
  @Id @GeneratedValue long id;
}
```
- 自动主键，使用`@GeneratedValue`注解有数据库自动生成主键
- 应用主键，由应用程序负责初始化主键值

## 非嵌入式复合主键，@IdClass
非嵌入式类，使用@IdClass注解为实体指定一个复合主键类（通常由两个或更多基元类型或JDK对象类型组成）。从原有数据库映射时（此时数据库主键由多列组成），通常将出现复合主键。

特征：
- POJO类
- 必须Public，并且必须有一个public无参构造函数
- 必须可序列化，定义equals和hashCode方法
- 字段或属性的类型和名称必须保持一致
```java
@Entity
@IdClass(ProjectPK.class)
public Class Project{
  @Id long id;
  @Id long organizationId;
}

Class ProjectPK implements Serializable{
  long id;
  long organizationId;
}
```
## 嵌入式复合主键，@EmbeddedId ，@Embeddable
由实体拥有的嵌入类。使用@EmbeddedId注解指定一个实体拥有的可嵌入式复合主键类。
```java
@Entity
public Class Project{
  @EmbeddedId ProjectPK id;
}

@Embeddable
Class ProjectPK implements Serializable{
  long id;
  long organizationId;
}
```


## Resources
- https://blog.csdn.net/tracycater/article/details/78319021