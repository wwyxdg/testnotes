---
title: vanblog配置图床图片存储到cloudflare R2存储桶（理论S3 API接口存储桶通用）
category: vanblog配置
tags: vanblog,R2,S3
updatedAt: 2024-02-19T14:49:23.523Z
date: 2024-02-19T14:29:16.187Z
---


vanblog自带的图床除了支持把图片存储到本地之外，还可以存储到别的图床或者对象存储中。这是基于 picgo-core 实现的。

PicGo有个Amazon S3 插件。支持 上传图片到Amazon S3 与其他兼容S3 API的云存储（比如cloudflare r2， backblaze b2等）。

以下是配置cloudflare r2。其他兼容S3 API的存储桶也可以参考。

<!-- more -->

存储策略选OSS图床。

## 自定义 picgo 插件

插件名称直接写`s3`就行

## picgo 配置

以下配置模板实测cloudflare r2存储桶可以用，根据实际改一下信息后即可使用，别的S3 API的存储桶删改几项参数就行。

>可能还有几项配置是多余的，有时间再测试哪几项可以删除

```
{
  "picBed": {
    "current": "aws-s3",
    "uploader": "aws-s3",
    "aws-s3": {
      "accessKeyID": "idididid",
      "secretAccessKey": "keykeykey",
      "uploadPath": "path/{year}/{month}/{fullName}",
      "bucketName": "bucket2344",
      "endpoint": "https://xxxxxxxxx.r2.cloudflarestorage.com",
      "urlPrefix": "https://example.com"
    }
  },
  "picgoPlugins": {
    "picgo-plugin-s3": true
  }
}
```

改完配置后直接把配置整体复制到系统设置-图床设置-存储策略设置-picgo 配置中，如图。

![例图](https://statics.xian1u.ren/notes/img/2024/02/3fa698830957c2ed672ff1b7bd4af9cf.%C3%A5%C2%9B%C2%BE%C3%A7%C2%89%C2%87.png)

### 必须要在`"aws-s3":{}`中改动值的几个key：

| Key             | 需要填入的值                          |     
| ---------------- | ----------------------------- | 
| accessKeyID     | 对应的是R2 API令牌的的访问密钥ID |
| secretAccessKey | 对应的是R2 API令牌的机密访问密钥 |
| bucketName |对应的是R2存储桶的名称 |
| endpoint | 对应的是R2存储桶的S3 API地址（其他的兼容的S3存储桶应该也是写这个API地址），R2存储桶的S3 API地址在R2存储桶的设置里，只需要写`https://域名`(例如`https://xxxxxxxxx.r2.cloudflarestorage.com`)就可以了 |
| urlPrefix | R2存储桶访问域名，格式：`https://example.com`,绑定自定义域名的写自定义域名,没有的写R2.dev 子域，并且允许公共访问 |

- 别的S3 API存储桶应该也就改这几项配置，可能还需要在在`"aws-s3":{}`加个`region`或者别的键值对
- 如果本身就是AWS S3存储桶，看需删改一下`endpoint`和`region`这两对键值

完整配置：


| Key                  | 说明                                                                    | 例子                                                     |
| -------------------- | ----------------------------------------------------------------------- | -------------------------------------------------------- |
| `accessKeyID`        | AWS 凭证 ID                                                             |                                                          |
| `secretAccessKey`    | AWS 凭证密钥                                                            |                                                          |
| `bucketName`         | S3 桶名称                                                               | `gallery`                                                |
| `uploadPath`         | 上传路径                                                                | `{year}/{month}/{fullName}`                              |
| `urlPrefix`          | 最终生成图片 URL 的自定义前缀                                           | `https://img.example.com/my-blog/`                       |
| `endpoint`           | 指定自定义终端节点                                                      | `s3.us-west-2.amazonaws.com`                             |
| `proxy`              | 代理地址                                                                | 支持http代理，例如 `http://127.0.0.1:1080`               |
| `region`             | 指定执行服务请求的区域                                                  | `us-west-1`                                              |
| `pathStyleAccess`    | 是否启用 S3 Path style                                                  | 默认为 `false`，使用 minio 请设置为 `true` (e.g., https://s3.amazonaws.com/<bucketName>/<key> instead of https://<bucketName>.s3.amazonaws.com/<key>)              |
| `rejectUnauthorized` | 是否拒绝无效 TLS 证书连接                                               | 默认为 `true`，如上传失败日志显示证书问题可设置为`false` |
| `acl`                | 访问控制列表，上传资源的访问策略                                        | 默认为 `public-read`, AWS 可选 `private"|"public-read"|"public-read-write"|"authenticated-read"|"aws-exec-read"|"bucket-owner-read"|"bucket-owner-full-control`                                     |
| `disableBucketPrefixToURL`  | 开启 `pathStyleAccess` 时，是否要禁用最终生成URL中添加 bucket 前缀   | 默认为 `false`  |
    
    
>来源：插件作者说明文档：https://github.com/wayjam/picgo-plugin-s3/blob/main/README.md#%E9%85%8D%E7%BD%AE-configuration

### 可选更改信息（上传图片的路径）-`uploadPath`

看需更改即可

| payload      | 描述                   |
| ------------ | ---------------------- |
| `{year}`     | 当前日期 - 年          |
| `{month}`    | 当前日期 - 月          |
| `{day}`      | 当前日期 - 日          |
| `{fullName}` | 完整文件名（含扩展名） |
| `{fileName}` | 文件名（不含扩展名）   |
| `{extName}`  | 扩展名（不含`.`）      |
| `{md5}`      | 图片 MD5 计算值        |
| `{sha1}`     | 图片 SHA1 计算值       |
| `{sha256}`   | 图片 SHA256 计算值     |
| `{timestamp}`   | Unix 时间戳     |
| `{timestampMS}`   | Unix 时间戳（毫秒）     |

>来源：插件作者说明文档：https://github.com/wayjam/picgo-plugin-s3/blob/main/README.md#%E9%85%8D%E7%BD%AE-configuration
    
## 测试
填完配置后保存测试下能不能在后台的图片管理测试下能不能上传图片。









