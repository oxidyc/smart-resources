# Spring Webflux

## Webflux是什么
名称中的Flux来源于Reactor中的类Flux，包含了对反应式HTTP、服务器推送事件和WebSocket的客户端和服务器端的支持。在服务器端，WebFlux支持两种不同的编程模型：一是Spring MVC中使用的基于Java注解的方式；二是基于Java8 的lambda表达式的函数式编程模型。这两种编程模型只是在代码编写方式上存在不同。他们运行在同样的反应式底层架构上，因此在运行时是相同的。WebFlux需要底层提供运行时的支持,可以运行在支持Servlet3.1非阻塞IO API 的Servlet容器上，或是其他异步运行时环境，如Netty和Undertow。
![webflux](../image/spring-webflux.png)

- 左侧：传统的基于Servlet的Spring Web MVC框架
- 右侧：5.0版本新引入的基于Reactive Streams的Spring Webflux框架，从上到下依次是Router Functions，WebFlux，Reactive Streams三个新组件
   * `Router Functions`：对标@Controller,@RequestMapping等标准的Spring MVC注解，提供一套函数式风格的API，用于创建Router，Handler和Filter。
   * ` WebFlux`：核心组件，协调上下游各个组件提供响应式编程支持。
   * `Reactive Streams`：一种支持背压（Backpressure）的异步数据流处理标准，主流实现有RxJava和Reactor，Spring WebFlux默认集成的是Reactor






## Resource
- [springboot 使用webflux响应式开发教程（一）](https://blog.csdn.net/wshl1234567/article/details/80320116)
- [使用 Spring 5 的 WebFlux 开发反应式 Web 应用 ](https://www.ibm.com/developerworks/cn/java/spring5-webflux-reactive/index.html)