# docker

## Repositories

### busybox

BusyBox 是一个集成了三百多个最常用Linux命令和工具的软件。BusyBox 包含了一些简单的工具，例如ls、cat和echo等等，还包含了一些更大、更复杂的工具，例grep、find、mount以及telnet。有些人将 BusyBox 称为 Linux 工具里的瑞士军刀。简单的说BusyBox就好像是个大工具箱，它集成压缩了 Linux 的许多工具和命令，也包含了 Android 系统的自带的shell。

[busybox](https://busybox.net/)

```
docker run -it --rm busybox sh -c 'echo world | nc docker.for.mac.localhost 9000'
```

### owner

### centos 7 dev

```
# gcc version 4.8.5 20150623 (Red Hat 4.8.5-28) (GCC)
# cmake-3.12.4
# libevent-2.1.8-stable
# boost_1_68_0
docker pull eagle042/centos7
```
