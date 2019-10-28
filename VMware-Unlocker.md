# MacOS Unlocker of VMware Workstation Pro

## Introduce

- [VMware Workstation Pro 15.5.0](https://download3.vmware.com/software/wkst/file/VMware-workstation-full-15.5.0-14665864.exe)
- [Unlocker 3.0.2](https://github.com/DrDonk/unlocker)

## Install
- 安装VMware Workstation Pro 15.5.0
- 安装MacOS补丁Unlocker。
  - 打开windows任务管理器，在服务里停止掉以VM开头的全部进程
  - 解压Unlocker文件
  - 以管理员身份运行win-install.cmd脚本文件（最好退出杀毒软件）。运行解锁补丁的同时会自动下载darwin.iso
  ```
  若下载失败可以手动下载. http://softwareupdate.vmware.com/cds/vmw-desktop/fusion/
  在最新的目录下packages里下载com.vmware.fusion.tools.darwin.zip.tar解压, 再把darwin.iso文件复制到VMware的安装目录里面.

  目前最新的版本为: http://softwareupdate.vmware.com/cds/vmw-desktop/fusion/11.0.2/10952296/packages/com.vmware.fusion.tools.darwin.zip.tar
  ```
- 解锁完成后运行VMware Workstation 虚拟机，选择新建虚拟机，操作步骤如下：
  ```
  创建新的虚拟机 >> 典型（推荐）>> 稍后安装操作系统 >> 选择Apple Mac OS X(M) >> 选择合适的版本
  ```