---
layout: post
title: "为Git设置代理"
description: "set git proxy"
keywords: "git"
category: "Linux"
tags: [Linux]
---
{% include JB/setup %}

在某些网络中，所有访问都通过代理服务器转发，为了正常使用Git，就需要对其代理进行配置，Git目前支持的三种协议 ``git://``、``ssh://`` 和 ``http://``，不同协议配置上有所区别，下面分别进行说明。


####配置HTTP代理

####http协议

如果是``git clone http://``或``git clone https://``，只需将代理服务器地址添加到环境变量即可，在``.bashrc``最后加入以下代码：

```bash
export http_proxy="http://username:password@host:port/"
export https_proxy="http://username:password@host:port/"
```

<!-- more -->

####git协议

为git协议配置HTTP代理此处要用到``socat``工具，并创建脚本配置代理参数，最后配置git使用创建的脚本：

```bash
$ sudo apt-get install socat

$ sudo vi /usr/bin/gitproxy
#!/bin/bash

PROXY=squid.vpsee.com
PROXYPORT=3128
PROXYAUTH=username:password
exec socat STDIO PROXY:$PROXY:$1:$2,proxyport=$PROXYPORT,proxyauth=$PROXYAUTH

$ sudo  chmod +x /usr/bin/gitproxy

$ git config --global core.gitproxy gitproxy
```




