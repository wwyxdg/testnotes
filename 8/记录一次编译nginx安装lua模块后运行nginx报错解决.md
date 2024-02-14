---
title: 记录一次编译nginx安装lua模块后运行nginx报错解决
category: 折腾记录
tags: nginx,linux
updatedAt: 2024-02-14T13:11:31.784Z
date: 2024-02-14T13:11:31.784Z
---


之前手动编译安装了nginx最新版，因为当时忘了给nginx添加lua模块。就重新下载了lua模块源码重新编译，编译时提示`./configure: error: unsupported LuaJIT version； ngx_http_lua_module requires LuaJIT 2.x.`,添加完环境变量后正常编译了,编译完后运行nginx报错。看错误提示，应该主要是`module 'thread.exdata' not found`和`module 'resty.core' not found`这俩问题。
折腾几个小时才搞定。特地记录下。


<!-- more -->


运行错误提示：
```
root@VM-0-4-debian:/www/server/nginxmodel/lua-resty-core-0.1.28# /etc/init.d/nginx  start
Starting nginx... nginx: [error] failed to run the Lua code for coroutine_api: 2: coroutine_api:2: module 'thread.exdata' not found:
	no field package.preload['thread.exdata']
	no file '/usr/local/Lua_core/lib/lua/thread/exdata.lua'
	no file './thread/exdata.so'
	no file '/usr/local/lib/lua/5.1/thread/exdata.so'
	no file '/usr/local/lib/lua/5.1/loadall.so'
	no file './thread.so'
	no file '/usr/local/lib/lua/5.1/thread.so'
	no file '/usr/local/lib/lua/5.1/loadall.so'
nginx: [alert] failed to load the 'resty.core' module (https://github.com/openresty/lua-resty-core); ensure you are using an OpenResty release from https://openresty.org/en/download.html (reason: module 'resty.core' not found:
	no field package.preload['resty.core']
	no file '/usr/local/Lua_core/lib/lua/resty/core.lua'
	no file './resty/core.so'
	no file '/usr/local/lib/lua/5.1/resty/core.so'
	no file '/usr/local/lib/lua/5.1/loadall.so'
	no file './resty.so'
	no file '/usr/local/lib/lua/5.1/resty.so'
	no file '/usr/local/lib/lua/5.1/loadall.so') in /www/server/nginx/conf/nginx.conf:98
 failed
```


## 解决`module 'resty.core' not found`

我在编译nginx时用的`lua-nginx-module`版本是`0.10.26`，低版本的模块（<`0.10.16`）可以使用`lua_load_resty_core off;`这个配置解决问题，告别那边就要手动安装这俩模块。


### 下载`lua-resty-lrucache`和`lua-resty-core`这两个模块源代码，使用`make install`命令安装这两个模块。

执行命令：

```
wget https://github.com/openresty/lua-resty-lrucache/archive/refs/tags/v0.13.zip
unzip v0.13.zip
cd lua-resty-lrucache-0.13/
make install PREFIX=/usr/local/lua_core

wget https://github.com/openresty/lua-resty-core/archive/refs/tags/v0.1.28.zip
unzip v0.1.28.zip
cd lua-resty-core-0.1.28/
make install PREFIX=/usr/local/lua_core
```

### 找到nginx配置文件，在http{}中加上一条`lua_package_path '/usr/local/lua_core/lib/lua/?.lua;';`即可。


>`make install PREFIX=/usr/local/lua_core`就是把模块安装在`/usr/local/lua_core`目录中

>参考：https://blog.51cto.com/u_15064643/4273810

再次执行`/etc/init.d/nginx start`测试，不报`module 'resty.core' not found`错误了，这个问题解决了。

```
root@VM-0-4-debian:/www/server/nginxmodel/lua-resty-core-0.1.28# /etc/init.d/nginx  start
Starting nginx... nginx: [error] failed to run the Lua code for coroutine_api: 2: coroutine_api:2: module 'thread.exdata' not found:
	no field package.preload['thread.exdata']
	no file '/usr/local/lua_core/lib/lua/thread/exdata.lua'
	no file './thread/exdata.so'
	no file '/usr/local/lib/lua/5.1/thread/exdata.so'
	no file '/usr/local/lib/lua/5.1/loadall.so'
	no file './thread.so'
	no file '/usr/local/lib/lua/5.1/thread.so'
	no file '/usr/local/lib/lua/5.1/loadall.so'
```


##  解决`module 'thread.exdata' not found`

搞完`module 'resty.core' not found`的问题还有`module 'thread.exdata' not found`的问题。



### 先卸载之前安装的luajit，再安装openresty优化的luajit

```
cd /www/server/nginxmodel/LuaJIT
make uninstall
```
>之前是用源代码编译安装的，卸载也是进源代码目录直接执行make uninstall



### 下载openresty优化后的luajit程序源代码，然后编译安装luajit

执行：

```
wget https://github.com/openresty/luajit2/archive/refs/tags/v2.1-20231117.zip
unzip v2.1-20231117.zip
cd /www/server/nginxmodel/luajit2-2.1-20231117
make
make install
```

使用`luajit -v`测试，输出版本号，安装成功。

```
root@VM-0-4-debian:/opt/vanblog# luajit -v
LuaJIT 2.1.1700206165 -- Copyright (C) 2005-2023 Mike Pall. https://luajit.org
```

>参考：https://blog.csdn.net/wzr54321/article/details/127702437

成功解决这俩问题，大功告成。。。