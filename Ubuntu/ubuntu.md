# ubuntu 

## 一、软件安装

### Clash

> 科学上网工具

```shell
cd && mkdir clash
gunzip clash*.gz
mv clash-linux-amd64-v1.18.0 clash
wget -O config.yaml "https://linkuserssnk.xxyjx.cc/s/d6BYBbiNruV0jKNU?clash=1&log-level=info"
chmod +x clash
sudo ./clash -d .
```

* 用脚本启动

  ```shell
  sudo vim start.sh
    nohup ./clash -d . > clash.log 2>&1 &
  sudo chmod +x start.sh
  ```

* 添加为开机启动

  修改start.sh脚本内容，改为全路径 如下

  ```shell
  nohup /home/dongms/clash/clash -d /home/dongms/clash > 	/home/dongms/clash/clash.log 2>&1 &
  ```

​		配置到“启动应用程序中”

![](添加启动程序1.png)





![](添加启动程序2.png)



### Typora

>  markdown编辑器

```shell
sudo dpkg -i typora*.deb
```

### Chrome

```shell
sudo dpkg -i google-chrome-stable_current_amd64.deb
```

### vim

```shell
sudo apt update
sudo apt install vim
vim --version

```

### Docker

* https://docs.docker.com/engine/install/ubuntu/

  * 1. Set up Docker's `apt` repository.

  ```shell
  # Add Docker's official GPG key:
  sudo apt-get update
  sudo apt-get install ca-certificates curl
  sudo install -m 0755 -d /etc/apt/keyrings
  sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
  sudo chmod a+r /etc/apt/keyrings/docker.asc
  
  # Add the repository to Apt sources:
  echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
    $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  sudo apt-get update
  ```

  * 2. Install the Docker packages.

  ```shell
  sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
  ```

  * 3. Verify that the installation is successful by running the `hello-world` image:

    ```shell
    sudo docker run hello-world
    ```

 * 代理设置

   * 制定目录创建.conf文件

   ```shell
   sudo mkdir -p /etc/systemd/system/docker.service.d
   sudo touch /etc/systemd/system/docker.service.d/proxy.conf
   ```

   * proxy.conf文件内容

   ```shell
   [Service]
   Environment="HTTP_PROXY=http://127.0.0.1:7890/"
   Environment="HTTPS_PROXY=http://127.0.0.1:7890/"
   Environment="NO_PROXY=localhost,127.0.0.1,.example.com"
   ```

   * 重启

   ```shell
   sudo systemctl daemon-reload
   sudo systemctl restart docker
   ```

* docker-compose 

  * 1. To download and install the Docker Compose CLI plugin, run:

  ```shell
  mkdir -p /usr/local/lib/docker/cli-plugins
  curl -SL https://github.com/docker/compose/releases/download/v2.30.3/docker-compose-linux-x86_64 -o /usr/local/lib/docker/cli-plugins/docker-compose
  ```

  * 2. Apply executable permissions to the binary:

  ```shell
  sudo chmod +x /usr/local/lib/docker/cli-plugins/docker-compose
  ```

  * 3. check

  ```shell
  docker compose version
  ```

  

### Git

> 版本控制工具

* 1. 添加Git官方仓库

     ```shell
     sudo add-apt-repository ppa:git-core/ppa
     ```

* 2. 安装Git

     ```shell
     sudo apt update
     sudo apt install git
     git --version
     ```

* 用法

  * clone

    ```shell
    git clone https://github.com/BrightSt/note.git
    ```



### Snipaste

> 截图软件   
>
> 安装参考 ： https://blog.csdn.net/qq_44684757/article/details/136062578

```shell
1.下载
https://www.snipaste.com/download.html
2.添加可执行权限
sudo chmod +x Snipaste-2.10.3-x86_64.AppImage
3.执行
./Snipaste-2.10.3-x86_64.AppImage
```

* 启动后报错

  > dlopen(): error loading libfuse.so.2
  >
  > AppImages require FUSE to run. 
  > You might still be able to extract the contents of this AppImage 
  > if you run it with the --appimage-extract option. 
  > See https://github.com/AppImage/AppImageKit/wiki/FUSE 
  > for more information

  ```shell
  # 处理方式
  sudo add-apt-repository universe
  sudo apt update -y && sudo apt upgrade -y
  sudo apt install libfuse2 -y
  
  ！！！执行后如果不生效需要重启
  ```
  

### Nextcloud

> 自建云盘

```shell
sudo -i
mkdir -p /root/data/docker_data/aio-nextcloud
cd /root/data/docker_data/aio-nextcloud

vim docker-compose.yml
```

yaml文件的内容

```yaml
version: "3.8"

services:
  nextcloud-aio-mastercontainer:
    image: nextcloud/all-in-one:latest
    init: true
    restart: always
    container_name: nextcloud-aio-mastercontainer # This line is not allowed to be changed as otherwise AIO will not work correctly
    volumes:
      - nextcloud_aio_mastercontainer:/mnt/docker-aio-config # This line is not allowed to be changed as otherwise the built-in backup solution will not work
      - /var/run/docker.sock:/var/run/docker.sock:ro # May be changed on macOS, Windows or docker rootless. See the applicable documentation. If adjusting, don't forget to also set 'WATCHTOWER_DOCKER_SOCKET_PATH'!
    network_mode: bridge # add to the same network as docker run would do
    ports:
      - 8090:8080
    environment:
      - APACHE_PORT=11000  # change this port number if 11000 is already in use on your host system.
      - APACHE_IP_BINDING=192.168.110.246     #改成你搭建的服务器的IP
      - BORG_RETENTION_POLICY=--keep-within=7d --keep-weekly=4 --keep-monthly=6
      - NEXTCLOUD_UPLOAD_LIMIT=50G
      - NEXTCLOUD_MAX_TIME=3600
      - NEXTCLOUD_MEMORY_LIMIT=1024M
      - NEXTCLOUD_ADDITIONAL_PHP_EXTENSIONS=imagick
volumes: # If you want to store the data on a different drive, see https://github.com/nextcloud/all-in-one#how-to-store-the-filesinstallation-on-a-separate-drive
  nextcloud_aio_mastercontainer:
    name: nextcloud_aio_mastercontainer # This line is not allowed to be changed as otherwise the built-in backup solution will not work

```



## 二、系统设置

### 禁用snap自动更新

为什么禁用？

​	snap会自动更新，可能会导致某些软件不兼容

```shell
禁用
snap refresh --hold
开启
snap refresh --unhold
```



### 禁用系统自动更新



### sudo时无法使用代理

> sudo在切换成root用户的时候，env并不会去保留这些环境变量，需要特别的指明才可以。

```shell
# 在/etc/sudoers中，env_reset下添加
Defaults env_keep="http_proxy https_proxy ftp_proxy no_proxy"
```

### 设置静态IP

sudo vim /etc/network/interfaces

```

```

