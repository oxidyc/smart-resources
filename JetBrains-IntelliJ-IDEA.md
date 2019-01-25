# IntelliJ IDEA Tutorial

## Introduce
Home：https://www.jetbrains.com/idea
## Download
https://www.jetbrains.com/idea/download/download-thanks.html?platform=windows 本文基于`2018.3.1`版本
## License
具备edu邮箱的在校学生或教师可以申请一年免费的授权许可，许可文件可以激活JetBrains的除了TeamCity，YouTrack 和 Upsource之外的全部产品

申请地址：https://www.jetbrains.com/student/   或   https://www.jetbrains.com/zh/student/
## Installation Steps
1. **UI Themes**
   - Darcule（深色主题）
   - Light
2. **Default plugins**
   - Java Frameworks
      - 复选：Hibernate、Spring、Java EE、 AspectJ
   - Build Tools（默认）
   - Web Development
      - 复选：HTML、Less、CSS、Sass、JavaScript
   - Version Controls
      - 复选：Git、Github、Subversion
   - Test Tools（默认）
   - Application Servers
      - 复选：Tomcat and TomEE、Jetty
   - Clouds
      - 全部取消复选
   - Swing（默认）
   - Android（默认）
   - Database Tools（默认）
   - Other Tools（默认）
   - Plugin Development（默认）
## Settings
- Appearance & Behavior -> Appearance -> Windows Options
  - Show memory indicator （复选,显示内存使用情况）
- Appearance & Behavior -> System Settings
  - Reopen last project on startup （取消）
  - Confirm application exit （复选）
  - Confirm window to open project in (单选，每次都弹出提示窗口，让我们选择用新窗口打开或是替换当前项目窗口。)
- Editor -> General
  - Change font size(Zoom) with Ctrl+Mouse Where （复选，`增加 Ctrl + 鼠标滚轮` 快捷键来控制代码字体大小显示）
- Editor -> General -> Auto Import -> Java
  - Add unambiguous imports on the fly （复选）
  - Optimize imports on the fly(for current project) （复选）
- Editor -> General -> Appearance
  - Show line numbers (复选，显示行号)
  - Show method separators (复选，显示方法线，便于方法区分)
- Editor -> General -> Code Completion
  - Match case 选择 First letter only
- Editor -> General -> Editor Tabs
  - Show tabs in one row （取消，多行显示打开的文件）
  - Tab limit：`15` (默认10，可以增加打开的文件 Tab 个数，当我们打开的文件超过该个数的时候，早打开的文件会被新打开的替换)
- Editor -> Font (Font: `Fira Code`； Size: `14`)
- Editor -> Code Style
   - General -> Hard wrap at:`120` (默认80，每行字符数，代码自动换行)
- Editor -> Code Style -> Java -> Imports
   - Class count to use import with \'*\':`99`；
   - Names counts to use static import with \'*\':`99`
- Editor -> Code Style -> Java -> Code Generation -> Comment Code
   - Line Comment at first column （取消，单行注释的两个斜杠跟随在代码的头部，而非行头部）
   - Block Comment at first column （取消，同上）
- Editor -> File and Code Templates -> Includes
   - File Header 添加如下代码
      ```java
      /**
      * ${NAME} Class
      *
      * @author <b>用户名</b>, Copyright &#169; 2018
      * @version 1.0, ${YEAR}-${MONTH}-${DAY} ${TIME}
      */
      ```
      > `用户名` 命名规则 : 使用固定的英文名称；或使用姓名，其中姓的全拼并且首字母大写，名的拼音首字母。当姓名为两个字时，名使用全拼。例如张三 -> Zhangsan ； 王小五 -> Wangxw
- Editor -> File Encodings (`UTF-8`, 复选Transparent native-to-ascii conversion)
- Plugins
   - 安装插件Lombok Plugin 
   - 安装插件Alibaba Java Coding Guidelines 
   - 安装插件.ignore
- Version Control -> Git
   - Path to Git executable: `c:\Program Files\Git\cmd\git.exe`
- Build,Execution,Deployment -> Build Tools -> Maven
   - Maven home directory：`Bundled(Maven 3，3.3.9)` 或者 自定义 `D:/DEV_ENV/apache-maven-3.6.0`
   - User settings file: `D:\DEV_ENV\apache-maven-3.6.0\conf\settings.xml` ；复选Override
   - Local repository : `D:\DEV_ENV\MVN_REPO` ; 复选Override
- Build,Execution,Deployment -> Build Tools -> Maven -> Importing
   - Import Maven projects automatically （复选）

## Plugins
- Lombok Plugin（Lombok 功能辅助插件）
- Alibaba Java Coding Guidelines（阿里巴巴出的代码规范检查插件）
- SonarLint
- .ignore  (各类版本控制忽略文件生成工具)
- Kotlin
- Gitee（Oschina开源中国码云官方插件）
## Keymap Reference

## Resource
- IntelliJ-IDEA-Tutorial：https://github.com/judasn/IntelliJ-IDEA-Tutorial


## Previous Releases
 https://www.jetbrains.com/idea/download/previous.html
 - ` Version：`[2018.3.2](https://download.jetbrains.com/idea/ideaIU-2018.3.2.exe) `Build：`183.4886.37 `Released：`December 18, 2018
- ` Version：`[2018.3.1](https://download.jetbrains.com/idea/ideaIU-2018.3.1.exe) `Build：`183.4588.61 `Released：`December 5, 2018
- `Version：`[2018.2.7](https://download.jetbrains.com/idea/ideaIU-2018.2.7.exe) `Build：`182.5107.41 `Released：`November 27, 2018
- `Version：`[2018.1.7](https://download.jetbrains.com/idea/ideaIU-2018.1.7.exe) `Build：`181.5540.23 `Released：`November 20, 2018
- `Version：`[2017.3.6](https://download.jetbrains.com/idea/ideaIU-2017.3.6.exe) `Build：`173.4674.60 `Released：`November 20, 2018
- `Version：`[2017.2.7](https://download.jetbrains.com/idea/ideaIU-2017.2.7.exe) `Build：`172.4574.19 `Released：`March 2, 2018
- `Version：`[2017.1.6](https://download.jetbrains.com/idea/ideaIU-2017.1.6.exe) `Build：`171.4694.73 `Released：`March 5, 2018
- `Version：`[2016.3.8](https://download.jetbrains.com/idea/ideaIU-2016.3.8.exe) `Build：`163.15529.8 `Released：`March 5, 2018
- `Version：`[2016.2.5](https://download.jetbrains.com/idea/ideaIU-2016.2.5.exe) `Build：`162.2228.15 `Released：`October 17, 2016
- `Version：`[2016.1.4](https://download.jetbrains.com/idea/ideaIU-2016.1.4.exe) `Build：`145.2070.6 `Released：`August 3, 2016
- `Version：`[15.0.6](https://download.jetbrains.com/idea/ideaIU-15.0.6.exe) `Build：`143.2370.31 `Released：`November 2, 2015
- `Version：`[14.1.7](https://download.jetbrains.com/idea/ideaIU-14.1.7.exe) `Build：`141.3058 `Released：`May 11, 2016
- `Version：`[14.0.5](https://download.jetbrains.com/idea/ideaIU-14.0.5.exe) `Build：`139.1803 `Released：`May 12, 2016