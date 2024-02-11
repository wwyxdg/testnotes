---
title: centos7安装Gitea-直接安装，非docker
category: Linux
tags: centos,gitea,git,linux
updatedAt: 2024-02-11T13:56:34.351Z
date: 2024-02-08T13:06:14.280Z
---


gitea 是一款轻量级的 Git 托管解决方案，它采用 Go 语言编写，操作简单方便，轻松搭建自己的 Git 服务。启动方便，只需要非常简单的命令就能启动。

<!-- more -->

## 下载gitea程序及配置环境
### 安装Golang

ubuntu/debian：

```
sudo apt-get install golang-go
```

centos：

```
sudo yum install golang
```

### 安装git

ubuntu/debian：

```
sudo apt-get install git
```
centos：

貌似自带git，执行`git version`查看系统自带git版本，最新版gitea 要求 git版本在2.0.0 以上才可以。低于该版本需要升级git才行。centos7 自带 git 最高才 1.83，需要升级。如果提示找不到git命令也需要安装git。

编译安装git最新版步骤：

1. 安装依赖

```
sudo yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel asciidocsudo yum install gcc perl-ExtUtils-MakeMaker
```

2. 卸载旧版 git

```
sudo yum remove git
```

3. 下载 git 源码

git 源码的下载地址：[https://mirrors.edge.kernel.org/pub/software/scm/git/](https://mirrors.edge.kernel.org/pub/software/scm/git/)

这里最新的版本是：git-2.30.0.tar.gz，下载后解压，然后进入目录

```
wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.30.0.tar.gz
tar -zvxf git-2.30.0.tar.gz
cd git-2.30.0
```

4. 编译安装

注意：install 的时候需要管理员权限，才能安装到 /usr/local 目录下面

```
make prefix=/usr/local/git all
sudo make prefix=/usr/local/git install
```

或

```
./configure --without-iconv
make CFLAGS=-liconv prefix=/usr/local/git all
sudo make CFLAGS=-liconv prefix=/usr/local/git install
```

编译安装后，git 的可执行文件会被放置到 /usr/local/git/bin/ 目录下

5. 使用方式

编译后还是无法使用 git 命令，是因为可执行文件被放在 /usr/local/git/bin/

有两种方法解决该问题

建立软链接：

```
sudo ln -s /usr/local/git/bin/git /usr/bin/git
```

添加环境变量：

```
echo “export PATH=$PATH:/usr/local/git/bin” >> /etc/bashrc
source /etc/bashrc
```

### 从官网下载最新版本的 gitea 安装包。

```
wget -O gitea https://dl.gitea.com/gitea/1.21.4/gitea-1.21.4-linux-amd64
```

### 将下载的 gitea 文件移动到 /usr/local/bin 目录下，并给予 gitea 可执行权限。

```
sudo mv gitea /usr/local/bin/
sudo chmod +x /usr/local/bin/gitea
```

### 创建一个用户

新版 gitea 不允许使用 root 用户运行，那就需要创建一个用户，使用这个用户运行gitea。

添加一个用户到 root 用户组（以创建gitea用户为例）

```
useradd gitea -g root
```
添加完用户后最好使用passwd命令重置下密码

### 创建 gitea 的配置文件，并设置相应的权限。
创建的文件夹和配置文件是gitea程序运行时所需要的，最新版gitea程序不允许使用root用户运行，只能使用非root用户运行，虽然gitea运行时会自动创建文件夹，但是因为权限不足创建失败，然后程序报错，结束运行...

```
mkdir /usr/local/bin/data
mkdir /usr/local/bin/custom
mkdir /usr/local/bin/data/tmp/package-upload
mkdir /usr/local/bin/data/tmp
mkdir -p /usr/local/bin/custom/conf/

echo > /usr/local/bin/custom/conf/app.ini

chown -R gitea /usr/local/bin/custom
chown -R gitea /usr/local/bin/data
chmod -R 755 /usr/local/bin/data
chmod -R 755 /usr/local/bin/custom
chown -R gitea /opt/gitea
chmod -R 755 /opt/gitea
```

>/opt/gitea是我设置的存储git仓库文件的路径
>
>chown是把文件夹/文件的所有者更改
>
>chmod是配置读写和可执行的权限


### 测试启动 gitea

先执行“su 用户名”切换到指定用户

切换到gitea用户
```
su gitea
```

测试运行

执行
```
gitea web
```
或
```
/usr/local/bin/gitea web
```


## 初始化相关配置

待补充...


## 后台运行 gitea

两种方法二选一

### 注册服务 （应该仅适用于 centos7 以上）

编辑配置文件

```
sudo vim /usr/lib/systemd/system/gitea.service
```
输入以下内容
```
[Unit]
#服务名称
Description=gitea

[Service]
#启动用户
User=gitea1
#启动命令
ExecStart=/usr/local/bin/gitea web
#自动重启
Restart=on-abort

[Install]
#多用户模式
WantedBy=multi-user.target
```

按 esc，输入:wq 保存
依次执行：

```
sudo systemctl daemon-reload
systemctl enable gitea
systemctl start gitea
```

说明：

1. 重新加载服务
2. 激活服务
3. 运行服务

### 使用 supervisor 运行 gitea

使用宝塔进程管理器可以直接新建supervisor守护进程

相关配置：

* 运行目录
* /home/gitea/
* 命令
* /usr/local/bin/gitea web
* 用户
* gitea


添加服务后需要在额外在配置文件中加 1 行

```
environment = HOME="/home/gitea"
```

完整配置文件 （手动添加supervisor配置文件可以使用这个配置文件实现守护进程）

```
[program:Gitea]
command=/usr/local/bin/gitea web
directory=/home/gitea/
autorestart=true
startsecs=3
startretries=3
stdout_logfile=/www/server/panel/plugin/supervisor/log/Gitea.out.log
stderr_logfile=/www/server/panel/plugin/supervisor/log/Gitea.err.log
stdout_logfile_maxbytes=2MB
stderr_logfile_maxbytes=2MB
user=gitea
priority=999
numprocs=1
process_name=%(program_name)s_%(process_num)02d
environment = HOME="/home/gitea"

```

## 其余步骤

使用 SSH 模式时需占用 22 端口，需要提权访问

```
setcap cap_net_bind_service=+eip /usr/local/bin/gitea
```
