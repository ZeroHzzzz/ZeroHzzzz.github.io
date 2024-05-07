---
title: 联想小新 pad pro 2023（TB371FC） root 过程记录
date: 2024-05-07 17:41:55
categories:
---
root结果还算是迷人，毕竟提升了自己机子的可玩性，但是这个过程真的算是道阻且长。
不管怎样，还是不建议在自己主力机上进行root
# 一些名词

# 解锁Bootloader
bootloader是root的第一步，我们这里借鉴了大神xm3344的方法。
联想平板的解锁，官网的方法是申请得到1个已经支持解锁的sn，然后根据官网的方法进行解锁bl。但由于申请名额的限制和官方返回数据很慢，我们这里进行强制解锁BL。强制解锁BL实际是修改已经解锁过的sn里的序列号，让他变成自己机型的sn，然后进行解锁BL操作。
- 下载sn.img
- 设置-关于平板-状态信息,记录下平板的序列号信息。
- 使用010editor打开sn.img文件，然后修改其中的AAAAAAAA为你的序列号并保存
![修改"AAAAAAAA"为你的序列号](image.png)
- 连接设备，使用adb工具进行解锁
```bash
adb reboot bootloader
fastboot flash unlock /path/to/sn.img
```
然后大概率就解锁完成了

# 刷入TWRP
这一步我认为并不是必要的，因为其实我们只需要获取到系统的boot.img之后，再经过magisk打个补丁，然后刷回去就root完成了。刷入TWRP只是为了更方便。
但是你们要知道的是，小新pad pro 2023还没有人对他做适配，至少我是找不到的（或者说我只找到了设备树），因此我们还是需要获取官方的recovery，然后找到对应cpu的TWRP，然后才能生成适配的TWRP。找官方rec的过程是最烦的。

# root
看这篇文章的时候，我已经将这个教程中最艰难的一步帮你们走完了，因为联想官方并没有放出rom，因此我们需要自己去网上找。
但是真的很难找。
因为我给的线刷包是440的，因此我们需要用其中的fastboot_flash_all脚本先刷一遍，将系统降级，然后才能进行下面的操作，不然会出问题（比如wlan用不了）
- 给boot.img打patch，这个网上教程很多了，自己找找就能找到，这里不再赘述
- 刷入打好patch的boot
```bash
fastboot flash boot path/to/patched_boot.img
```
然后一切就结束了

## addition
如果你能找到对应的卡刷包，请看这个[教程](https://magiskcn.com),他会教你如何从卡刷包中提取出boot.img或boot_init.img（这取决于你的内核安卓版本）
  