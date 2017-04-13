---
layout: post
title: Centos7下安装Python3.6
category: 技术
tags: Essay
keywords: Centos7,Linux,Python
description: 无
---

今天下午在Centos7上安装Python3.6.1时遇到了报错，导致安装失败。错误如下：
> zipimport.ZipImportError: can’t decompress data; zlib not available

通过查找网上解决方法如下：

1. 安装依赖zlib、zlib-devel
	1. 下载zlib源码
	2. 解压zlib压缩文件
	3. ./configure
	4. make & make install
2. 重新编译安装Python
	1.  ./configure 
	2. 编辑Modules/Setup文件 
	3. 找到下面这句，去掉注释 
	4. #zlib zlibmodule.c -I$(prefix)/include -L$(exec_prefix)/lib -lz 
	5. 重新编译安装：make & make install

另外安装好后，我们可以使用python3命令使用python新版本，但我们想将python3设置为python命令的默认使用版本，而由于centos7现在默认版本为python2.7.5，并且yum命令使用了python2.7.5，所以按如下步骤解决：

1. 先将原来的python软连接重名 mv /usr/bin/python /usr/bin/python2.7.5
2. 编辑下yum的配置文件：vi /usr/bin/yum，把文件头部的#!/usr/bin/python改成#!/usr/bin/python2.7.5保存退出即可
3. 建立一个新的链接：ln -s /usr/local/bin/python3.6 /usr/bin/python
4. 检查是否成功，python -V