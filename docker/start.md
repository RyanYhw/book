# docker

## list images

```
# 所有镜像
docker image ls
```

```
# 所有容器
docker container ls --all
```

## Dockerfile

[完整事例](https://docs.docker.com/get-started/part2/#apppy)

创建一个新的文件夹，创建一个新的Docerfile

```
# Use an official Python runtime as a parent image
FROM python:2.7-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

创建新的image
```
# 在 Dockerfile 目录里执行
# -t 打标签
# image为 friendlyhello:latest
docker build -t friendlyhello .

```

Proxy server settings
```
# Set proxy server, replace host:port with values for your servers
ENV http_proxy host:port
ENV https_proxy host:port
```

DNS settings

```
# 在本机设置 DNS，并让docker 生效
# /etc/docker/daemon.json
# sudo service docker restart
{
  "dns": ["your_dns_address", "8.8.8.8"]
}
```

## run app

```
# -p 将本机的4000映射到容器的80端口
docker run -p 4000:80 friendlyhello
```

```
# 后台运行
docker run -d -p 4000:80 friendlyhello
```

```
# 终止容器
docker container stop ${CONTAINER ID}
```

## Log in with your Docker ID

```
docker login
```

## tag images

```
docker tag ${image} ${username/repository:tag}

# 例子
docker tag friendlyhello gordon/get-started:part2
```

## publish the image

```
docker push username/repository:tag
```

## services

docker-compose.yml

```
version: "3"
services:
  web:                         # 服务名字
    # replace username/repo:tag with your name and image details
    image: username/repo:tag   # 镜像名字，使用该镜像打容器
    deploy:
      replicas: 5              # 5 个实例
      resources:
        limits:
          cpus: "0.1"          # 10% cpu, 50MB RAM
          memory: 50M
      restart_policy:
        condition: on-failure  # 如果失败了立马重启
    ports:
      - "4000:80"              # 端口映射
    networks:
      - webnet                 # 使用webnet共享80端口
networks:
  webnet:                      # webnet 为默认设置
```
This docker-compose.yml file tells Docker to do the following:

* Pull the image we uploaded in step 2 from the registry.

* Run 5 instances of that image as a service called web, limiting each one to use, at most, 10% of the CPU (across all cores), and 50MB of RAM.

* Immediately restart containers if one fails.

* Map port 4000 on the host to web’s port 80.

* Instruct web’s containers to share port 80 via a load-balanced network called webnet. (Internally, the containers themselves publish to web’s port 80 at an ephemeral port.)

* Define the webnet network with the default settings (which is a load-balanced overlay network).



## Run your new load-balanced app

```
# 1 先执行
docker swarm init
```

```
# 2 getstartedlab 为自定义的app名字
docker stack deploy -c docker-compose.yml getstartedlab
```

```
# 3 查看
docker service ls
```

```
# 4 查看对应的task
# getstartedlab为#2起的名字，web为yaml文件指定的名字
docker service ps getstartedlab_web 

docker container ls -q  # 也可以看到
```

## Scale the app

修改 docker-compose.yml 文件 replicas, 然后重启

```
# 重新执行
docker stack deploy -c docker-compose.yml getstartedlab

# 事例，如果改成1
# docker service ps getstartedlab_web
ty7887rdpl1f        getstartedlab_web.1   gordon/get-started:part2   linuxkit-025000000001   Running             Running 6 minutes ago                       
qydrkupiiswt        getstartedlab_web.2   gordon/get-started:part2   linuxkit-025000000001   Remove              Running 5 seconds ago                       
dzo6129j6n2a        getstartedlab_web.3   gordon/get-started:part2   linuxkit-025000000001   Remove              Running 5 seconds ago                       
pfdqdtuahs6r        getstartedlab_web.4   gordon/get-started:part2   linuxkit-025000000001   Remove              Running 5 seconds ago                       
scat65cjnfr9        getstartedlab_web.5   gordon/get-started:part2   linuxkit-025000000001   Remove              Running 5 seconds ago

```

## take the app down

```
docker stack rm ${getstartedlab}
```

```
# Take down the swarm.
docker swarm leave --force
```

## Swarms


## 任务说明

以下如果没有的，则写略

###功能说明
    说明 或者 文档

### 设计说明
    针对功能的设计说明 或者文档 （总）

### 流程说明（算法说明）
    针对设计的算法说明 

### 第三方库使用说明
    （使用了哪些库，哪些功能）
### 单元测试用例，单元测试用例结果
    代码位置，结果说明

### 服务测试时所记录的日志
    文件或者说明

### 需要提交编译说明，部署说明
    说明或者文档

### bug 
    bug 说明
    bug 解析
