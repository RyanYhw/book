# tools

## mpstat

```
%user：表示处理用户进程所使用CPU的百分比。用户进程是用于应用程序（如Oracle数据库）的非内核进程；            
%nice：表示使用nice命令对进程进行降级时CPU的百分比；  
%sys：表示内核进程使用的CPU百分比；
%iowait：表示等待进行I/O所使用的CPU时间百分比；
%irq：表示用于处理系统中断的CPU百分比；
%soft：表示用于软件中断的CPU百分比；
%steal ：显示虚拟机管理器在服务另一个虚拟处理器时虚拟CPU处在非自愿等待下花费时间的百分比
%guest ：显示运行虚拟处理器时CPU花费时间的百分比
%idle：显示CPU的空闲时间；
%intr/s：显示每秒CPU接收的中断总数；

mpstat -P ALL 2
```

## ss

