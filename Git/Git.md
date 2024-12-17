# GIT

## 一、安装

### Ubuntu

```shell
# 1. 添加Git官方仓库
sudo add-apt-repository ppa:git-core/ppa
# 2. 安装Git
sudo apt update
sudo apt install git
git --version
```

## 二、clone 用法

### public的仓库

> public的仓库直接clone就行

```shell
git clone https://github.com/spring-projects/spring-framework.git
```

### private的仓库

> private的仓库需要账号密码，这里特别要注意的是**密码不是github的登陆密码，而是Tokens**，Tokens需要到github生成。生成步骤如下截图。



```shell
git clone https://github.com/BrightSt/my_note.git
```

## 三、提交

### 常用

```shell
# 添加当前目录到暂存区
git add .
# 从暂存区提交到本地版本控制中
git commit -m '提交信息'
# 从本地版本中推到远程仓库中
git push origin
# 从远程仓库更新到本地
git pull 
```

