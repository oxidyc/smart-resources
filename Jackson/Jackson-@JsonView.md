# Jackson @JsonView


用来过滤序列化对象的属性，可以有选择的序列化对象，首先定义一个View类，里面包含我们对要序列化的字段的定义，也可以将View类理解为一组标识。

使用步骤：
1. 使用接口来声明多个视图
2. 在返回值对象的get方法指定视图
3. 在Controller方法上指定视图


## Resources
- https://blog.csdn.net/weixin_38118016/article/details/80977841
- https://segmentfault.com/a/1190000016662666?utm_source=tag-newest
- https://www.jianshu.com/p/9635f0e14eef
- https://www.jianshu.com/p/dab9dae5bf20
- https://blog.csdn.net/Dongguabai/article/details/80884774