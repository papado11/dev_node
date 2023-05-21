# docker network

## 网络模式

bridge :桥接docker(默认)  
none:不配置网络  
host :和宿主机共享网络  
container :容器网络连通!(用的少!局限很大。)  


```shell
docker network ls # 查看所有的docker网络

# 默认情况下启动一个容器 都会使用bridge网络
docker run -d -P --name backend --net bridge backend

# 自定义一个网络 mynet
docker network create
    --driver bridge # (默认是bridge)
    --subnet 192.168.0.0/16 # (子网)
    --gateway 192.168.0.1  # (出口网关)
    mynet
```

## 网络联通

```shell
docker network connect 
```