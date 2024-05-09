---
title: 记录Ubuntu 22.04 LTS 磁盘无法正常访问问题的解决
date: 2024-05-10 02:43:59
categories:
- Technologies_exploration
- Linux
---
最近属实是有点太压抑了，于是斥巨资买下了HOGWARTS，然后在下载的时候发现游戏盘掉了，表现为：
```
unable to access "xxx", an operation is pending 
```
找了一下，原因是上一次拔硬盘的时候没有安全退出

【解决方法】
```bash
sudo fdisk -l 
```
![](image.png)
最后的设备/dev/sda1就是出问题的磁盘，于是我们需要修复挂载错误的相应分区
```bash
sudo ntfsfix /dev/sda1
```
然后再次插入硬盘就可以正常使用了，后续有空了可能会对挂载失败问题进行更深入的探究