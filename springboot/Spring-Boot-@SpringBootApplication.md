# Spring Boot 之 @SpringBootApplication

## @SpringBootApplication
@SpringBootApplication注解源码
```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = {
		@Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {
	...
}
```
可以分解为：
- @SpringBootConfiguration
- @EnableAutoConfiguration
- @ComponentScan

## @SpringBootConfiguration
```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Configuration
public @interface SpringBootConfiguration {

}
```
说明@SpringBootConfiguration来源于@Configuration。二者功能都是将当前类标注为配置类，并将当前类里以@Bean注解标记的方法的实例注入到spring容器中，实例名即为方法名。

@Configuration标注在类上，相当于spring-bean.xml中的\<beans\>标签的作用，主要用于Bean的注入，使用该注解注入Bean后，获取IoC容器的方式不再使用ClassPathXmlApplicationContext或文件系统路径来获取对应的IoC容器，而是使用AnnotationConfigApplicationContext(AnnotationConfiguration.class)的方式来获取IoC容器（AnnotationConfiguration为自定义的配置类）
## @EnableAutoConfiguration
```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@AutoConfigurationPackage
@Import(AutoConfigurationImportSelector.class)
public @interface EnableAutoConfiguration {
	...
}
```
@EnableAutoConfiguration 注解启用自动配置，其可以帮助 SpringBoot 应用将所有符合条件的 @Configuration 配置都加载到当前 IoC 容器之中，可以简要用图形示意如下：

## @ComponentScan
对应于XML配置形式中的\<context:component-scan\>, 用于将一些标注了特定注解的bean定义批量采集注册到Spring的IoC容器中，这些特定的注解大致包括：
- @Controller
- @Entity
- @Component
- @Service
- @Repository
等等，对于该注解，还可以通过basePackages属性来更细粒度的控制该注解的自动扫描范围，例如：
```java
@ComponentScan(basePackages = {"io.smart.controller","io.smart.entity"})
```


## Resource
- https://blog.csdn.net/leoxyk/article/details/79800020