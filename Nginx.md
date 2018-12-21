# Nginx  Tutorial

## Introduce
Nginx (engine x) 是一个高性能的HTTP和反向代理服务，也是一个IMAP/POP3/SMTP服务。

Home: http://www.nginx.org
## Download
安装所需环境下载：
+ PCRE库
  
  PCRE(Perl Compatible Regular Expressions) 是一个Perl库，包括 perl 兼容的正则表达式库。nginx 的 http 模块使用 pcre 来解析正则表达式，所以需要在 linux 上安装 pcre 库，pcre-devel 是使用 pcre 开发的一个二次开发库。nginx也需要此库。
  
  本文使用的版本是pcre-8.33，其下载地址为：http://jaist.dl.sourceforge.net/project/pcre/pcre/8.33/pcre-8.33.tar.gz
  
  其它版本下载地址为：
  + https://sourceforge.net/projects/pcre/files/pcre/
  + http://jaist.dl.sourceforge.net/project/pcre/pcre/
  
  Home: http://www.pcre.org/
+ SSL库

  OpenSSL是一个强大的安全套接字层密码库，囊括主要的密码算法、常用的密钥和证书封装管理功能及SSL协议，并提供丰富的应用程序供测试或其它目的使用，nginx 不仅支持http协议，还支持https（即在ssl协议上传输http），所以需要在 Centos 安装OpenSSL库。
    
  本文使用的版本是openssl-1.0.1j,其下载地址为：http://www.openssl.org/source/openssl-1.0.1j.tar.gz
  
  其它版本下载地址为：https://www.openssl.org/source/
  
  Home: https://www.openssl.org/
+ zlib库
    
  zlib 库提供了很多种压缩和解压缩的方式， nginx 使用 zlib 对 http 包的内容进行 gzip ，所以需要在 Centos 上安装 zlib 库。

  本文使用的版本是zlib-1.2.11，其下载地址为：http://zlib.net/zlib-1.2.11.tar.gz
  
  其它版本下载地址为：http://www.zlib.net/fossils/
  
  Home: http://zlib.net/
   
+ Nginx下载

  本文使用的版本是nginx-1.14.2，其下载地址为：http://nginx.org/download/nginx-1.14.2.tar.gz
  
  其它版本下载地址为：http://nginx.org/download/
## Installation Steps

## Settings

## Keymap

## Rources


