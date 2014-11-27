---
layout: post
title: "手动清除Linux Cache"
description: "clean linux cache manually"
keywords: "cache"
category: "Linux"
tags: [Linux, Cache]
---
{% include JB/setup %}


由于Linux系统为了提高效率，会将一些page及object放在缓存中便于快速访问，这样会对查看系统内存消耗造成影响，因此我们需要手动释放这些缓存，可以通过如下命令释放Linux Cache:

```bash
sync
echo 3 > /proc/sys/vm/drop_caches
```

执行后，可以通过``cat /proc/meminfo``中的``Cached``字段来查看系统的缓存.

<!-- more -->

在kernel的[vm.txt](https://www.kernel.org/doc/Documentation/sysctl/vm.txt)文档中有对``drop_caches``的详细描述

由于``drop_caches``不会清除未写入硬盘的cache，因此执行sync是为了将一些Cache中的内容写入硬盘，增加可释放的cache。


####Note:
如果禁用cache会对系统性能造成影响，系统每次都需要重新去访问及创建被删除的page及object，会增加I/O及CPU负载，因此在正常的系统运行中，应保持``/proc/sys/vm/drop_caches``的值为默认值0.

