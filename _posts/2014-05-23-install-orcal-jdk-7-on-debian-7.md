---
layout: post
title: "Install Oracle JDK 7 on Debian 7"
description: "Steps used for install JDK on Debian like system"
keywords: "JDK, Debian"
category: "Java"
tags: [Java]
---
{% include JB/setup %}

Debian及Ubuntu中的JDK源是Open-JDK，如果需要安装Oracle版的JDK，可以根据以下步骤进行安装。

####Step 1:

从Oracle[网站](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)下载相应JDK 7版本，此处下载 ``jdk-7u55-linux-i586.tar.gz``。

<!-- more -->

####Step 2:
从终端进入下载目录，执行解压命令：

```bash
john@localhost:~$ tar xzvf jdk-7u55-linux-i586.tar.gz 
```

解压后会生成相应目录\(此处为``jdk1.7.0_55``\), 将解压后的目录放到/usr/lib/jvm下：

```bash
john@localhost:~$ sudo mkdir -p /usr/lib/jvm
john@localhost:~$ sudo mv jdk1.7.0_55 /usr/lib/jvm/jdk1.7.0
john@localhost:~$ sudo chown -R root:root /usr/lib/jvm/jdk1.7.0
```

####Step 3:
最后我们需要通过``update-alternatives``命令来管理Java版本,执行以下命令将我们需要的Java版本添加到系统中：

```bash
john@localhost:~$ sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk1.7.0/bin/java" 1
john@localhost:~$ sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/lib/jvm/jdk1.7.0/bin/javac" 1 
john@localhost:~$ sudo update-alternatives --install "/usr/bin/javaws" "javaws" "/usr/lib/jvm/jdk1.7.0/bin/javaws" 1
```

查看Java版本是否是我们所需要的：

```bash
john@localhost:~$ java -version
java version "1.7.0_55"
Java(TM) SE Runtime Environment (build 1.7.0_55-b13)
Java HotSpot(TM) Server VM (build 24.55-b03, mixed mode)

```

如果版本仍热是其他版本：

```bash
john@localhost:~$ java -version
java version "1.6.0_27"
OpenJDK Runtime Environment (IcedTea6 1.12.6) (6b27-1.12.6-1~deb7u1)
OpenJDK Server VM (build 20.0-b12, mixed mode)

```
这说明系统中还存在其他版本的JDK，同样通过``update-alternatives --config``来选择相应版本：

```bash
john@localhost:~$ sudo update-alternatives --config java
There are 3 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                             Priority   Status
  ------------------------------------------------------------
  * 0         /usr/lib/jvm/java-7-openjdk-i386/jre/bin/java   1071      auto mode
    1         /usr/lib/jvm/java-6-openjdk-i386/jre/bin/java   1061      manual mode
    2         /usr/lib/jvm/java-7-openjdk-i386/jre/bin/java   1071      manual mode
    3         /usr/lib/jvm/jdk1.7.0/bin/java                  1         manual mode
  
  Press enter to keep the current choice[*], or type selection number: 3
```

从上面运行结果可以看出，默认的Java版本是openjdk 7，我们输入Oracle Java相应序号\(此处为``3``\)，再执行``java -version``，Java已经切换到Oracle版本。javac及javaws也可以通过相同方式进行配置。

最后配置``JAVA_HOME``：

```bash
sudo sh -c 'echo "export JAVA_HOME=/usr/lib/jvm/jdk1.7.0/" >> /etc/profile.d/java.sh'
```
