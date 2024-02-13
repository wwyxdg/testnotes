---
title: nginx反代vanblog配置
category: Linux
tags: vanblog,nginx,反向代理,linux,宝塔面板,宝塔
updatedAt: 2024-02-13T14:53:46.082Z
date: 2024-02-08T14:19:54.908Z
---




#### 反向代理配置代码

```nginx
location /
{
    proxy_pass http://127.0.0.1:7843;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header Upgrade $http_upgrade;
    
     

    proxy_ignore_headers Set-Cookie Cache-Control expires;
    proxy_cache cache_one;
    proxy_cache_key $host$uri$is_args$args;
    proxy_cache_valid 200 304 301 302 0m;
}
```

### 修改站点配置文件避免首页内容不刷新


<!-- more -->

如果站点配置里有35-46行这样的代码，也需要注释掉，选中后ctrl+/即可，别忘保存配置



![需要注释的内容](https://statics.xian1u.ren/notes/img/2024/02/9b3448c2ca1b7fc5ed9f18dcb189dfe8.QQå¾ç20240205151838.png)

![注释后](https://statics.xian1u.ren/notes/img/2024/02/e66f90e44307e7dda0ca353597ee8723.QQå¾ç20240205151909.png)





