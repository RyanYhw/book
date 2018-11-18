# system

## 资源

### 修改系统支持的最大文件句柄数

```
/proc/sys/fs/file-max 
如 echo 2000000 > /proc/sys/fs/file-max
```

### 修改当前进程的最大文件句柄数

```
可以修改 
/etc/security/limits.conf
    soft nofile
    hard nofile
```

### 设置线程栈

```
pthread_attr_init
```

### 设置线程数

```
/proc/sys/kernel/threads-max
```


### 其他内核参数

```
/etc/sysctl.conf
/sbin/sysctl -p 生效
# 有些参数需要根据系统的实际情况设置，不可以认为是固化的值

# 允许将TIME_WAIT状态的socket重新用于新的TCP链接
net.ipv4.tcp_tw_reuse = 1

# 当keepalive启动时，TCP发送keepalive消息的频度；默认是2小时，将其设置为10分钟
ner.ipv4.tcp_keepalive_time = 600

# 当服务器主动关闭链接时，socket保持在FIN_WAIT_2状态的最大时间
net.ipv4.tcp_fin_timeout = 30

# 这个参数表示操作系统允许TIME_WAIT套接字数量的最大值，如果超过这个数字，TIME_WAIT套接字将立刻被清除并打印警告信息。
net.ipv4.tcp_max_tw_buckets = 5000

# 定义UDP和TCP链接的本地端口的取值范围。
net.ipv4.ip_local_port_range = 1024 65000

# 定义了TCP接受缓存的最小值、默认值、最大值。
net.ipv4.tcp_rmem = 10240 87380 12582912

# 定义TCP发送缓存的最小值、默认值、最大值。
net.ipv4.tcp_wmem = 10240 87380 12582912

# 当网卡接收数据包的速度大于内核处理速度时，会有一个列队保存这些数据包。这个参数表示该列队的最大值。
net.core.netdev_max_backlog = 8096

#表示内核套接字接受缓存区默认大小。
net.core.rmem_default = 6291456

#表示内核套接字发送缓存区默认大小。
net.core.wmem_default = 6291456

#表示内核套接字接受缓存区最大大小。
net.core.rmem_max = 12582912

# 表示内核套接字发送缓存区最大大小。
net.core.wmem_max = 12582912

# 用于解决TCP的SYN攻击。
net.ipv4.tcp_syncookies = 1

# 这个参数表示TCP三次握手建立阶段接受SYN请求列队的最大长度，默认1024,
# 将其设置的大一些可以使出现Nginx繁忙来不及accept新连接的情况时，Linux不至于丢失客户端发起的链接请求。
net.ipv4.tcp_max_syn_backlog = 8192

# 这个参数用于设置启用timewait快速回收。线上环境不建议使用，尤其是在有NAT环境下
# 如果发现客户端带时间戳的包无法建立连接的话，考虑是否开启了这个选项
# net.ipv4.tcp_tw_recycle = 1

# 这个参数用于调节系统同时发起的TCP连接数(每个端口)，默认128，在高并发的请求中，
# 默认的值可能会导致链接超时或者重传，因此需要结合高并发请求数来调节此值。
net.core.somaxconn=8196

# This limit exists only to prevent simple DoS attacks,
# you _must_ not rely on this oｒ lower the limit artificially,
# but rather increase it (probably, after increasing installed memory),
# if network conditions require more than default value,
# anｄ tune network services to linger anｄ kill such states more aggressively.

net.ipv4.tcp_max_orphans=262114

```

## interupts

```
cat /proc/interrupts

	   CPU0       CPU1
  0: 1366814704          0          XT-PIC  timer
  1:        128        340    IO-APIC-edge  keyboard
  2:          0          0          XT-PIC  cascade
  8:          0          1    IO-APIC-edge  rtc
 12:       5323       5793    IO-APIC-edge  PS/2 Mouse
 13:          1          0          XT-PIC  fpu
 16:   11184294   15940594   IO-APIC-level  Intel EtherExpress Pro 10/100 Ethernet
 20:    8450043   11120093   IO-APIC-level  megaraid
 30:      10432      10722   IO-APIC-level  aic7xxx
 31:         23         22   IO-APIC-level  aic7xxx
NMI:          0
ERR:          0
```

The first column refers to the IRQ number.  (逻辑中断号)
Each CPU in the system has its own column and its own number of interrupts per IRQ.  
The next column reports the type of interrupt.  
The last column contains the name of the device that is located at that IRQ.  

根据IRQ可以查看CPU亲和性

```
cat /proc/irq/{IRQ}/smp_affinity_list
```

查看软中断

```
cat /proc/softirqs
```

## NIC

1. 查看网卡信息, 确认网卡信息，确认bus-info

```
ethtool -i eth0
```

2. 确认网卡是否支持多网卡

```
1. lspci -vvv

如果网卡信息中包含 MSI-X，即支持多网卡队列

2. 查看lspci与实际网卡对应关系

/sys/devices/ 目录下搜索网卡名称，比如eth0，找到网卡对应的PCI总线位置, 例如 00:18.7, 然后 'lspci -vvv -s 00:18.7'获取设备信息
```

3. 查看具体的网卡是多少队列

```
ll /sys/class/net/eth0/queues
```

4. 中断绑定

修改
```
/proc/irq/{IRQ}/smp_affinity
位为1表示CPU可以被中断
```