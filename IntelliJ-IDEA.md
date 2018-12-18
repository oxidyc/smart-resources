# IntelliJ IDEA Tutorial

## Introduce
Home：https://www.jetbrains.com/idea
## Download
https://www.jetbrains.com/idea/download/download-thanks.html?platform=windows 本文基于`2018.3.1`版本
## License
具备edu邮箱的在校学生或教师可以申请一年免费的授权许可，许可文件可以激活JetBrains的除了TeamCity，YouTrack 和 Upsource之外的全部产品

申请地址：https://www.jetbrains.com/student/   或   https://www.jetbrains.com/zh/student/
## Installation Steps

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
  - Tab limit：15 (默认10，可以增加打开的文件 Tab 个数，当我们打开的文件超过该个数的时候，早打开的文件会被新打开的替换)
- Editor -> Font (Font: Fira Code； Size: 14)
- Editor -> Code Style -> Java -> Imports
   - Class count to use import with \'*\':99；
   - Names counts to use static import with \'*\':99
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
- Editor -> File Encodings (UTF-8, 复选Transparent native-to-ascii conversion)
- plugins
   - 安装插件lombok Plugin （Lombok 功能辅助插件）
   - 安装插件Alibaba Java Coding Guidelines （阿里巴巴出的代码规范检查插件）
   - 安装插件.ignore (各类版本控制忽略文件生成工具)
- Version Control -> Git
   - Path to Git executable: c:\Program Files\Git\cmd\git.exe
- Build,Execution,Deployment -> Build Tools -> Maven
   - Maven home directory：Bundled(Maven 3，3.3.9) 或者 自定义 D:/DEV_ENV/apache-maven-3.6.0
   - User settings file: D:\DEV_ENV\apache-maven-3.6.0\conf\settings.xml ；复选Override
   - Local repository : D:\DEV_ENV\MVN_REPO ; 复选Override
- Build,Execution,Deployment -> Build Tools -> Maven -> Importing
   - Import Maven projects automatically （复选）
## Keymap Reference

## Resource
- IntelliJ-IDEA-Tutorial：https://github.com/judasn/IntelliJ-IDEA-Tutorial
