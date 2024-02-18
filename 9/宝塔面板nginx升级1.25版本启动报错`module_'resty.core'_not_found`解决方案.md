---
title: 宝塔面板nginx升级1.25版本启动报错`module 'resty.core' not found`解决方案
category: Linux
tags: 宝塔面板,宝塔,nginx,linux
updatedAt: 2024-02-18T08:50:41.328Z
date: 2024-02-18T08:50:41.328Z
---



宝塔面板nginx升级到1.25可能启动失败，报错`module 'resty.core' not found`。

类似这样：
```
警告消息：

nginx: [alert] failed to load the 'resty.core' module (https://github.com/openresty/lua-resty-core); ensure you are using an OpenResty release from https://openresty.org/en/download.html (reason: module 'resty.core' not found:
no field package.preload['resty.core']
no file './resty/core.lua'
no file '/usr/local/share/luajit-2.1.0-beta3/resty/core.lua'
no file '/usr/local/share/lua/5.1/resty/core.lua'
no file '/usr/local/share/lua/5.1/resty/core/init.lua'
no file './resty/core.so'
no file '/usr/local/lib/lua/5.1/resty/core.so'
no file '/usr/local/lib/lua/5.1/loadall.so'
no file './resty.so'
no file '/usr/local/lib/lua/5.1/resty.so'
no file '/usr/local/lib/lua/5.1/loadall.so') in /www/server/nginx/conf/nginx.conf:109
```

<!-- more -->


## 解决方案

可以尝试在nginx配置文件中`http{}`这一段加入lua_package_path`"/www/server/nginx/lib/lua/?.lua;";`

