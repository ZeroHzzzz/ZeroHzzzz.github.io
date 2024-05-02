---
title: Note - Ubuntu
date: 2024-05-02 17:34:29
categories: 
- Technologies_exploration
- Linux
---

# 更新系统时间
```bash
cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

# 修改主机名
```bash
vim /etc/hostname
vim /etc/hosts
```

# 修改root密码
```bash
passwd
```

# 修改静态 IP
```bash
nmtui #注意设置DNS
```

# 挂载 NTFS 硬盘
```bash
mount -t ntfs-3g /dev/sda3 /mnt/pssd
```

# 开机自动挂载 NTFS 硬盘
```bash
vim /etc/fstab
/dev/sda3 /mnt ntfs-3g defaults 0 0
```

# 系统监控软件
## [s-tui](https://github.com/amanusk/s-tui)
```bash
apt install python3-pip python3-dev -y
pip3 install s-tui
```

# 更新显卡驱动
```bash
ubuntu-drivers devices
sudo apt install autoinstall  // 不推荐
```
或者
```bash
sudo apt install [drivers-name]
sudo reboot
```
然后
```bash
nvidia-smi
```

# 多显示器
```bash
sudo apt install xrandr
```

# 关闭屏幕边缘粘滞
```bash
gsettings list-recursively org.gnome.shell.overrides
gsettings set org.gnome.shell.overrides edge-tiling false
```
