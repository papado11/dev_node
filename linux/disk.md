# disk

## 查看硬盘状态

```shell
df -h

# 单个目录
df -h /usr

# 具体文件夹
du --max-depth=1 -h
du --max-depth=1 -h /usr

# 计算文件夹大小
du -sh /usr
```

```shell
# $lsblk lsblk -f #查看硬盘状态 
$fdisk /dev/sdb 分区命令  ## 硬盘文件
```
