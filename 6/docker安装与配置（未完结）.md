---
title: docker安装与配置（未完结）
category: Linux
tags: linux,docker
updatedAt: 2024-02-08T15:40:55.948Z
date: 2024-02-08T15:38:45.151Z
---



<!-- more -->

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
docker-compose -version
```

2. ### 卸载docker-compose

```
rm  /usr/local/bin/docker-compose
```
                      
>原文链接：https://blog.csdn.net/m0_37899908/article/details/131268835