# Visual Studio Code Tutorial

## Introduce

Home:https://code.visualstudio.com/
## Download
地址1：https://code.visualstudio.com/docs/?dv=win64user

地址2：https://aka.ms/win32-x64-user-stable

本文基于`v1.30.0`版本，下载地址：
https://vscode.cdn.azure.cn/stable/c6e592b2b5770e40a98cb9c2715a8ef89aec3d74/VSCodeUserSetup-x64-1.30.0.exe

## Installation Steps
1. 安装向导
![setuping](image/vscode-1.png)
2. 许可协议
![license](image/vscode-2.png)
3. 选择目标位置
![target-location](image/vscode-3.png)
4. 选择开始菜单文件夹
![start-menu](image/vscode-4.png)
5. 选择其他任务
![other-setting](image/vscode-5.png)
复选资源管理器文件/目录上下文菜单
![other-setting](image/vscode-5.1.png)
6. 安装准备就绪
![ready](image/vscode-6.png)
7. 正在安装
![setuping](image/vscode-7.png)
8. 完成安装
![success](image/vscode-8.png)
## Settings
1. 设置

修改 `settings.json`
```json
{
    // 控制字体系列。默认为 Consolas, 'Courier New', monospace
    // 推荐等宽（monospace）字体：Source Code Pro, Menlo, SF Mono
    // 常见比较好用的字体： 'Helvetica Neue', Helvetica, 'PingFang SC', 'Hiragino Sans GB' , 'Fira Code Retina', 'DejaVu Sans Mono', Inconsolata-g,'PingFang Mono SC',
    "editor.fontFamily": "'SF Mono', Menlo, 'Microsoft Yahei UI', '微软雅黑', Consolas, 'Courier New', monospace",
    //设置主题样式 One Dark Pro Vivid ，One Dark Pro
    "workbench.colorTheme": "One Dark Pro",
    // 图标主题
    "workbench.iconTheme": "material-icon-theme",
    //设置字体，默认12
    "editor.fontSize": 15,
    //设置自动保存，默认off
    "files.autoSave": "onFocusChange",
    "window.zoomLevel": 0,
    "diffEditor.ignoreTrimWhitespace": true,
    "diffEditor.renderIndicators": true,
    "diffEditor.renderSideBySide": true
    //解决内置终端字体间隔过大问题，修改默认“”值为等宽字体样式
    // "terminal.integrated.fontFamily": "Lucida Console",
    // "terminal.integrated.shell.windows": "C:\\WINDOWS\\System32\\cmd.exe",

    // "terminal.integrated.shell.windows": "D:\\Program Files\\Git\\bin\\bash.exe",
    // "workbench.colorCustomizations": {
    //     "statusBar.background": "#1A1A1A",
    //     "statusBar.noFolderBackground" : "#0A0A0D",
    //     "statusBar.debuggingBackground": "#511f1f"
    // }
}
```
  - 修改字体Fira Code
  
主页：https://github.com/tonsky/FiraCode 下载最新版本（2.0）字体压缩包，解压后找到ttf文件夹，将其中的全部文件复制到“`C:\Windows\Fonts`”文件夹中。包括：`FiraCode-Bold.ttf`, `FiraCode-Light.ttf`, `FiraCode-Medium.ttf`, `FiraCode-Regular.ttf`, `FiraCode-Retina.ttf`
    字体名称：`Fira Code`, `Fira Code Retina`,
  - 修改字体Source Code Pro 主页：https://github.com/adobe/Source-Code-Pro / https://github.com/adobe-fonts/source-code-pro
  - 修改字体Dejavu Sans Mono 主页：https://github.com/dejavu-fonts/dejavu-fonts
  - 修改字体Menlo、Monaco https://github.com/ueaner/fonts
  - 中文语言环境设置：

    操作步骤：快捷键`Ctrl + Shift + P` -> `Configure Display Language` ( `配置显示语言`) -> `en` 改为 `zh-CN` -> 保存 `locale.json` -> 扩展中搜索出品自Microsoft的 `Chinese (Simplified) Language Pack for Visual Studio Code` -->安装扩展->重启VSCode

 修改 `locale.json`
```json
{
    "locale":"zh-CN"
}
```

2. 安装插件
    - Dracule Official （Dracula Theme）：主题包（可选安装）
    - One Dark Pro （binaryify）：主题包（可选安装）
    - HTML CSS Support （ecmel）：智能提示
    - ESLint （Dirk Baeumer）：代码检测工具
    - Chinese (Simplified) Language Pack for Visual Studio Code （Microsoft）：简体中文语言包
    - Vetur（Pine Wu）：vue.js 高亮插件（vue开发必选）
    - Auto Close Tag(Jun Han): 自动关闭标签
    - Auto Rename Tag(Jun Han): 自动重命名标签
    - IntelliSense for CSS class names in HTML(Zignd)：自动提示
    - Material Icon Theme(Philipp Kief): 图标主题

3. KeyMap
 - Ctrl + ` : 打开/关闭 终端    
## Resource