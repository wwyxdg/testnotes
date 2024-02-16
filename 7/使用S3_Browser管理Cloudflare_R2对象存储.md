---
title: 使用S3 Browser管理Cloudflare R2对象存储
category: Linux
tags: 对象存储,S3,windows,cloudflare,R2
updatedAt: 2024-02-16T14:28:46.178Z
date: 2024-02-14T05:48:47.670Z
---


Cloudflare R2对象存储不计流量费用，且每月都有免费存储容量和请求次数额度，还支持使用自家的cdn，超出免费额度他的存储和请求费用也不算贵。用来存储一些小文件是个不错的选择。可惜网页控制台中不支持单文件大小超300M/一次上传100个以上文件。偶尔需要上传大文件/很多小文件着实不太方便，最后发现S3 Browser软件支持访问兼容S3 API的存储桶，用来管理R2对象存储中的文件还挺合适的。

<!-- more -->


## 下载安装

去S3 Browser官网:(https://s3browser.com/) 下载S3 Browser。

直达下载链接：https://s3browser.com/download/s3browser-11-5-7.exe

下载后运行安装程序，一路点next就完事。

## 获取连接配置信息

### S3 API地址
进入cloudflare的控制台，左边列表中点进入R2-概述，进入创建好的存储桶，找到设置选项。

在存储桶详细信息里面有一项是S3 API。是一个网页链接，`https://域名/存储桶名称`这样的格式。
先把把域名复制下。

![图片.png](https://statics.xian1u.ren/notes/img/2024/02/9cc108dce7af9c3fd1efa787f7d1aafe.%C3%A5%C2%9B%C2%BE%C3%A7%C2%89%C2%87.png)


### 获取API令牌
进入R2概述界面，点右上角的`管理R2 API令牌`。


![图片.png](https://statics.xian1u.ren/notes/img/2024/02/e14c0800de8e4641bee7d6659323c4ba.%C3%A5%C2%9B%C2%BE%C3%A7%C2%89%C2%87.png)


令牌名称随意写，权限选`对象读和写`，指定存储桶选`仅应用于特定存储桶`，再选创建好的存储桶，其他都不用写，拉到最下面点创建API令牌就行了。

![图片.png](https://statics.xian1u.ren/notes/img/2024/02/89c5bffc8679bf9b08487545f07e128f.%C3%A5%C2%9B%C2%BE%C3%A7%C2%89%C2%87.png)

然后会显示令牌信息，令牌信息只显示一次，要趁现在保存。这里只需要保存`为 S3 客户端使用以下凭据：`中的访问密钥、ID机密访问密钥就行了，`为 S3 客户端使用管辖权地特定的终结点：`不需要复制，刚才复制的那个S3 API地址就是。

复制好信息点完成就可以了。


![图片.png](https://statics.xian1u.ren/notes/img/2024/02/b63be899aaaded8f35ab07b3e4ef7b3b.%C3%A5%C2%9B%C2%BE%C3%A7%C2%89%C2%87.png)

## 软件运行与配置
点桌面上的S3 Browser软件图标双击运行，找不到可以在开始菜单里找。

第一次打开软件会提示添加个新账户什么的。在这里Account type就要选S3 
COmpatible Storage。
>Cloudflare R2只是支持S3 API，本身并不是AWS的S3对象存储。


![选S3 COmpatible Storage](https://statics.xian1u.ren/notes/img/2024/02/542b528ae82b3e1b49d4e41bdd371924.%C3%A5%C2%9B%C2%BE%C3%A7%C2%89%C2%87.png)

需要要填写的几项就是刚才复制的信息。
- Display name就是备注，随便写就行。
- REST Endpoint对应填入的是S3 API地址，这里只需要填域名就可以了
- Access Key ID对应填入的是`为 S3 客户端使用以下凭据：`中的访问密钥
- Secret Access Key对应填入的是`为 S3 客户端使用以下凭据：`中的ID机密访问密钥


填完后点Add new accout，保存填入的信息即可，其他信息不需要写。


![图片.png](https://statics.xian1u.ren/notes/img/2024/02/680c3564eda76a462ff3d3654b33ff1d.%C3%A5%C2%9B%C2%BE%C3%A7%C2%89%C2%87.png)

然后会弹窗，这个提醒弹窗的大致意思就是不允许获得桶列表，要不要手动添加一个存储桶，因为刚才创建的R2 Token只有读取指定存储桶的权限。

直接点是就行。


![图片.png](https://statics.xian1u.ren/notes/img/2024/02/6a7ccc3e2caa70d909cf79535df31ad6.%C3%A5%C2%9B%C2%BE%C3%A7%C2%89%C2%87.png)

然后输入创建的存储桶的名称。再点`Add External Bucket`


![图片.png](https://statics.xian1u.ren/notes/img/2024/02/5697b5f9cc609831878c53123feff2f0.%C3%A5%C2%9B%C2%BE%C3%A7%C2%89%C2%87.png)

这个时候不出意外就能读取R2存储桶的数据了，就可以读写存储桶，上传文件/文件夹了。操作逻辑和window资源管理器类似。

>如果还是不显示存储桶的文件，点一下Refresh就行了


![图片.png](https://statics.xian1u.ren/notes/img/2024/02/e50965cca2d245a80485d2f6a2eae6f6.%C3%A5%C2%9B%C2%BE%C3%A7%C2%89%C2%87.png)
