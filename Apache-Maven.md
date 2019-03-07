# Apache Maven Tutorial

## Introduce
 Apache Maven is a software project management and comprehension tool. Based on the concept of a project object model (POM), Maven can manage a project's build, reporting and documentation from a central piece of information. 

项目管理工具，主要作用：依赖管理、项目构建、项目信息管理
 
Home:http://maven.apache.org

## Download
http://maven.apache.org/download.cgi 本文基于`v3.6.0`版本

Maven 3.3+ require JDK 7+

http://mirrors.hust.edu.cn/apache/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.zip
## Installation Steps
 下载apache-maven-3.6.0-bin.zip后解压到d:\DEV_ENV目录下，完成安装。
 
 目录分析：
 - bin：包含mvn运行的脚本
 - boot：含有pleus-classworlds类加载器框架
 - conf：含有settings.xml配置文件
 - lib：含有maven运行时所需的Java类库
 - LICENSE.txt, NOTICE.txt, README.txt：针对maven版本，第三方软件等简要介绍
## Settings
```tcl
# 在bin/mvn.cmd中第17行添加JDK路径
SET JAVA_HOME="D:\DEV_ENV\Java\jdk1.7.0_72"
```
```xml
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
## Maven项目结构

项目构建步骤：清理 -> 编译 -> 测试 -> 报告 -> 打包 -> 部署

org.apache.maven.archetypes: maven-archetype-webapp: RELEASE

org.apache.maven.archetypes: maven-archetype-quickstart: RELEASE

mvn archetype: generate 自动创建Maven目录结构
```
- groupId：io.smart （公司、组织名称，默认是包名，必须）
- artfactId：smart-project （工程项目名称、子项目(模块)标识，默认命名方式是“项目名-模块名”，必须）
- version：1.0-SNAPSHOT （版本，必须）
- packaging：jar  （打包方式，定义项目打包方式，如jar、war、pom、zip等，可选、默认jar）
- name：smart-project  （项目描述名）
- description：Smart framework Core 
```
```
projectName 项目根目录
  |- src
  |     |- main
  |     |    |- java  项目的源码，java文件
  |     |    |- resources 项目的资源配置文件，如spring、hibernate配置文件
  |     |    |- webapp  页面素材
  |     |           |- WEB-INF
  |     |                   |- web.xml
  |     |- test
  |          |- java  测试的源码，如JUnit测试类
  |          |- resources 测试的配置文件
  |- target  项目输出目录
  |     |- classes
  |     |- generated-sources
  |     |- generated-test-sources
  |     |- maven-status
  |     |- test-classes
  |     |- <artifactId>-<version>
  |- pom.xml   maven核心文件
  ```
## Maven与IDE集成 使用教程
- Lifecycle
  - clean 清除，会删除target目录的内容
  - validate
  - compile 编译，将src/main/java下的文件编译为class文件输出到target目录下
  - test 测试，会执行src/test/java下的单元测试类。
  - package 打包，对于java工程打成jar包，对于web工程打成war包，生成未见位置在target目录下
  - verify
  - install  打包并发布到本地maven仓库，以后其他项目直接依赖这个项目即可
  - site
  - deploy 
- Plugins
  - clean
    - clean:clean
    - clean:help
  - compiler
    - compiler:compiler
    - compiler:help
    - compiler:testCompile
  - deploy
    - deploy:deploy
    - deploy:deploy-file
    - deploy:help 
  - install
    - install:help
    - install:install
    - install:install-file   
  - jar
    - jar:help
    - jar:jar
    - jar:test-jar
  - resources
    - resources:copy-resources
    - resources:help
    - resources:resources
    - resources:testResources
  - site
    - site:attach-descriptor
    - site:deploy
    - site:effective-site
    - site:help
    - site:jar
    - site:run
    - site:site
    - site:stage
    - site:stage-deploy
  - spring-boot
    - spring-boot:build-info
    - spring-boot:help
    - spring-boot:repackage
    - spring-boot:run
    - spring-boot:start
    - spring-boot:stop
  - surefire
    - surefire:help
    - surefire:test
  - war
    - war:exploded
    - war:help
    - war:inplace
    - war:manifest
    - war:war              
- Dependencies

## Resource
- MVN Repository:https://mvnrepository.com/
- Nexus aliyun : http://maven.aliyun.com/nexus/content/groups/public
