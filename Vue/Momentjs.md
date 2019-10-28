# Moment.js

## Install
```tcl
npm install moment --save
```
main.js 引用
```js
import moment from 'moment'
moment.locale('zh-cn')
Vue.prototype.moment = moment
```
组件vue文件
```
this.moment().format('LL')
```

## 常见函数
- 格式化
```js
moment(1543809357000).format('LL'); //2018年12月3日 注意这是毫秒转换，参数是Number值，不能是字符串
moment.unix(1543809357).format('LL'); //2018年12月3日 注意这是秒转换，参数是Number值，不能是字符串
moment().format('L');    // 2019-02-23
moment().format('l');    // 2019-02-23
moment().format('YYYY-MM-DD H:mm');  // 2019-08-12 14:08，某些时候上面-会变成/，例如2019/02/23这时候可以手动设置格式YYYY-MM-DD
moment().format('LL');   // 2019年2月23日
moment().format('ll');   // 2019年2月23日
moment().format('LLL');  // 2019年2月23日中午11点39分
moment().format('lll');  // 2019年2月23日中午11点39分
moment().format('LLLL'); // 2019年2月23日星期六中午11点39分
moment().format('llll'); // 2019年2月23日星期六中午11点39分

moment().format('MMMM Do YYYY, h:mm:ss a'); // 二月 23日 2019, 11:36:57 中午
moment().format('dddd');                    // 星期六
moment().format("MMM Do YY");               // 2月 23日 19
moment().format('YYYY [escaped] YYYY');     // 2019 escaped 2019
moment().format(); 
```
- 时间加减
```js
moment().format("YYYY-MM-DD HH:mm:ss"); //当前时间
moment().subtract(10, "days").format("YYYY-MM-DD");    //当前时间的前10天时间
moment().subtract(1, "years").format("YYYY-MM-DD");    //当前时间的前1年时间
moment().subtract(3, "months").format("YYYY-MM-DD");   //当前时间的前3个月时间
moment().subtract(1, "weeks").format("YYYY-MM-DD");    //当前时间的前一个星期时间
 //减法subtract    加法？直接-负数即可
```
- 相对时间
```js
moment("20111031", "YYYYMMDD").fromNow(); // 7 年前
moment("20120620", "YYYYMMDD").fromNow(); // 7 年前
moment().startOf('day').fromNow();        // 12 小时前
moment().endOf('day').fromNow();          // 12 小时内
moment().startOf('hour').fromNow();       // 38 分钟前
```



## Resources
- https://www.cnblogs.com/DZzzz/p/8891612.html
- https://www.jianshu.com/p/e5b7c0606a3f
- https://blog.csdn.net/qq_38933412/article/details/82879127
- https://segmentfault.com/a/1190000016117935