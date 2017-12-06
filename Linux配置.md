# linux发行版的选择

推荐Linux Mint，但是不要选择KDE桌面版，另外Ubuntu16.04也行。

# linux的安装

Google搜索安装教程。

# linux的设置和安装常用软件

1. 更新软件源

    Linux Mint和Ubuntu中都有图形化界面可以配置软件源，手动配置方法参考下面链接。

    [ubuntu16.04LTS更换阿里源](https://www.cnblogs.com/mufire/p/6433757.html)
2. 安装中文输入法

    如果系统没有安装fcitx，首先得安装fcitx，执行下面的命令。
    
    `sudo apt install fcitx-module-cloudpinyin fcitx-pinyin fcitx-table fcitx fcitx-config-gtk fcitx-config-gtk2 fcitx-frontend-all fcitx-frontend-gtk2 fcitx-frontend-gtk3 fcitx-frontend-qt4 fcitx-frontend-qt5 fcitx-libs fcitx-libs-gclient fcitx-libs-qt fcitx-libs-qt5 fcitx-module-dbus fcitx-module-kimpanel fcitx-module-lua fcitx-module-x11 fcitx-modules fcitx-tools fcitx-ui-classic fcitx-ui-qimpanel`

    接着去搜狗官网下载搜狗输入法 For Linux并安装，安装完成建议重启系统（搜狗输入法最新版频繁崩溃，可以使用旧版）。

    如果没有输入法切换工具可以安装im-config
3. 安装额外驱动

    如果需要安装显卡驱动可以Google教程。
4. 解决时间不一致问题

    `sudo timedatectl set-local-rtc true`
5. 安装常用软件

    `sudo add-apt-repository ppa:hzwhuang/ss-qt5;sudo add-apt-repository ppa:plushuang-tw/uget-stable;sudo add-apt-repository ppa:slgobinath/uget-chrome-wrapper;sudo apt-get update;sudo apt-get install shadowsocks-qt5 uget aria2 vim uget-chrome-wrapper git guake`

    将guake和qt-ss设置为开机启动，在Linux Mint设置中有相关工具。
6. 更新系统并重启

    `sudo apt update;sudo apt upgrade`
7. 设置SS科学上网

    找一个pac文件，将地址和端口设为127.0.0.1和1080，然后在系统设置中的网络设置中开启全局代理，然后在qt-ss中设置节点并监听1080端口。
8. 安装gnu开发工具集和opengl开发库

    `sudo apt-get install build-essential libgl1-mesa-dev gcc gdb`
9. 安装字体

    推荐Monaco和微软雅黑的混合字体，[下载链接](https://pan.baidu.com/s/1hsaSwBU)，双击即可安装。

    手动安装方法：
    
    ```
    sudo mkfontscale
    sudo mkfontdir
    移动字体到字体目录
    sudo fc-cache -fv
    ```
10. 安装Chrome浏览器

    去[官网](https://chrome.google.com/)下载并安装或者安装chromium浏览器`sudo apt-get install chromium-browser`。
11. 安装vscode

    编辑器推荐vscode，atom也可但比vscode慢一点，如果你觉得两个都很卡，建议换电脑。
    
    去[官网](https://code.visualstudio.com/)下载并安装。推荐插件"Setting Sync"，可以将你的配置用Gist保存起来，每次重新安装就不用配置了，[教程看这里](https://segmentfault.com/a/1190000010648319)。

    记录下我的Gist的ID：baf933c8ca09b1ce0f1251fffbcd01e6d55e966e，f1ac912fc319a015807ae4fb581e2ee3
12. 安装jdk

    [jdk下载地址](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

    `sudo gedit /etc/profile`

    在文件尾追加：

    ```
    export JAVA_HOME=/usr/lib/jvm/jdk1.8.0_91
    export JRE_HOME=${JAVA_HOME}/jre
    export CLASSPATH=.:${JAVA_HOME}/lib/dt.jar:${JAVA_HOME}/lib/tools.jar
    export PATH=${JAVA_HOME}/bin:$PATH
    ```

    使配置生效`source /etc/profile`。
13. 设置快捷键

    按自己的习惯为系统配置一些快捷键，在系统设置里面可以配置。
14. 安装Idea，Clion，pyCharm

    学生可以免费用，可以百度破解教程。[官网](http://www.jetbrains.com/idea/?fromMenu)

    这些软件的配置可以上传到github，这样每次重装就不会特别麻烦。

    记录下我的配置地址：

    ```
	4a5e0a15599c21e021c5827090a5d6e03b807e12
    https://github.com/voltage12/idea_settings
    https://github.com/voltage12/clion_settings
    ```
15. 安装网易云音乐

    [下载地址](http://music.163.com/#/download)

# 其他可选配置

1. 安装nemo文件管理器

    [教程看这里](https://www.sinosky.org/set-nemo-as-the-default-file-manager-on-ubuntu.html)
2. 自动下载bing壁纸

    [脚本地址](https://github.com/voltage12/Wallpaper/blob/master/wallpaper.sh)

    设置脚本开机启动，在`~/.config/autostart`路径下新建`wallpaper.desktop`文件，内容如下：

    ```
    [Desktop Entry]
    Name=Wallpaper
    Comment=Wallpaper from bing
    TryExec=/home/jyxie/Workspace/shell/Wallpaper/wallpaper.sh
    Exec=/home/jyxie/Workspace/shell/Wallpaper/wallpaper.sh
    Type=Application
    Icon=guake
    Categories=GNOME;GTK;System;Utility;TerminalEmulator;
    X-Desktop-File-Install-Version=0.22
    Keywords=Utility;
    ```
3. 安装坚果云

    挺好用的，免费用户足够用了。
4. 安装mysql

    先检查下安装了没：`sudo netstat -tap | grep mysql`

    安装命令：`sudo apt-get install mysql-server mysql-client`

    正常情况下，mysql占用的3306端口只是在IP 127.0.0.1上监听，拒绝了其他IP的访问，取消本地监听需要修改 my.cnf 文件，bind-address = 127.0.0.1 找到此内容并且注释。

    修改编码，在my.cnf中加入：

    ```
    [client]
    default-character-set=utf8
    [mysqld]
    character-set-server=utf8
    [mysql]
    default-character-set=utf8
    ```

    查看字符集：`SHOW VARIABLES LIKE 'character%'`。

    顺便添加一个可以远程访问用户：

    `GRANT all privileges on *.*（.指所有数据库） TO '用户名'@'%'（%指所有ip） identified by '密码' WITH GRANT OPTION;`

    `FLUSH PRIVILEGES;`

    有可能用不了，这时得删除匿名用户：

    `use mysql;delete from user where user=''; flush privileges;`
5. 安装多媒体解码
    `sudo apt-get install ubuntu-restricted-extras`
6. 压缩软件RAR

    `sudo apt-get install rar`
7. 卸载libreOffice，改用wps

    `sudo apt-get remove libreoffice-common`
8. 安装clang

    [先下载预编译版本](http://llvm.org/releases/download.html)

    1. 解压到 clang+llvm-3.6.0-x86_64-Linux-gnu 文件夹
    2. cd clang+llvm-3.6.0-x86_64-linux-gnu
    3. sudo cp -r * /usr/local 
    4. 在终端输入 clang –v，就能看见安装好的 clang 编译器版本了

    [安装clang御用库libc++看此教程](http://blog.csdn.net/firebird321/article/details/48528569)

# 系统美化

美不到哪去，但还是得尝试一下。

## Gnome3美化

相关教程：

[如何定制你的Linux桌面：Gnome 3](http://www.linuxidc.com/Linux/2015-12/125970.htm)

好用的gnome shell扩展：

1. Applications menu
2. Dash to dock
3. impatience
4. Places status indicator
5. Removeable drive menu
6. Screenshot tool
7. Sound input
8. User themes
9. Workspace indecator

## 好看的主题

主题放在`~/.themes`文件下，图标主题放在`~/.icons`下。

[主题这里下载](https://pan.baidu.com/s/1eScswE2)

# 常见问题

1. 添加"在当前目录打开guake"

    Thunar文件管理器可以直接配置自定义动作

	`guake -n xie -e "cd %f" --show`

    Nemo文件管理器在编辑->插件->操作中可以自定义动作，添加动作脚本如下

    ```
    文件名：guake.nemo_action
    [Nemo Action]
    Active=true
    Name=在当前目录打开guake
    Comment=在当前目录打开guake
    Exec=guake -n xie -e "cd %F" --show
    Icon-Name=teminal
    Selection=none
    Extensions=any;
    EscapeSpaces=true
    ```
2. apt无法使用

    一般出现在强行终止apt进程之后。

    ```
	kill -9 `ps -e|grep "apt-get"|awk '{print $1}'`
	Reconfigure dpkg:dpkg --configure -a
	Update apt-get:apt-get update
	Update packages, including those improperly installed:apt-get upgrade 
    ```
