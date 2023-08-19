# disk

## 查看硬盘状态

```shell
df -h

# 单个目录
df -h /usr

# 具体文件夹 -- 查看各文件夹大小
du --max-depth=1 -h
du --max-depth=1 -h /usr

# 计算文件夹大小
du -sh /usr
```

## 添加硬盘

```shell
# 查看新加入的硬盘 sd[b,c,d,f,] 通常是sdb
fdisk -l
# 分区命令 添加一个分区
fdisk /dev/sdb ## 硬盘文件
# 分区以后会多出个 /dev/sdb1

# 格式化磁盘 注意要格式化的硬盘分区
mkfs.ext4 /dev/sdb1


# 创建挂载目录 名称随意
mkdir /b
# 挂载
mount /dev/sdb1 /b

# 设置新硬盘开机自动挂载
vim /etc/fstab
添加以下信息
/dev/sdb1               /DataCenter2            ext3    defaults        1 2
```
