---
title: 安装宝塔面板nginx防火墙启动失败解决方案
category: 宝塔面板相关
tags: nginx,linux
updatedAt: 2024-02-19T14:38:30.159Z
date: 2024-02-18T08:50:44.573Z
---



安了宝塔带的nginx防火墙模拟攻击不出现拦截效果，重启nginx服务报错，报错大概这样：

```
ERROR:
nginx: [emerg] "lua_package_path" directive is duplicate in /www/server/panel/vhost/nginx/btwaf.conf:6
nginx: configuration file /www/server/nginx/conf/nginx.conf test failed
```

<!-- more -->


打开`/www/server/panel/vhost/nginx/btwaf.conf`文件：
```
lua_shared_dict spider 10m;
lua_shared_dict btwaf 30m;
lua_shared_dict drop_ip 30m;
lua_shared_dict drop_sum 30m;
lua_shared_dict btwaf_data 100m;
lua_package_path "/www/server/btwaf/?.lua;";
init_by_lua_file  /www/server/btwaf/init.lua;
access_by_lua_file /www/server/btwaf/waf.lua;
#header_filter_by_lua_file /www/server/btwaf/header.lua;
body_filter_by_lua_file /www/server/btwaf/body.lua;
```
第6行配置是`lua_package_path "/www/server/btwaf/?.lua;";`，不出意外在nginx主配置文件（`http{}`中）里也有一行`lua_package_path "/xxx/path/?.lua;";`的语句。

而nginx所有的引用的配置文件中应该是只允许出现一行`lua_package_path "/xxx/path/?.lua;";`的语句，这里因为`/www/server/panel/vhost/nginx/btwaf.conf`这个文件也有一行类这样的语句，那总共就有两行这样的语句了，自然就会报错。

## 解决方案
这时候可以把`/www/server/panel/vhost/nginx/btwaf.conf`文件第六行的`lua_package_path "/www/server/btwaf/?.lua;";`注释报错。

并且把`/www/server/btwaf/?.lua;`添加到nginx主配置文件（`http{}`中）里`lua_package_path "/xxx/path/?.lua;";`的语句中，改成`lua_package_path "/xxx/path/?.lua;/www/server/btwaf/?.lua;";`这样。再重启下nginx，如果nginx重启不报错，应该就没啥问题了。再用宝塔nginx防火墙里的模拟攻击，能显示拦截网页就没问题了。


![图片.png](https://statics.xian1u.ren/notes/img/2024/02/319c125fcad10c0553a4417db88e1906.%C3%A5%C2%9B%C2%BE%C3%A7%C2%89%C2%87.png)