# CentOS  Tutorial

## Introduce
CentOS 是一个基于Red Hat Linux 提供的可自由使用源代码的企业级Linux发行版本。

Home:http://www.centos.org
## Download

ISO镜像下载地址：http://isoredirect.centos.org/centos/7/isos/x86_64/CentOS-7-x86_64-DVD-1810.iso
## Installation Steps
+ 1.选择安装语言
+ 2.选择安装时间DATE&TIME，设置为亚洲/上海
+ 3.选择系统安装位置INSTALLATION DESTINATION，配置分区
    + 3.1 配置/boot分区：500MB
    + 3.2 配置swap分区：2GB
    + 3.3 配置/(剩余空间）
+ 4.选择配置ip地址 NETWORK&HOSTNAME
+ 5.开始安装，编辑root密码
+ 6.完成安装

## Settings

## Keymap

#### 文件与目录操作
+ cd ..                    返回上一级目录
+ cd ../..                 返回上两级目录
+ cp file1 file2           将file1复制为file2
+ cp -a dir1 dir2          复制一个目录
+ cp -a /tmp/dir1 .        复制一个目录到当前工作目录（.代表当前目录）
+ ls                       查看目录中的文件
+ ls -a                    显示隐藏文件
+ pwd                      显示工作路径
+ mkdir dir1               创建文件夹
+ mkdir -p /tmp/dir1/dir2  创建一个目录树
+ mv dir1 dir2             移动/重命名一个目录
+ rm -f file1              删除 ‘file1’
+ rm -rf dir1              删除 ‘dir1’ 目录及其子目录内容

#### 查看文件内容
+ cat file1                从第一个字节开始正向查看文件的内容
+ head -2 file1            查看一个文件的前两行
#### 文本内容处理
+ grep str /tmp/test       在文件 ‘/tmp/test’ 中查找 “str”
+ grep ^str /tmp/test      在文件 ‘/tmp/test’ 中查找以 “str” 开始的行
+ diff file1 file2         找出两个文件的不同处
+ vi file                  编辑文件
    + i     	进入编辑文本模式
    + Esc       退出编辑文本模式
    + :w        保存当前修改
    + :q        不保存退出vi
    + :wq       保存当前修改并退出vi
#### 压缩、解压
+ bzip2 file1               压缩 file1
+ bunzip2 file1.bz2         解压 file1.bz2
+ unzip file1.zip           解压一个zip格式的压缩包到当前目录
+ unzip test.zip -d /tmp/   解压一个zip格式的压缩包到 /tmp 目录
#### 系统相关
+ shutdown -h now           关机
+ shutdown -r now           重启

## Rources
+ https://www.osyunwei.com/archives/7829.html
