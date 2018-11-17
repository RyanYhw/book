# DOCKER

## ISSUE

### docker 中无法输入中文解决

```
# 创建容器的时候
# docker run 增加
env LANG=C.UTF-8
```

```
# 创建镜像
# Dockerfile

ENV LANG=C.UTF-8
```

```
# 容器如果已经存在
docker exec -it CONTAINER env LANG=C.UTF-8 bash
```
