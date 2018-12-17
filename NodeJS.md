# NodeJS Tutorial

## Introduce
Node.js is a JavaScript runtime built on [Chrome's V8 JavaScript engine](https://developers.google.com/v8/). Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, [npm](https://www.npmjs.com/), is the largest ecosystem of open source libraries in the world.

`Node.js®`是一个基于Chrome V8引擎的JavaScript运行环境。Node.js使用了一个事件驱动、非阻塞式I/O的模型，使其轻量又高效。

Home：https://nodejs.org
## Download
https://nodejs.org/en/download/

Node.js有两个版本，一个是LTS长期支持版本，一个是当前最新版本；推荐下载LTS版本。本文基于`v10.14.2`（包含npm 6.4.1）版本 

x64版本下载地址：https://nodejs.org/dist/v10.14.2/node-v10.14.2-x64.msi
## Installation Steps
- 1.安装Node.js，默认安装路径为d:\Program Files\nodejs
- 2.图片步骤。
## Settings
```tcl
# prefix默认路径
c:\Users\<Current User>\AppData\Roaming\npm
# cache默认路径
c:\Users\<Current User>\AppData\Roaming\npm-cache
```

​        在Node.JS的主目录下创建npm的全局模块的存放路径`node_global` 以及cache的路径`node_cache` 这两个文件夹。具体配置如下：

  方法一：启动CMD，输入如下命令：（此方法有时会失效，暂时原因不明）

```tcl
$ npm config set prefix "D:\Program Files\nodejs\node_global"
$ npm config set cache "D:\Program Files\nodejs\node_cache"

# npm安装模块时都去国外的镜像下载的，由于网络原因会导致安装模块失败，使用淘宝NPM镜像
$ npm config set registry https://registry.npm.taobao.org
```

  方法二：在nodejs安装目录内的路径为`.\node_modules\npm`的`npmrc`文件修改为：

```tcl
# %APPDATA%地址为C:\Users\<用户名>\AppData\Roaming\npm
# 默认
prefix=${APPDATA}\npm
# 修改后
prefix=D:\Program Files\nodejs\node_global
cache=D:\Program Files\nodejs\node_cache
registry=https://registry.npm.taobao.org
```

将`node_global`路径添加到 **`用户的PATH环境变量`** 中解决`不是内部或外部命令` 的错误。

```tcl
set PATH = %PATH%;D:\Program Files\nodejs\node_global
```

方法二：进入NodeJS文件的目录下，重新尝试vue -V。如果还是不行，管理员模式再次进入NodeJS安装目录尝试vue -V命令，上述方法一旦成功，以后就不用进入NodeJS安装目录也可以直接使用vue了。

添加PATH是终极方法了

# NPM
NPM(node package manager),通常称为node包管理器，是node.js的模块依赖管理工具。

```tcl
# 获取帮助
$ npm -h
Usage ：npm <command>
where <command> is one of:
    access, adduser, bin, bugs, c, cache, completion, config,
    ddp, dedupe, deprecate, dist-tag, docs, edit, explore, get,
    help, help-search, i, init, install, install-test, it, link,
    list, ln, logout, ls, outdated, owner, pack, ping, prefix,
    prune, publish, rb, rebuild, repo, restart, root, run,
    run-script, s, se, search, set, shrinkwrap, star, stars,
    start, stop, t, tag, team, test, tst, un, uninstall,
    unpublish, unstar, up, update, v, version, view, whoami

npm <cmd> -h     quick help on <cmd>
npm -l           display full usage info
npm help <term>  search for help on <term>
npm help npm     involved overview

Specify configs in the ini-formatted file:
  C:\Users\IKMS\.npmrc
or on the command line via: npm <command> --key value
Config info can be viewed via: npm help config

npm@3.10.3 D:\DEV_ENV\nodejs\node_modules\npm

# 查看npm版本
$ npm -v
6.11.3
# npm更新升级
$ npm install npm -g 或 npm install -g npm
$ npm install npm@latest -g

# 安装Node.js模块语法格式如下: pkg=Module Name
$ npm install <pkg> #表示安装最新版本
$ npm install <pkg>@<tag>

#表示安装指定版本
$ npm install <pkg>@<version> 
$ npm install element-ui@1.4.4

#安装模块指定版本号范围内的某一个版本
$ npm install <pkg>@<version range> 
$ npm install async@">=0.2.0 <0.2.9"

#安装本地文件系统中制定的目录包含的模块
$ npm install <folder>        

#安装本地模块文件
$ npm install <tarball file>  
$ npm install ./package.tgz

 #安装指定URL的模块
$ npm install <tarball url>  
$ npm install https://github.com/indexzero/forever/tarball/v0.5.6

$ npm install <git:// url>
$ npm install <github username>/<github project>

# npm的包安装分为本地安装(local)、全局安装(global)两种
# 本地安装，将安装包放在当前执行npm命令的目录的node_modules目录中
$ npm install express 
# 全局安装，使用-g 或 --global 将安装包放在/usr/local下或你node的安装目录
$ npm install express -g 

# 引导你创建一个package.json文件，包括名称、版本、作者这些信息等
$ npm init

# 安装模块的同时将信息(模块名称及其版本信息)写入package.json中
$ npm install <pkg> [-S|--save|-D|--save-dev|-O|--save-optional] 

# -S, --save安装包信息将加入到dependencies(生产阶段的依赖)
$ npm install express --save 或 npm install express -S
# -D, --save-dev安装包信息将加入到devDependencies(开发阶段的依赖)，所以开发阶段一般使用它
$ npm install express --save-dev 或 npm install express -D
# -O, --save-optional安装包信息将加入到optionalDependencies(可选阶段的依赖)
$ npm install express --save-optional 或 npm install express -O

# 显示npm的bin目录
$ npm bin

# npm config管理npm的配置路径
$ npm config set <key> <value> [-global]
# 获取npm配置
$ npm config get <key>
# 删除npm配置
$ npm config delete <key>
# 查看所有配置
$ npm config list 或 npm config ls 或 npm config ls -l

# 卸载模块
$ npm uninstall express
# 检测当前目录安装了哪些模块
$ npm ls
# 更新模块
$ npm update express
# 搜索模块
$ npm search express
# 清空NPM本地缓存
$ npm cache clear
```

## 国内优秀npm镜像

### 淘宝npm镜像

* 搜索地址：http://npm.taobao.org/
* registry地址：http://registry.npm.taobao.org/

### cnpmjs镜像

* 搜索地址：http://cnpmjs.org/
* registry地址：http://r.cnpmjs.org/

### 如何使用

1. 临时使用

   ```tcl
   $ npm --registry https://registry.npm.taobao.org install express
   ```

2. 持久使用

   ```tcl
   $ npm config set registry https://registry.npm.taobao.org

   # 配置后可通过下面方式来验证是否成功
   $ npm config get registry
   # 或
   $ npm info express
   ```

3. 通过cnpm使用

   ```tcl
   $ npm install -g cnpm --registry=https://registry.npm.taobao.org

   # 使用
   $ cnpm install express
   ```


