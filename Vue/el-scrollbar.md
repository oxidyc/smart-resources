# Element-UI隐藏滚动条组件scrollbar的使用

src: packages/scrollbar/src/main.js
```css
<el-scrollbar>
  <your-components/>
</el-scrollbar>
将会出现滚动的内容放到上述标签内就可以了。 
这里要简单的设置一下，将标签的height设为100%，查看效果的时候，会出现一个横向的滚动条，如果你不想要横向的滚动条，使用下面css属性设置就可以只显示竖向滚动条。
.el-scrollbar{height：100%;}
ps:如果竖向滚动条旁边有1px的竖线，则是因为原始滚动条隐藏的时候，距离不够。只要将margin-right:-15px改成margin-right:-16px即可。
 
.el-scrollbar__wrap {
overflow-x: hidden;
}
ps: 同时显示横向和竖向滚动条，不能设置overflow:hidden,而是要针对overflow-x: hidden(让浏览器原始滚动条隐藏);设置，否则竖向的滚动条会不随滚轮滚动。
```


### Resources
- https://segmentfault.com/q/1010000018573262