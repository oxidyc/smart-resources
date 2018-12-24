# CentOS 7 Settings 
## Keymap

## 常用指令
- 默认命令前缀
```
[root@loaclhost ~]#
[root@centos ~]#
```
- 开关机指令
```tcl
shutdown -h now     #立刻关机
shutdown -h 10      #将于10分钟后关闭，且会显示在登录用户的当前屏幕中
shutdown -h 22:22   #将于指定时刻关机
shutdown -r now     #立刻重启
shutdown -r +10     #将于10分钟后重启
reboot              #直接重启
halt                #关机
poweroff            #系统关机
init 0
init 6
```
- 服务指令
```
# 防火墙
systemctl stop firewalld.service #停止firewall
systemctl disable firewalld.service #禁止firewall开机启动
```
- vi编辑
```tcl
vi <filepath> # 打开文件
- 按i键，进入insert模式，进入insert模式后才能修改文件
- 修改完成后，按esc键进入command模式，
- 然后 `:wq` 保存文件并退出vi 

:w      保存文件但不退出vi
:w file 将修改另外保存到file中，不退出vi
:w!     强制保存，不退出vi
:wq     保存文件并退出vi
:wq!    强制保存文件，并退出vi
q:      不保存文件，退出vi
:q!     不保存文件，强制退出vi
:e!     放弃所有修改，从上次保存文件开始再编辑
```
## IP and DNS
`CentOS默认安装后未自动开启网络连接`
1. 查看IP分配情况
```tcl
# CentOS最小化安装 没有ifconfig命令。
$ ifconfig 
$ ip addr
```
2. 编辑ifcfg-ens33
```tcl
$ cd /etc/sysconfig/network-scripts
$ vi /etc/sysconfig/network-scripts/ifcfg-ens33
```
点击 `i` 进入编辑模式，编辑后按 `Esc` 键，输入 `:wq` 保存并退出
```powershell
BOOTPROTO=static        # dhcp -> static，启用静态IP地址
ONBOOT=yes              # no -> yes，开机自动启用网络连接，一般在最后一行
IPADDR=10.10.6.128      # 新增，静态IP
GATEWAY=10.10.6.1       # 新增，默认网关
NETMASK=255.255.255.0   # 新增，子网掩码
NM_CONTROLLED=no        # 新增，该接口通过配置文件进行设置，而不是通过网络管理器进行管理
DNS1=223.5.5.5          # 新增，DNS配置
DNS2=202.98.0.68
```


3. 重启网络服务
```tcl
$ service network restart
$ systemctl restart network.service
```
4. 验证网络配置

```tcl
$ ping www.baidu.com
$ ping -c 10 www.baidu.com
```
- ping -c N URL 表示ping N次后自动结束，其中N为正整数
- ctrl + C 退出ping命令

5. 设置主机名为www
```tcl
$ hostnamectl status [--static|--transient|--pretty] # 查看主机名相关的设置
$ hostnamectl --static set-hostname <host-name>
$ hostnamectl set-hostname www    # 使用此命令会立即生效且重启也生效
$ hostname                        # 查看当前的hostname,默认为localhost.localdomain
$ vi /etc/hostname                # 编辑hostname文件
localhost.localdomain

$ vi /etc/hosts                   # 编辑hosts文件，给127.0.0.1添加hostname
127.0.0.1 localhost localhost.localdomain localhost4 loaclhost4.loacldomain4 www
::1       localhost localhost.localdomain localhost4 loaclhost4.loacldomain4

$ cat /etc/hosts                  # 检查
```