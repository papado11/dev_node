# Apt

## 常用命令

```shell
apt list --installed ## 系统上安装的所有软件包

apt remove softname

apt remove --purge softname # 包含配置文件
```
## apt 代理

新建文件  
/etc/apt/apt.conf.d/proxy.conf  
配置其中一行即可

```conf
Acquire::http::Proxy "http://init@PassW0rd321#@192.168.56.102:3128/";
Acquire::https::Proxy "http://init@PassW0rd321#@192.168.56.102:3128/";
```