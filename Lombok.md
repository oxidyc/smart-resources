# Lombok

## 配置
### Maven依赖
```xml
<dependency>
	<groupId>org.projectlombok</groupId>
	<artifactId>lombok</artifactId>
	<version>1.16.16</version>
</dependency>
```
### IDE集成（JetBrains IntelliJ IDEA Plugins）
Lombok插件主页：https://github.com/mplushnikov/lombok-intellij-plugin

IDEA直接安装步骤：
- 安装插件：Settings -> Plugins -> Browse repositories -> Lombok Plugin 
- 配置参数：Settings -> Build,Execution,Deployment -> Compiler -> Annotation Processors -> 复选Enable annotation processing 
- 重启IDEA  

## 主要注解
- `@Getter`、`@Setter`：自动为属性提供Set和Get方法
- `@ToString`：为类自动生成toString()方法
- `@EqualsAndHashCode`：为对象字段自动生成hashCode和equals实现
- `@AllArgsConstructor`, `@RequiredArgsConstructor`, `@NoArgsConstructor`：为类自动生成对应参数的constructor
- `@Log`，`@Log4j`，`@Log4j2`，`@Slf4j`，`@XSlf4j`，`@CommonsLog`，`@JBossLog`：自动为类添加对应的log支持
- `@Data`：自动为所有字段添加@ToString，@EqualsAndHashCode，@Getter，为非final字段添加@Setter，和@RequiredArgsConstructor，本质上相当于几个注解的综合效果
- `@NonNull`：自动帮助我们避免空指针。作用在方法参数上的注解，用于自动生成空值参数检查
- `@Cleanup`：自动帮我们调用close()方法。作用在局部变量上，在作用域结束时会自动调用close()方法释放资源