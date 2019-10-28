# CentOS 6 Settings


1. 查看版本
```
[root@localhost ~]# cat /etc/issue  
CentOS release 6.2 (Final)
```

2. 服务状态查询
```
[root@localhost ~]# service --status-all
```

3. 服务状态 启动/重新启动/状态查看/停止
```
[root@localhost ~]# service nginx start/restart/status/stop
```

4. 查询MySQL安装路径
```tcl
[root@localhost ~]# whereis mysql
```

5. 防火墙开放3306端口
```tcl
# 打开防火墙配置文件
vi /etc/sysconfig/iptables

# 增加一行
-A INPUT -m state --state NEW -m tcp -p tcp --dport 3306 -j ACCEPT

# 保存后重启防火墙
service iptables restart
```

6. curl会显示出源码
```tcl
curl http://www.baidu.com/index.html
```