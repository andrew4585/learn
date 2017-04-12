## iptraf
#### overview
iptraf命令可以实时地监视网卡流量，可以生成网络协议数据包信息、以太网信息、网络节点状态和ip校验和错误等信息

#### 安装

* centos

yum install iptraf -y

#### 语法
> iptraf(选项)

#### 选项
```
-i  网络接口：立即在指定网络接口上开启IP流量监视；

-g  立即开始生成网络接口的概要状态信息；

-d  网络接口：在指定网络接口上立即开始监视明细的网络流量信息；

-s  网络接口：在指定网络接口上立即开始监视TCP和UDP网络流量信息；

-z  网络接口：在指定网络接口上显示包计数；

-l  网络接口：在指定网络接口上立即开始监视局域网工作站信息；

-t  时间：指定iptraf指令监视的时间；

-B  将标注输出重新定向到“/dev/null”，关闭标注输入，将程序作为后台进程运行；

-f  清空所有计数器；

-h  显示帮助信息。
```

```
Syntax:
    iptraf [ -f ] [ { -i iface | -g | -d iface | -s iface | -z iface |
           -l iface } [ -t timeout ] [ -B ] [ -L logfile ] [-I interval] ]

Issue the iptraf command with no parameters for menu-driven operation.
These options can also be supplied to the command:

-i iface    - start the IP traffic monitor (use "-i all" for all interfaces)
-g          - start the general interface statistics
-d iface    - start the detailed statistics facility on an interface
-s iface    - start the TCP and UDP monitor on an interface
-z iface    - shows the packet size counts on an interface
-l iface    - start the LAN station monitor ("-l all" for all LAN interfaces)
-B          - run in background (use only with one of the above parameters)
-t timeout  - when used with one of the above parameters, tells
              the facility to run only for the specified number of
              minutes (timeout)
-L logfile  - specifies an alternate log file for any direct invocation
              of a facility from the command line.  The log is placed in
              /var/log/iptraf if path is not specified.
-I interval - specifies the log interval for all facilities except the IP
              traffic monitor.  Value is in minutes.
-f          - clear all locks and counters.  Use with great caution.
              Normally used to recover from an abnormal termination.

```
