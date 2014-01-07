---
layout: post
title: "Franca IDL 介绍"
description: "Franca IDL 的简单介绍"
keywords: "Franca, IDL"
category: "GENIVI"
tags: [GENIVI]
---
{% include JB/setup %}


Franca是[GENIVI Alliance](http://www.genivi.org)于2011年推出一套开发框架，用于定义及转换软件接口。[Franca IDL](http://code.google.com/a/eclipselabs.org/p/franca/)(Franca Interface Definition Language)属于Franca framework的一部分，是一种基于文本的接口描述语言。


Franca IDL的一个例子:

![fidl sample](/assets/images/genivi/franca/franca_player_screenshot.png)

<!-- more -->

###Franca IDL 优点

   * 静态接口定义
    * 可定义接口属性(attribute)，方法(method)，广播(broadcast)。
    * 支持多个输入、输出参数及错误返回值。
    * 支持接口继承

   * 类型定义
    * 丰富的预定义基本类型
    * 可通过: enumeration, array, struct, union, map, typedef 定义自定义类型
    * 支持struct, union 和 enumeration的继承 

   * 接口行为定义
    * 接口支持状态机机制。


###Franca IDL 编辑器 

Franca提供基于eclipse的代码编辑器，支持以下特性:

* 语法高亮

* 代码折叠

* 错误提示

* 内容补全

* 跳转及重构

![fidl editor](/assets/images/genivi/franca/fidl_editor.png)



###Franca IDL 代码生成器
   Franca IDL可由专门的代码生成插件生成相应的C++代码，目前支持生成[C++ Common API]()和基于DBus的绑定。

   C++ Common API 已广泛应用于GENIVI的IVI系统中。

   选中相应的fidl文件，右键点击选中文件 > Common API > Generate D-Bus C++ Code

   ![fidl_generator](/assets/images/genivi/franca/fidl_generator.png)

