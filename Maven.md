# Apache Maven Tutorial

## Introduce
 Apache Maven is a software project management and comprehension tool. Based on the concept of a project object model (POM), Maven can manage a project's build, reporting and documentation from a central piece of information. 
 
Home:http://maven.apache.org

## Download
http://maven.apache.org/download.cgi 本文基于`v3.6.0`版本

Maven 3.3+ require JDK 7+

http://mirrors.hust.edu.cn/apache/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.zip
## Installation Steps
 下载apache-maven-3.6.0-bin.zip后解压到d:\DEV_ENV目录下，完成安装。
## Settings
```
# 在bin/mvn.cmd中第17行添加JDK路径
SET JAVA_HOME="D:\DEV_ENV\Java\jdk1.7.0_72"

# 在conf/settings.xml中的<settings>根节点下添加本地仓库地址
<localRepository>D:/DEV_ENV/MVN_REPO</localRepository>

# 添加到conf/settings.xml 中的<settings>根节点下的<mirrors>节点中
<mirror>
<id>nexus-aliyun</id>
<mirrorOf>*</mirrorOf>
<name>Nexus aliyun</name>
<url>http://maven.aliyun.com/nexus/content/groups/public</url>
</mirror>
```
## Resource
- MVN Repository:https://mvnrepository.com/
- Nexus aliyun : http://maven.aliyun.com/nexus/content/groups/public
