---
layout: post
title: "用script命令录制终端会话"
description: "record terminal session with script "
keywords: "script"
category: "Linux"
tags: [Linux]
---
{% include JB/setup %}

在使用Linux的过程中，很多时候（比如配置某种开发环境）需要记录终端的操作步骤，以后后续参考。虽然很多终端具有将会话保存成文件的功能，但本文要介绍的是使用Linux系统内置的命令``script``来进行录制。


####录制

script的使用非常简单，直接键入``script``，就会将后续终端操作记录在默认的``typescript``文件中,退出录制需要键入``exit``命令：

```bash
john@john-pc:~$ script
Script started, file is typescript
john@john-pc:~$ ls
Desktop  Documents  Downloads  typescript  Videos
john@john-pc:~$ exit
exit
Script done, file is typescript

```

<!-- more -->

我们可以查看typescript文件中的内容：

```bash
john@john-pc:~$ cat typescript 
Script started on Fri 13 Jun 2014 10:54:42 PM CST
john@john-pc:~$ ls
Desktop  Documents  Downloads  typescript  Videos
john@john-pc:~$ exit
exit

Script done on Fri 13 Jun 2014 10:54:44 PM CST

```


####指定保存文件名

``-a``选项可以给script执行输出文件名，这样便于区分不同的记录。

```bash
john@john-pc:~$ script -a record.txt
Script started, file is record.txt
john@john-pc:~$ ls
Desktop  Documents  Downloads  typescript  record.txt  Videos
john@john-pc:~$ uname
Linux
john@john-pc:~$ exit
exit
Script done, file is record.txt
```

####回放录制内容

我们可以通过``scriptreplay``命令来回放录制内容，前提是在录制的时候加上``-t``选项，如下：

```bash
john@john-pc:~$ script -trecord.time -a record.txt 
Script started, file is record.txt
john@john-pc:~$ date
Fri Jun 13 23:23:52 CST 2014
john@john-pc:~$ exit
exit
Script done, file is record.txt
```

这样就会多生成一个timing文件“record.time”.

如果``-t``选项后直接跟文件名，文件名和``-t``之间不能有空格，``-t``默认是将时间输出到stderr，若使用空格，需按以下方式将stderr内容重定向到指定文件:

```bash
john@john-pc:~$ script -t 2>record.time -a record.txt 
```


回放时指定时间文件与录制文件即可：

```bash
john@john-pc:~$ scriptreplay -t record.time record.txt 
```





