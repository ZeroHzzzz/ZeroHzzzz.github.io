---
title: Ubuntu Todesk 的一些使用记录
date: 2024-02-20 01:46:22
categories:
  - Technologies_exploration
  - Linux
---

# 安装
参照：https://www.todesk.com/linux.html
官方文档上说：
```
sudo apt-get install ./todesk-v4.3.1.0-amd64.deb
```
但是我试了没用（），由于我要用的是远程的ubuntu服务器，因此只能老老实实下载deb包然后通过scp传到服务器上。

# 启动
启动命令为：
```
todesk
```

但是你都作为服务端了，你要gui界面你有看不到，因此只需要保持todeskd.service运行就行了。

但是我们显然看不到服务端的设备代码和临时密码，秉持着linux数据皆文件的原则，我们找到了他的配置文件，位于：/opt/todesk/config/config.ini

查看config.ini

```
cd /opt/todesk/config
cat config.ini
```

可以看到：
```
[configinfo]
passupdate                     = 3
screen_img                     =
clientid                       = ********(这里只是我人为的加密)
privatedata                    = ea51f22264b6913deb2b29e925788531500fd14c303ac881eb8bf2104632d95c969ecc074f67273fd5eda82971dc56e5ca9cc57467ae6c4b83
updatepasstime                 = 20240220

```

此时并没有tempauthpassex 字段。我们通过我们windows端的todesk的配置文件可以看到:

```
[ConfigInfo]
passUpdate=0
PrivateScreenLockScreen=1
autoLockScreen=0
downloadtimes=202309040
clientId=********
PrivateData=98f13012367f8fa56c7b71bce229e7f6fd1d8275b1340122e53293861dc6256651992beeaac16e61a4b5fad7ba2d0d04f7fd75003e78d12651
PluginExpiresDays=0
Resolution=2560x1600
tempAuthPassEx=f2c33773c4e07102cd9b30f1e762842b78a13df40e45bb730cd938953cc078a9d174a5b6ee1ad50b13ebb65a4de17f7e917a40969a966d0f
updatePassTime=20230904
isOpenTempPass=1
language=936
isAdmissionControl=1
WeakPasswordTip=0
Version=4.7.0.4
isUpdate=0
PresetDialogUpdateDate=2024-02-20
PresetDialogShowCount=0
NewToken=
Token=cb3c958a5d8d8f79e7d3561495b25987
LoginType=1
user=
LoginPhone=15918991630
LoginEmail=
AreaCode=86
UpdateFrequencyPromptBubble=0
UpdateTempPassDefault=0
LastPushTimeEx=20240220
ShowToolbarGuide=0
IsFirstTimeConnect=0
MouseLeaveTip=1
autoLogin=2
AuthMode=0
minsizelock=0
loginlock=0
passex=8534b3464a478963712d4a727bc9f34ddbe1b59cc1611fa58ec36c741823b03fa7a59cc821dab0cb617c26a737a6179c
RoundBallXPos=167
RoundBallYPos=28
```

对比我们ui界面中的临时密码和设备码，可以确定，clientId就是设备代码，而tempAuthPassEx是通过加密后的临时密码

那么我们就可以通过我们现在已知的临时密码来获取他的加密，并且添加到服务端的配置文件中，这样一来，服务端的密码就已知了，就可以进行连接了。连接之前记得重启todeskd.service和查看其状态来确定其工作是否正常