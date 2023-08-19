# 清理docker

```shell
# docker 占用的空间
docker system df
# 清理无用镜像、缓存、挂载数据
docker system prune -a


# 创建清理docker日志的脚本
vim docker_clean.sh

#!/bin/bash
echo "======== start clean docker containers logs ========"
logs=$(find /var/lib/docker/containers/ -name *-json.log)
for log in $logs
        do
                echo "clean logs : $log"
                cat /dev/null > $log
        done
echo "======== end clean docker containers logs ========"

# 执行
./docker_clean.sh
```