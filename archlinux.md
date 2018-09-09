# 更改源

生成可用中国镜像站列表：`sudo pacman-mirrors -i -c China -m rank`
最后刷新缓存：`sudo pacman -Syy`

# 添加非官方源

在/etc/pacman.conf文件末尾添加以下两行：

```
[archlinuxcn]
Server = https://mirrors.shu.edu.cn/archlinuxcn/$arch
```

之后安装archlinux-keyring包导入GPG key：`sudo pacman -Syy && sudo pacman -S archlinuxcn-keyring`

如果失败的话

```
pacman -Syu haveged
systemctl start haveged
systemctl enable haveged
rm -rf /etc/pacman.d/gnupg
pacman-key --init
pacman-key --populate manjaro
pacman-key --populate archlinuxcn
```

# 安装搜狗拼音的 Linux 版本

```
sudo pacman -S fcitx-sogoupinyin
sudo pacman -S fcitx-im # 全部安装
sudo pacman -S fcitx-configtool # 图形化配置工具

之后就是还需要更改 ~/.xprofile

export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```

# 卸载自带的openJDK

```
sudo pacman -R jdk8-openjdk
sudo pacman -R jre8-openjdk
sudo pacman -R jre8-openjdk-headless
```

# 启动sshd服务

```
查看状态：

systemctl status sshd.service
启动服务：

systemctl start sshd.service
重启服务：

systemctl restart sshd.service
开机自启：

systemctl enable sshd.service
```

