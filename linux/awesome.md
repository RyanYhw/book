# Linux awesome

## 使用过的命令

查看网络状态
```
netstat -n | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}'
ss -a | awk '/^tcp/ {++S[$2]} END {for(a in S) print a, S[a]}'
```

thrift 文件夹的批量处理

```
ls -l | grep -v ^d |awk '{cmd = "thrift --gen go "$9; system(cmd)}'
```