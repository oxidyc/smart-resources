# ES6

## 

1. 用`&&`和`||`简化`if{}else{}`的写法 [via](https://www.520mwx.com/view/67017)
- if else 的写法
  ```js
  if ( this.pointJson[0]){
    const d=[+this.pointJson[0].Lng, +this.pointJson[0].Lat]; 
  } else {
    const d=[120.079551, 30.319468];
  }
  ```
  表示如果传入数组为非空，则赋值传入的经纬度数据；如果表示如果传入数组为空，则赋值固定的经纬度数据。
- && 和 || 的用法
  * `a() && b()`;如果执行a()后返回true，则执行b()并返回b的值；如果执行a()后返回false，则整个表达式返回a()的值，b()不执行；
  * `a() || b()` :如果执行a()后返回true，则整个表达式返回a()的值，b()不执行；如果执行a()后返回false，则执行b()并返回b()的值；
  * `&& 优先级高于 ||`
  * `a() && b()||c()`;如果执行a()后返回true,则执行b()并返回b的值，不执行c()；如果执行a()后返回false，则执行c()并返回c()的值；
- 实例
  ```js
  const d = this.pointJson[0] && [+this.pointJson[0].Lng, +this.pointJson[0].Lat] || [120.079551, 30.319468]
  ```
  解释：如果执行this.pointJson[0]后返回true，则执行[+this.pointJson[0].Lng, +this.pointJson[0].Lat] ，并返回其值；如果执行this.pointJson[0]后返回false，则执行 [120.079551, 30.319468]并返回其值。其逻辑与#1相同。
  含义：表示如果传入数组为非空，则赋值传入的经纬度数据；如果表示如果传入数组为空，则赋值固定的经纬度数据。