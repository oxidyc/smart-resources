# Nginx  Tutorial

## Introduce
Nginx (engine x) 是一个高性能的HTTP和反向代理服务，也是一个IMAP/POP3/SMTP服务。

Home: http://www.nginx.org
## Download
  版本下载地址为：http://nginx.org/download/ 

  本文基于`nginx-1.14.2`版本，下载地址：http://nginx.org/download/nginx-1.14.2.tar.gz
## Installation Steps

### 前置条件
```tcl
# wget安装。网络上自动下载文件的自由工具。
yum -y install wget
# gcc 安装。编译源码。
yum install -y gcc gcc-c++
# pcre pcre-devel 安装。 perl兼容的正则表达式库。
yum install -y pcre pcre-devel
# zlib安装。 压缩和解压缩。
yum install -y zlib zlib-devel
# OpenSSL安装。安全套接字层密码库。
yum install -y openssl openssl-devel
```
### 安装步骤

1. 使用wget下载nginx包：
```
 cd /usr/local
 wget http://nginx.org/download/nginx-1.14.2.tar.gz
``` 
2. 解压`nginx-1.14.2.tar.gz` 二进制包
```
 tar -zxvf nginx-1.14.2.tar.gz
```
3. 配置nginx，这里使用默认配置
```
 cd nginx-1.14.2
 ./configure
```
4. 安装，默认安装目录为/
```
 make && make install
```
5. 在/usr/local/nginx/sbin目录下，启动nginx服务

指令为：
```
 cd /usr/local/nginx/sbin
 ./nginx
```
6. 配置防火墙或关闭防火墙后，在浏览器中输入`http://10.10.6.126:80`查看，显示如下内容表示连接成功。
 ```
    Welcome to nginx ......
```
## Settings

防火墙firewall配置：
+ 添加80端口

相关命令如下：
```
firewall-cmd --zone=public --add-port=80/tcp --permanent   #添加80端口
firewall-cmd --reload      #更新防火墙规则
firewall-cmd --zone=public --query-port=80/tcp    #查看端口状态
firewall-cmd --zone=public --remove-port=80/tcp --permanent    #删除开放的端口

```

## Command 
```
在nginx安装目录sbin下执行命令：
cd /usr/local/nginx/sbin
    ./nginx            #启动nginx服务
    ./nginx -s stop    #此方式停止步骤是待nginx进程处理任务完毕进行停止。 
    ./nginx -s quit    #此方式相当于先查出nginx进程id再使用kill命令强制杀掉进程。
    ./nginx -s reload  #重新载入配置文件
    ./nginx -s reopen  #重启nginx服务
    ./nginx -v         #查看版本
    ./nginx -t         #查看nginx的配置文件
    ./nginx -h         #帮助
```
## Keymap

## Rources

+ https://blog.csdn.net/wxyjuly/article/details/79443432


