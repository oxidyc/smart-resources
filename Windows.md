# Windows Tips

## 远程桌面问题
Windows10 版本的远程桌面安装补丁后，出现身份验证错误，要求的函数不受支持，可能是由于CredSSP加密Oracle修正。
``` tcl
# 微软给出解决方案:
https://support.microsoft.com/zh-cn/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018

# 解决办法(一)组策略
专业版以上
Win+R运行 -> gpedit.msc -> 本地计算机策略 -> 计算机配置 -> 管理模板 -> 系统 -> 凭据分配 -> 加密Oracle修正
值修改 "未配置" -> "已启用"；保护级别: 已缓解

# 解决办法(二)注册表
家庭版
Win+R运行 -> regedit -> 依次打开路径
"计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\CredSSP\Parameters"
创建DWORD(32位)值 AllowEncryptionOracle = 2
然后重启
```