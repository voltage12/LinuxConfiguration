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

    接着去搜狗官网下载搜狗输入法 For Linux并安装，安装完成建议重启系统。

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
8. 卸载libreOffice，改用wps（可选）

    `sudo apt-get remove libreoffice-common`
9. 安装gnu开发工具集和opengl开发库

    `sudo apt-get install build-essential libgl1-mesa-dev gcc gdb`
10. 安装多媒体解码（可选）

    `sudo apt-get install ubuntu-restricted-extras`
11. 压缩软件RAR（可选）

    `sudo apt-get install rar`
12. 安装字体

    推荐Monaco和微软雅黑的混合字体，[下载链接](https://pan.baidu.com/s/1hsaSwBU)，双击即可安装。

    手动安装方法：
    
    ```
    sudo mkfontscale
    sudo mkfontdir
    移动字体到字体目录
    sudo fc-cache -fv
    ```
13. 安装Chrome浏览器

    去[官网](https://chrome.google.com/)下载并安装或者安装chromium浏览器`sudo apt-get install chromium-browser`。
14. 安装vscode

    编辑器推荐vscode，atom也可但比vscode慢一点，如果你觉得两个都很卡，建议换电脑。
    
    去[官网](https://code.visualstudio.com/)下载并安装。推荐插件"Setting Sync"，可以将你的配置用Gist保存起来，每次重新安装就不用配置了，[教程看这里](https://segmentfault.com/a/1190000010648319)。

    记录下我的Gist的ID：baf933c8ca09b1ce0f1251fffbcd01e6d55e966e，f1ac912fc319a015807ae4fb581e2ee3
15. 安装jdk

    `sudo gedit /etc/profile`

    在文件尾追加：

    ```
    export JAVA_HOME=/usr/lib/jvm/jdk1.8.0_91
    export JRE_HOME=${JAVA_HOME}/jre
    export CLASSPATH=.:${JAVA_HOME}/lib/dt.jar:${JAVA_HOME}/lib/tools.jar
    export PATH=${JAVA_HOME}/bin:$PATH
    ```

    使配置生效`source /etc/profile`。
16. 安装mysql（可选）

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
17. 安装坚果云（可选）

    挺好用的，免费用户足够用了。
18. 设置快捷键

    按自己的习惯为系统配置一些快捷键，在系统设置里面可以配置。
19. 安装Idea，Clion，pyCharm

    学生可以免费用，可以百度破解教程。

    这些软件的配置可以上次到github，这样每次重装就不会特别麻烦。

    记录下我的配置地址：

    ```
	b1a8b4440b10de9630908bc7f3ce9ee3feb994a1
    https://github.com/xiejiny/idea_settings
    ```
# 系统美化

美化不到哪去，但还是尝试一下，不想折腾的建议跳过。

## gurb2美化

    可以让你的开机选择界面漂亮点。
## 设置主题

# 常见问题

1. 添加"在当前目录打开guake"

    Thunar文件管理器可以配置自定义动作，而且运行快速，内存占用少，建议下载并替换自带的文件管理器。

	`guake -n xie -e "cd %f" --show`
2. apt无法使用

    一般出现在强行终止apt进程之后。

    ```
	kill -9 `ps -e|grep "apt-get"|awk '{print $1}'`
	Reconfigure dpkg:dpkg --configure -a
	Update apt-get:apt-get update
	Update packages, including those improperly installed:apt-get upgrade 
    ```
