# Java 8 - Stream

## 定义
Stream是Java API的新成员，它允许你以声明性方式处理数据集合（通过查询语句来表达，而不是临时编写一个实例）

接口定义在java.util.stream.Stream里

```java
List<Dish> menu = Dish.MENU;
// 从menu获得流
List<String> threeHighCaloricDishNames = menu.stream()
        // 通过链式操作，筛选出高热量的菜肴
        .filter(d -> d.getCalories() > 300)
        // 获取菜名
        .map(Dish::getName)
        .limit(3)
        .collect(Collectors.toList());
// [pork, beef, chicken]
System.out.println(threeHighCaloricDishNames);
```
## Stream与集合

和迭代器类似，**`流Stream只能遍历一次`**。遍历完之后，我们就说这个流已经被消费掉了。你可以从原始数据源那里再获得一个新的流来重新遍历一遍，就像迭代器一样（这里假设它是集合之类的可重复的源，如果是I/O通道就没戏了）。

## Stream 操作
java.util.stream.Stream 中的 Stream 接口定义了许多操作。它们可以分为两大类。

```java
//中间操作
List<String> names = menu.stream()
                // 中间操作
                .filter(d -> d.getCalories() > 300)
                // 中间操作
                .map(Dish::getName)
                // 中间操作
                .limit(3)
                // 将Stream转为List
                .collect(toList());

List<String> names = menu.stream()
                .filter(d -> {
                    System.out.println("filtering:"+d.getName());
                    return d.getCalories() > 300;
                })
                .map(dish -> {
                    System.out.println("mapping:"+dish.getName());
                    return dish.getName();
                })
                .limit(3)
                .collect(toList());
System.out.println(names);                

//终端操作
menu.stream().forEach(System.out::println);

long count = menu.stream()
                .filter(d -> d.getCalories() > 300)
                .distinct()
                .limit(3)
                .count();
```


流的使用一般包括三件事
1. 一个数据源（比如集合）来执行查询
2. 一个中间操作链，形成一条流的流水线
3. 一个终端操作，执行流水线，并能生成结果。

Stream的流水线背后的理念类似于构建器模式。在构建器模式中有一个调用链来设置一套配置（对Stream来说这就是一个中间操作链），接着调用built方法（对Stream来说就是终端操作）。

中间：

| 操作 |  类型 | 返回类型 | 操作参数 | 函数描述 |
| --- | --- | --- | --- | --- | ---| 
| filter`(筛选)` | 中间 | Stream<T> | Predicate<T> | T -> boolean |
| map`(提取)` | 中间 | Stream<R> | Function<T,R> | T -> R |
| limit`(截断)` | 中间 | Stream<T> |    |   |
| sorted | 中间 | Stream<T> | Comparator<T> | (T,T) -> int |
| distinct | 中间 | Stream<T> |  |  |

终端：

| 操作 | 类型 | 目的 |
| --- | --- | --- |
| foreach | 终端 | 消费流中的每个元素并对其应用Lambda。这一操作返回void |
| count | 终端 | 返回流中元素的个数。这一操作返回long |
| collect | 终端 | 把流归约成一个集合，比如List、Map甚至是Integer |

Stream是一个非常好用的一个新特性，它能帮助我们简化很多冗长的代码，提高我们代码的可读性。

总结：
1. Stream是“从支持数据处理操作的源生成的一系列元素”。
2. Stream利用内部迭代：迭代通过filter、map、sorted等操作被抽象掉了。
3. Stream操作有两类：中间操作和终端操作。
4. filter和map等中间操作会返回一个Stream，并可以链接在一起。可以用它们来设置一条流水线，但并不会生成任何结果。
5. forEach和count等终端操作会返回一个非流的值，并处理流水线以返回结果。
6. Stream中的元素是按需计算（懒加载）的。


## Resources
- [Java 8之stream进阶](https://segmentfault.com/a/1190000015806792)
- [《Java8实战》-第四章读书笔记（引入流Stream）](https://segmentfault.com/a/1190000016145140)
- [Java 8之stream介绍和使用](https://segmentfault.com/a/1190000015723744)
- [Java 8之stream实际应用](https://segmentfault.com/a/1190000016062437)
