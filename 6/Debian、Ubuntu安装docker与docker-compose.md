---
title: Debian、Ubuntu安装docker与docker-compose
category: Linux
tags: linux,docker
updatedAt: 2024-04-06T13:32:28.714Z
date: 2024-02-08T15:38:45.151Z
---


## 安装/卸载docker

### Debian安装docker

阿里云Debian系统docker软件源：https://mirrors.aliyun.com/docker-ce/linux/debian/
中科大Debian系统docker软件源：https://mirrors.ustc.edu.cn/docker-ce/linux/debian/
>下面安装步骤用的都是阿里云的源，想用中科大的源，直接把命令中的`https://mirrors.aliyun.com/docker-ce/linux/debian/`替换成`https://mirrors.ustc.edu.cn/docker-ce/linux/debian/`

<!-- more -->

#### 更新软件包索引

```
sudo apt-get update
```

#### 安装依赖

```
sudo apt-get -y install apt-transport-https ca-certificates curl gnupg2 software-properties-common
```

#### 添加 Docker 的官方 GPG 密钥：

```
curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/debian/gpg | sudo apt-key add -
```

>比较新的系统在执行这个的时候可能会提示错误：

```
root@VM-0-4-debian:~# curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/debian/gpg | sudo apt-key add -
Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8)).
OK
```

>解释：
>
>apt-key 是一个用于管理Debian及其衍生系统中APT软件包管理器所用的密钥的命令。在较新版本的Debian和Ubuntu系统中，该命令已被弃用，并建议使用新的方法（用`gpg`命令）来管理密钥。

这时候可以先把GPG密钥下载下载，再用`gpg`命令导入进去

下载密钥保存成名为`gpgfile`的文件：
```
curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/debian/gpg -o gpgfile
```

使用`gpg`命令导入密钥：
```
gpg --import gpgfile
```


运行过程记录：
```
root@VM-0-4-debian:~# curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/debian/gpg -o gpgfile
root@VM-0-4-debian:~# gpg --import gpgfile
gpg: directory '/root/.gnupg' created
gpg: keybox '/root/.gnupg/pubring.kbx' created
gpg: /root/.gnupg/trustdb.gpg: trustdb created
gpg: key 8D81803C0EBFCD88: public key "Docker Release (CE deb) <docker@docker.com>" imported
gpg: Total number processed: 1
gpg:               imported: 1
```

>理论上合成一条命令也是可以的：
>```
>curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/debian/gpg | gpg --import
>```


#### 使用以下指令设置稳定版仓库

```
sudo add-apt-repository "deb [arch=amd64] https://mirrors.aliyun.com/docker-ce/linux/debian $(lsb_release -cs) stable"
```
#### 再更新软件包索引

```
sudo apt-get update
```

#### 安装最新版本的 Docker Engine-Community 和 containerd

```
sudo apt-get -y install docker-ce docker-ce-cli containerd.io
```

部分内容参考[菜鸟教程](https://www.runoob.com):https://www.runoob.com/docker/debian-docker-install.html

### Ubuntu 14.04/16.04（使用 apt-get 进行安装）安装docker

```
# step 1: 安装必要的一些系统工具
sudo apt-get update
sudo apt-get -y install apt-transport-https ca-certificates curl software-properties-common
# step 2: 安装GPG证书
curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
# Step 3: 写入软件源信息
sudo add-apt-repository "deb [arch=amd64] https://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
# Step 4: 更新并安装Docker-CE
sudo apt-get -y update
sudo apt-get -y install docker-ce

# 安装指定版本的Docker-CE:
# Step 1: 查找Docker-CE的版本:
# apt-cache madison docker-ce
#   docker-ce | 17.03.1~ce-0~ubuntu-xenial | https://mirrors.aliyun.com/docker-ce/linux/ubuntu xenial/stable amd64 Packages
#   docker-ce | 17.03.0~ce-0~ubuntu-xenial | https://mirrors.aliyun.com/docker-ce/linux/ubuntu xenial/stable amd64 Packages
# Step 2: 安装指定版本的Docker-CE: (VERSION例如上面的17.03.1~ce-0~ubuntu-xenial)
# sudo apt-get -y install docker-ce=[VERSION]
```

>转自：https://developer.aliyun.com/mirror/docker-ce/


### 卸载docker

Debian/Ubuntu:

```
sudo apt-get  remove docker-ce docker-ce-cli containerd.io
```

### 国内机器使用docker官方脚本安装失败后执行更新软件包索引命令`suo apt-get -y update`报错/卡顿修复方案

原理就是把官方脚本添加的软件源给删掉,即删除`/etc/apt/sources.list.d/docker.list`和`/etc/apt/sources.list.d/docker.list`两个文件

命令:

```
sudo rm -rf /etc/apt/sources.list.d/docker.list
sudo rm -rf /etc/apt/sources.list.d/docker.list.save
```
这俩文件里的东西就是docker官方脚本添加的软件源。删除这俩文件按前面步骤安装docker就行了。

## 安装/卸载docker-compose

1. ### 安装docker-compose

下载docker-compose文件到/usr/local/bin/
```
curl -L https://github.com/docker/compose/releases/download/1.21.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```

给执行权限
```
chmod +x /usr/local/bin/docker-compose
```
查看是否安装成功
```
docker-compose --version
```

2. ### 卸载docker-compose

```
rm  /usr/local/bin/docker-compose
```
                      
>原文链接：https://blog.csdn.net/m0_37899908/article/details/131268835