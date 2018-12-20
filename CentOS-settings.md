# CentOS 7 Settings 
## Keymap

## 常用指令
- 开关机指令
```tcl
shutdown -h now #立刻关机
shutdown -h 10 #将于10分钟后关闭，且会显示在登录用户的当前屏幕中
shutdown -h 22:22 #将于指定时刻关机
shutdown -r now #立刻重启
shutdown -r +10 #将于10分钟后重启
reboot #重启
halt #关机
init 0
init 6
```
- 服务指令
```
```
## IP and DNS
1. 查看IP分配情况
```tcl
CentOS最小化安装 没有ifconfig命令。
# ifconfig 
# ip addr
```
2. 编辑ifcfg-ens33
```tcl
# cd /etc/sysconfig/network-scripts
# vi /etc/sysconfig/network-scripts/ifcfg-ens33
```
i 进入编辑模式，编辑后按Esc键，输入:wq 保存并退出
```powershell
BOOTPROTO=static        # dhcp -> static
ONBOOT=yes              # no -> yes，开机启用本配置，一般在最后一行
IPADDR=10.10.6.128      # 新增，静态IP
GATEWAY=10.10.6.1       # 新增，默认网关
NETMASK=255.255.255.0   # 新增，子网掩码
NM_CONTROLLED=no        # 新增，该接口通过配置文件进行设置，而不是通过网络管理器进行管理
DNS1=223.5.5.5          # 新增，DNS配置
DNS2=202.98.0.68
```


3. 重启网络服务
```tcl
# service network restart
# systemctl restart network.service
```
4. 验证网络配置

```tcl
# ping www.baidu.com
# ping -c 10 www.baidu.com
```
- ping -c N URL 表示ping N次后自动结束，其中N为正整数
- ctrl + C 退出ping命令