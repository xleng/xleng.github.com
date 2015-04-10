---
layout: post
title: "Linux screen命令的使用"
description: "linux command useage screen"
keywords: "linux, screen"
category: "Linux"
tags: [Linux, screen] 
---
{% include JB/setup %}

###问题

在开发中，经常需要SSH远程登录到Linux服务器进行编译，某些编译需要很长时间才能完成，以前都是为每一个任务开一个putty，而且在此期间不能关掉窗口或者断开连接，否则这个任务就会被杀掉。如果遇到连接出现问题，下次就需要重新开始进行任务，这样会做很多无用功。

<!-- more -->


###GNU Screen

GNU Screen可以看作是窗口管理器的命令行界面版本。它提供了统一的管理多个会话的界面和相应的功能。


####会话恢复

只要Screen本身没有终止，在其内部运行的会话都可以恢复。这一点对于远程登录的用户特别有用——即使网络连接中断，用户也不会失去对已经打开的命令行会话的控制。只要再次登录到主机上执行screen -r就可以恢复会话的运行。同样在暂时离开的时候，也可以执行分离命令detach，在保证里面的程序正常运行的情况下让Screen挂起（切换到后台）。这一点和图形界面下的VNC很相似。


####多窗口

在Screen环境下，所有的会话都独立的运行，并拥有各自的编号、输入、输出和窗口缓存。用户可以通过快捷键在不同的窗口下切换，并可以自由的重定向各个窗口的输入和输出。Screen实现了基本的文本操作，如复制粘贴等；还提供了类似滚动条的功能，可以查看窗口状况的历史记录。窗口还可以被分区和命名，还可以监视后台窗口的活动。


####会话共享

Screen可以让一个或多个用户从不同终端多次登录一个会话，并共享会话的所有特性（比如可以看到完全相同的输出）。它同时提供了窗口访问权限的机制，可以对窗口进行密码保护。



###常用命令

``screen -S bitbake``   创建一个名为bitbake的session

``screen -ls``          列出当前的所有session

``screen -r bitbake``   恢复session的连接，可用session的名字或者通过``screen -ls``列出的id

``screen -x bitbake``   以共享方式恢复session的连接，多个client的session将显示相同内容

``C-a d``               从当前的session中分离

``C-a k``               杀掉当前的session


