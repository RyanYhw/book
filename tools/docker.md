# docker

## 问题

### docker 中无法输入中文解决

docker 创建容器的时候增加如下选项

```
env LANG=C.UTF-8
```

docker 创建镜像的时候

```
Dockerfile

ENV LANG=C.UTF-8
```

docker 启动已经存在的容器的时候

```
docker exec -it CONTAINER env LANG=C.UTF-8 bash
```
