# 网络监控ss

```shell
Usage:ss [OPTIONS]ss [OPTIONS][FILTER]-h,--help
    -V,--version       output version information
    -n,--numeric       don't resolve service names # 不解析服务名称
    -r,--resolve       resolve host names # 不解析主机名
    -a,--all           display all sockets # 显示所有的 sockets
    -l,--listening     display listening sockets # 显示监听的 sockets
    -o,--options       show timer information # 显示定时器信息
    -e,--extended      show detailed socket information # 显示详细的 socket 信息
    -m,--memory        show socket memory usage # 显示内存的使用情况
    -p,--processes     show process using socket # 显示使用套接字的进程
    -i,--info          show internal TCPinformation # 显示 tcp 内部信息
    -s,--summary       show socket usage summary # 显示套接字（socket）使用概况
    -b,--bpf           show bpf filter socket information
    -E,--events        continually display sockets asthey are destroyed
    -Z,--context       display process SELinux security contexts
    -z,--contexts      display process and socket SELinux security contexts
    -N,--net           switchto the specified network namespace name
    -4,--ipv4          display only IPversion 4sockets # 仅显示 IPv4 的套接字
    -6,--ipv6          display only IPversion 6sockets # 仅显示 IPv6 的套接字
    -0,--packet        display PACKETsockets # 显示 PACKET套接字
    -t,--tcp           display only TCPsockets # 仅显示 TCP套接字
    -S,--sctp          display only SCTPsockets # 仅显示 SCTP套接字
    -u,--udp           display only UDPsockets # 仅显示  UDP套接字
    -d,--dccp          display only DCCPsockets # 仅显示 DCCP套接字
    -w,--raw           display only RAWsockets # 仅显示  RAW套接字
    -x,--unix          display only Unix domain sockets # 仅显示 Unix 套接字
        --vsock         display only vsock sockets
    -f,--family=FAMILYdisplay sockets oftype FAMILYFAMILY:={inet|inet6|link|unix|netlink|vsock|help}# 显示 FAMILY类型的套接字，FAMILY可选  Unix， inet,inet6,link ,netlink
    -K,--kill          forcibly close sockets,display what was closed
    -H,--no-header     Suppress header line
    -A,--query=QUERY,--socket=QUERYQUERY:={all|inet|tcp|udp|raw|unix|unix_dgram|unix_stream|unix_seqpacket|packet|netlink|vsock_stream|vsock_dgram}[,QUERY]-D,--diag=FILEDump raw information about TCPsockets to FILE-F,--filter=FILEread filter information fromFILE# 从文件中都去过滤信息
       FILTER:=[state STATE-FILTER][EXPRESSION]STATE-FILTER:={all|connected|synchronized|bucket|big|TCP-STATES}TCP-STATES:={established|syn-sent|syn-recv|fin-wait-{1,2}|time-wait|closed|close-wait|last-ack|listen|closing}connected :={established|syn-sent|syn-recv|fin-wait-{1,2}|time-wait|close-wait|last-ack|closing}synchronized :={established|syn-recv|fin-wait-{1,2}|time-wait|close-wait|last-ack|closing}bucket :={syn-recv|time-wait}big :={established|syn-sent|fin-wait-{1,2}|closed|close-wait|last-ack|listen|closing}
```

## 操作步骤

### 1. 显示系统内的 TCP 连接

命令：ss -at

### 2. 显示 socket 摘要

命令：ss -s

### 3. 显示监听的 sockets

命令：ss -l

### 4. 显示进程使用的 sockets

命令：ss -lp

### 5. 显示所有 UDP 监听的 socket

命令：ss -au

### 6. 显示 dst IP 为 172.31.2.25 且状态为 established 的 TCP 连接，同时显示 timer

命令：ss -t -o state established dst 172.31.2.25

### 7. 显示 src IP 为 172.31.2.101 且状态为 established 的 TCP 连接，同时显示 timer

命令：ss -ato state established src 172.31.2.102  
state 可以参考以下：  
STATE-FILTER:={all|connected|synchronized|bucket|big|TCP-STATES}TCP-STATES:={established|syn-sent|syn-recv|fin-wait-{1,2}|time-wait|closed|close-wailast-ack|listen|closing}connected :={established|syn-sent|syn-recv|fin-wait-{1,2}|time-wait|close-wait|last-ack|closing}synchronized :={established|syn-recfin-wait-{1,2}|time-wait|
close-wait|last-ack|closing}bucket :={syn-recv|time-wait}big :={established|syn-sent|fin-wait-{1,2}|closed|close-wait|last-aclisten|closing}

### 8. 匹配远程地址和端口号

命令：ss dst 172.31.2.25:61895  
不指定端口号则匹配所有，查看本地的以此类推。

### 9. 显示所有 IPv4 监听在 TCP 端口的进程

命令： ss -a4tlp  
我们很方便的就能从结果中找到相关的有用信息，比如：pid，fd。
