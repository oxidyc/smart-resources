# MongoDB for CentOS Tutorial

## Download

CentOS 需要选择RHEL 7.0 Linux 64-bit x64
https://repo.mongodb.org/yum/redhat/7/mongodb-org/4.0/x86_64/RPMS/mongodb-org-server-4.0.5-1.el7.x86_64.rpm

## Installation Steps
```tcl
# 安装curl、openssl
yum install libcurl openssl
# 下载rpm
curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-4.0.5.tgz
# 解压
tar -zxvf mongodb-linux-x86_64-4.0.5.tgz
```


- 启动MongoDB
```tcl
# 启动服务
systemctl start mongod.service
# 停止服务
systemctl stop mongod.service
# 查看状态
systemctl status mongod.service
# 重启服务
systemctl restart mongod.service
```