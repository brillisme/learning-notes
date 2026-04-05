# Linux 系统性能排查常用指令
## CPU 排查
- `top`：实时进程、CPU 负载、使用率监控
- `htop`：美化版进程管理，支持多核查看
- `uptime`：查看 1/5/15 分钟系统平均负载
- `mpstat -P ALL 1`：查看所有 CPU 核心使用情况
- `pidstat -u 1`：按进程实时统计 CPU 占用
- `vmstat 1`：CPU 上下文切换、中断、IO 等待
- `iostat -c 1`：单独查看 CPU 统计信息
- `sar -u 1`：系统级 CPU 使用率趋势统计
- `ps -eo pid,ppid,pcpu,cmd | sort -k 3 -r`：按 CPU 占用降序排列进程
- `strace -p PID`：追踪进程系统调用，排查 CPU 异常消耗

## 内存排查
- `free -h`：内存总览、空闲、缓存、Swap 使用
- `free -mh`：人性化显示内存使用
- `cat /proc/meminfo`：详细内存内核信息
- `vmstat 1`：虚拟内存、交换分区使用情况
- `sar -r 1`：内存使用率实时统计
- `ps aux --sort=-%mem`：按内存占用从高到低排序
- `top`：shift+M 按内存排序
- `pidstat -r 1`：进程级内存使用统计
- `swapon -s`：查看 Swap 分区使用状态
- `slabtop`：查看内核 slab 内存占用
- `pmap -x PID`：查看进程内存映射详情

## 磁盘 IO & 空间排查
- `df -h`：磁盘分区使用率
- `df -i`：inode 使用情况
- `du -sh *`：目录大小统计
- `du -ah --max-depth=1`：一级目录大小详情
- `iostat 1`：磁盘 IO、吞吐量、%util 使用率
- `iostat -x 1`：扩展 IO 统计（await、svctm）
- `iotop`：实时进程级磁盘 IO 监控
- `pidstat -d 1`：按进程查看磁盘 IO
- `sar -d 1`：磁盘设备 IO 统计
- `dmesg | grep -i error`：磁盘硬件/IO 错误
- `lsblk`：块设备信息查看
- `fdisk -l`：磁盘分区信息
- `fstrim -av`：SSD Trim 优化（不影响排查）

## 网络排查
- `ss -lntup`：查看监听端口与对应进程
- `ss -s`：网络连接统计
- `netstat -antp`：TCP/UDP 连接、端口、进程
- `ip addr`：网卡 IP 信息
- `ip link`：网卡状态
- `sar -n DEV 1`：网卡流量收发包统计
- `sar -n TCP 1`：TCP 连接、重传、半连接状态
- `ifstat`：实时网卡带宽监控
- `ethtool eth0`：查看网卡速率、模式
- `tcpdump -i any port 80`：端口抓包
- `nslookup / dig`：DNS 解析排查
- `ping / mtr`：网络连通性与链路质量
- `traceroute`：路由追踪
- `ss -ti`：查看 TCP 拥塞、重传信息
- `conntrack -L`：连接跟踪表查看

## 进程 & 系统 & 日志排查
- `ps aux`：全量进程信息
- `ps -efH`：进程树查看
- `lsof -p PID`：进程打开文件、端口
- `lsof -i:端口`：查看占用指定端口的程序
- `lsof /var/log/*`：查看文件被哪些进程占用
- `dmesg -T`：带时间内核日志
- `journalctl -xe`：系统最新日志
- `journalctl -u nginx`：查看指定服务日志
- `journalctl -f`：实时滚动日志
- `uptime`：系统运行时间、负载
- `w`：当前登录用户与系统负载
- `who`：登录用户查看
- `last`：登录历史
- `kill -9 PID`：强制结束进程
- `systemctl status 服务名`：服务状态、启动异常
- `pstree`：进程父子关系树
- `numastat`：NUMA 架构内存分布查看
