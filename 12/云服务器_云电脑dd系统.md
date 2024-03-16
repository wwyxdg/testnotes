---
title: 云服务器 云电脑dd系统
category: Windows
tags: dd,windows,linux
updatedAt: 2024-03-16T02:50:19.770Z
date: 2024-03-16T02:50:19.770Z
---


## 用的项目地址

https://github.com/bin456789/reinstall

## Windows系统dd到Windows系统

<!-- more -->

## 准备
1. 关闭Windows防火墙
2. 关闭自带杀毒软件，微软自带的杀软关闭实时防护
3. 记录下当前的IP地址、网关、DNS、MAC地址，通常都能自动获取，但是最后记录下

```
reinstall.bat windows --iso='https://drive.massgrave.dev/zh-cn_windows_10_enterprise_ltsc_2021_x64_dvd_033b7312.iso'  --image-name='Windows 10 Enterprise LTSC 2021'
```

>--iso的是镜像下载地址，--image-name是镜像名称

重装完后默认用户是`Administrator`，密码`123@@@`
