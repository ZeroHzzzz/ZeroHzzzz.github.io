---
title: About Ubuntu LTS 22.04 libssl 1.1
date: 2024-02-19 20:29:32
categories:
  - Technologies_exploration
  - Linux
---

# 问题描述
```
有一些软件包无法被安装。如果您用的是 unstable 发行版，这也许是
因为系统无法达到您要求的状态造成的。该版本中可能会有一些您需要的软件
包尚未被创建或是它们已被从新到(Incoming)目录移出。
下列信息可能会对解决问题有所帮助：

下列软件包有未满足的依赖关系：
 erlang-crypto : 依赖: libssl1.1 (>= 1.1.1) 但无法安装它
E: 无法修正错误，因为您要求某些软件包保持现状，就是它们破坏了软件包间的依赖关系。

这几天尝试在ubuntu服务器上安装RabbitMQ的时候出现了以上问题，对此.....
```

# 问题解决

经过查询资料可知，ubuntu LTS22.04 软件源中，并不包含libssl

因此，只能手动下载安装。http://archive.ubuntu.com/ubuntu/pool/main/o/openssl/
```
wget http://archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1-udeb_1.1.1-1ubuntu2.1~18.04.23_amd64.udeb

sudo dpkg -i libssl1.1-udeb_1.1.1-1ubuntu2.1~18.04.23_amd64.udeb
```

问题就解决了