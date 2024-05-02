---
title: Ubuntu Wake on Lan
date: 2024-02-20 23:42:36
categories:
---

最近因为自己搭建了一个vps而欣喜若狂而导致日崩。由于某些...的需求，我需要能够再不用的时候将服务器关机。因此我开始折腾远程开机。

我的思路是通过电脑主板自带的Wake on Lan 功能，目前来说大部分主板都有（我的主板是x99 QD4）。最大的问题是在于配置为S5(shutdown)状态下时网卡需要在关机后处于激活状态，而这里需要系统在启动后将对应的网卡状态设置为对应状态。（因为Ubuntu20.04后网络唤醒重启之后网卡状态设置就会失效。。。不知道为啥）

过程很简单，即通过发送一组特殊格式的网络封包（Magic Packet）给具有某个MAC地址的电脑，让该电脑从睡眠模式甚至是关机模式苏醒，即从ACPI的Sx(S3，S4，S5)模式返回S0运行模式。

根据以上的思路，我们就开始着手准备了。

# 服务端配置
我们可以通过ethtool工具来查看并修改网卡状态，因此首先安装ethtool工具：
```
sudo apt update
sudo apt install ethtool
```
通过ifconfig查看网络信息：
```
ifconfig
```

以我的为例：
```
enp6s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.200  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::b7e2:6743:aa3:5e49  prefixlen 64  scopeid 0x20<link>
        ether 0a:e0:af:b3:23:bf  txqueuelen 1000  (以太网)
        RX packets 10466  bytes 6877996 (6.8 MB)
        RX errors 0  dropped 3  overruns 0  frame 0
        TX packets 8851  bytes 860614 (860.6 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

这个就是我的有线网卡信息。可以看出，ether就是mac地址，网卡名为enp6s0。接下来通过ethtool查看网卡状态：
```
sudo ethtool enp6s0
```

可以看到：
```
Supports Wake-on: pumbg
Wake-on: d
```

这里附上Wake-on各种状态的参数含义：
```
Option	Description
p	Wake on PHY activity
u	Wake on unicast messages
m	Wake on multicast messages
b	Wake on broadcast messages
g	Wake on MagicPacket messages
```

更新网卡状态。由于我们要使用的是MagicPacket信息，因此：
```
sudo ethtool --change enp6s0 wol g
sudo ethtool enp6s0
```

此时看到：
```
Wake-on: g
```
说明状态修改成功。

由于每次开机后都要重新设置网卡的状态才能在下一次关机后再次使用网络唤醒，所以我们可以通过systemd添加一个系统服务在每次开机后修改网卡状态。
首先确定ethtool路径：
```
which ethtool
```
可见:
```
/usr/sbin/ethtool
```
这个因机器而异，因此下面的内容需要根据实际情况修改：

创建一个 /etc/systemd/system/wol.service 文件，在这里写下启动执行一次的服务信息：

```
[Unit]
Description=Enable Wake On Lan

[Service]
Type=oneshot
ExecStart = /usr/sbin/ethtool --change enp6s0 wol g

[Install]
WantedBy=basic.target
```

之后只需要enable该服务就可以:
```
sudo systemctl daemon-reload
sudo systemctl enable wol.service
```

检查一下对应的状态:
```
systemctl status wol
```
可以看到：
```
○ wakeonlan.service - Enable Wake On Lan
     Loaded: loaded (/etc/systemd/system/wol.service; enabled; vendor preset: enabled)
     Active: inactive (dead) since Tue 2024-02-20 23:32:35 +08; 28min ago
   Main PID: 948 (code=exited, status=0/SUCCESS)
        CPU: 2ms

Feb 20 23:32:34 Server systemd[1]: Starting Enable Wake On Lan...
Feb 20 23:32:35 Server systemd[1]: wol.service: Deactivated successfully.
Feb 20 23:32:35 Server systemd[1]: Finished Enable Wake On Lan.
```

说明服务正常运行。

# 远程启动

## Ubuntu && Mac
以Ubuntu和Mac为例，在命令行中执行wakeonlan xx:xx:xx:xx:xx:xx （输入Ubuntu机器对应的mac地址）就可以唤醒机器了

但是前提是安装了wakeonlan

## windows
这里我偷懒了，不想自己写一个脚本出来，因此我就用一些现成的工具了。此处我选择的是[WakeOnLanGui](https://www.depicus.com/wake-on-lan/wake-on-lan-gui)

界面如下：

{%asset_img image.png This is a image... %}

根据实际情况填写MAC地址、被控端域名\ip、子网掩码和端口号（任一）就行了