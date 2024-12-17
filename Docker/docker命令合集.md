# docker 命令合集

## 安装

```shell
# centos7 为例
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo systemctl start docker
```

## 基本命令

### 1.docker --help

> **凡是对命令不知道怎么用的，多用--help查看**
>
> 查看帮助文档
>
> docker pull --help   查看docker pull 命令的使用

### 2.docker system df

> Show docker disk usage

## 镜像命令

### 1.docker search 

> 搜索镜像

### 2.docker pull 

> 拉取镜像

### 3.docker images 

> 列出本地镜像

### 4.docker rmi

> 删除镜像  可根据镜像名称或者id进行删除
>
> 删除全部：docker rmi -f $(docker images -aq)

## 容器命令

### 1.docker run image

> 新建+启动容器
>
> docker run -it redis 
>
> -i, --interactive                      Keep STDIN open even if not attached
>
> -t, --tty                                    Allocate a pseudo-TTY

### 2.docker ps 

> 列出启动的容器
>
> -a, --all             Show all containers (default shows just running)

### 3.退出

> exit  run进去的容器，exit退出，容器停止
>
> ctrl+p+q run进去的容器，ctrl+p+q退出，容器不停止

### 4.docker start container_id

> 启动容器

### 5.docker restart container_id

> 重启容器

### 6.docker stop container_id

> 停止容器

### 7.docker rm container_id

> 删除容器

### 8.docker logs container_id

> 查看容器日志

### 9.docker top container_id

> 查看容器内运行的进程

### 10.docker inspect container_id

> 查看容器内部细节

### 11.docker cp 

> Usage:  
>
> ​	docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
> ​	docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH
>
> Copy files/folders between a container and the local filesystem

### 12.docker exprt

> 导出
>
> docker export 35744fad8059 > /data/redis.tar.gz

### 13.docker import

> cat redis.tar.gz | docker import - dms/redis:3.0



