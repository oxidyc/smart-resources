# vue  Tutorial

## Introduce

https://cn.vuejs.org/
## Download

## Installation Steps

### 前置条件
```tcl
  + 安装node.js  v10.13.0
  + 安装npm  v6.4.1
  + 安装webpack  
     npm install webpack -g
  + 安装vue  v2.9.6
     npm install vue
  + 全局安装 vue-cli  ## vue脚手架
     npm install --global vue-cli  
```
 ### 安装步骤
 
   1. 使用webpack模板创建项目，在项目根目录中打开命令窗口并执行以下命令：
   
      vue init webpack projectName         ## projectName为项目名
     
      ![create-project](../image/vue-1.png)
     
      创建过程中需要进行一些配置，默认回车即可
      
      ![init-webpack-project](../image/vue-2.png)
      
      其中：
      
      Install vue-router?            ##是否安装vue-router默认选中yes
      
      Use ESLint to lint your code ？##是否使用ESLint管理你的代码默认选择yes
           
   2. 出现如下信息，说明创建成功；
   
      ![create-success](../image/vue-3.png)
     
   3. 进入到项目的根目录中，执行npm run dev 启动vue项目
   
      cd vuetest                            ##进入到项目根目录
     
      npm run dev                           ##启动项目
     
   4. 出现如下界面说明，项目启动成功，即可在浏览器中访问
   
      ![project-run](../image/vue-4.png)
      
## Settings
```tcl
 使用VSCode启动vue项目
  1. 安装element-ui插件和引用
      安装：npm i element-ui -S
      引用：在src/main.js中引入
      import ElementUI from 'element-ui'
      import 'element-ui/lib/theme-chalk/index.css'
      Vue.use(ElementUI)
  2. 安装axiox插件和引用
      安装：npm install --save axios vue-axios
      引用：在src/main.js中引入
      import axios from 'axios';
      import VueAxios from 'vue-axios';
      Vue.use(VueAxios, axios)
  3.解决跨域问题
  (1).在config下新建dev-host.js,并在文件中添加后台访问地址
      'use strict'
        module.exports={
            devApiHost:"http://10.10.6.38:8080"   //后端访问地址
        }
  (2).在config/index.js中进行相关配置
    调用:const devHost = require('./dev-host')
    配置:重新index.js里面的proxyTable
    其中:
    target: devHost.devApiHost//源地址
    changeOrigin: true //是否跨域
    pathRewrite: {'^/': '/'} //路径重写
    具体配置：
    proxyTable: {
      '/': {
        target: devHost.devApiHost,
        changeOrigin: true,
        pathRewrite: {
          '^/': '/'
        }
      }
    }
    配置完成后，在前端页面方法中调用即可完成前后端交互
    this.axios.get(api).then((response) => {
      console.log(response.data)
    })
  4.配置ESLint
      https://blog.csdn.net/hsl0530hsl/article/details/78594973
      使用：   "generator-star-spacing": 0       ##生成器函数*的前后空格
               "indent": ["error",2]             ##缩进风格2个空格
               "linebreak-style": [0, "windows"] ##换行风格
               "quotes": [1, "single"]           ##引号类型 ''
               "semi": [2, "always"]             ##语句强制分号结尾
  
```
## Command 
    1.启动vue项目
       npm run dev
## Keymap

## Rources
+  https://www.cnblogs.com/wx1993/p/6136892.html             ##vue使用webpack创建项目
+  https://www.cnblogs.com/hasubasora/p/7118846.html         ##安装axios
+  https://element.eleme.cn/#/zh-CN/component/installation   ##element组件安装及其使用


