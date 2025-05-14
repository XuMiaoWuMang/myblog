+++
date = '2025-05-14T16:59:45+08:00'
draft = true
title = 'MkfifoNoSuchFileOrDirectory解决办法'
+++
mkfifo函数报错：“mkfifo: No such file or directory”解决办法
<!--more-->

## 原因：
你的文件路径在Windows的共享文件夹里，而window的文件系统又不支持管道文件。

## 解决办法：
将创建的管道文件路径改为linux的本地文件夹。