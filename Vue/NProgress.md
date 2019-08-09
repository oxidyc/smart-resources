# NProgress 

## 简介

- 官方主页：http://ricostacruz.com/nprogress/
- Github主页：https://github.com/rstacruz/nprogress

## 安装
```tcl
# npm install -g nprogress --save
# npm install -g nprogress -S
```
在`src/main.js`中引入
```js
import NProgress from 'nprogress'
import 'nprogress/nprogress.css'

// 配置NProgress进度条选项  —— 动画效果
NProgress.configure({ ease: 'ease', speed: 500 })

router.beforeEach((to, from, next) => {
   NProgress.start()
   next()
})

router.afterEach(() => {
   NProgress.done()
})
```
修改NProgress颜色。在 App.vue 文件的 style 中增加
```css
#nprogress .bar {
   background: red !important; //自定义颜色
}
```

## 高级用法
1. `百分比`：通过设置progress的百分比，调用` .set(n)`来控制进度，其中n的取值范围为`0-1`。
```js
NProgress.set(0.0);    
NProgress.set(0.4);
NProgress.set(1.0);  
```
2. `递增`：要让进度条增加，只要调用 .inc()。这会产生一个随机增量，但不会让进度条达到100%。此函数适用于图片加载或其他类似的文件加载。
```js
NProgress.inc();
```
3. `强制完成`：通过传递 true 参数给done()，使进度条满格，即使它没有被显示。
```js
NProgress.done(true);
```
4. `minimum`：设置`最低百分比`
```js
NProgress.configure({minimum:0.1});
```
5. `template`：改变进度条的HTML结构。为保证进度条能正常工作，需要元素拥有`role=’bar’`属性。
```js
NProgress.configure({
	template:"<div class='....'>...</div>"
});
```
6. `ease`：调整动画设置，ease可传递CSS3缓冲动画字符串（如`ease`、`linear`、`ease-in`、`ease-out`、`ease-in-out`、`cubic-bezier`）。`speed`为动画速度（单位`ms`）。
```js
NProgress.configure({ease:'ease',speed:500});
```