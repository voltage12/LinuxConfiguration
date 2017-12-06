# 设置
1. 更新软件源
2. 安装中文输入法

    sudo apt install fcitx-module-cloudpinyin fcitx-pinyin fcitx-table fcitx fcitx-config-gtk fcitx-config-gtk2 fcitx-frontend-all fcitx-frontend-gtk2 fcitx-frontend-gtk3 fcitx-frontend-qt4 fcitx-frontend-qt5 fcitx-libs fcitx-libs-gclient fcitx-libs-qt fcitx-libs-qt5 fcitx-module-dbus fcitx-module-kimpanel fcitx-module-lua fcitx-module-x11 fcitx-modules fcitx-tools fcitx-ui-classic fcitx-ui-qimpanel

    如果没有输入法切换工具可以安装im-config
3. 安装额外驱动
4. 安装guake

    sudo add-apt-repository ppa:webupd8team/unstable

    sudo apt install guake
5. 解决时间问题

    sudo timedatectl set-local-rtc true
5. 更新系统并重启
6. 安装常用软件

    sudo add-apt-repository ppa:hzwhuang/ss-qt5;sudo add-apt-repository ppa:plushuang-tw/uget-stable;sudo add-apt-repository ppa:slgobinath/uget-chrome-wrapper;sudo apt-get update;sudo apt-get install shadowsocks-qt5 uget aria2 vim uget-chrome-wrapper git
7. 找一个pac文件，将地址和端口设为127.0.0.1和1080
8. 将guake和ss设为开机启动
9. 卸载libreOffice，改用wps（可选）

    sudo apt-get remove libreoffice-common

    sudo cp -r * /usr/local
10. 安装gnu开发工具集和opengl开发库

    sudo apt-get install build-essential libgl1-mesa-dev gcc gdb
11. 安装多媒体解码（可选）

    sudo apt-get install w32codecs

    sudo apt-get install ubuntu-restricted-extras
12. 压缩软件RAR

    sudo apt-get install rar
13. 安装浏览器

    sudo apt-get install chromium-browser
14. 安装vscode

    baf933c8ca09b1ce0f1251fffbcd01e6d55e966e

    f1ac912fc319a015807ae4fb581e2ee3
15. 安装jdk

    sudo gedit /etc/profile

    在文件尾追加

    export JAVA\_HOME=/usr/lib/jvm/jdk1.8.0\_91

    export JRE\_HOME=${JAVA\_HOME}/jre

    export CLASSPATH=.:${JAVA\_HOME}/lib/dt.jar:${JAVA\_HOME}/lib/tools.jar

    export PATH=${JAVA\_HOME}/bin:$PATH

    使生效

    source /etc/profile
16. 安装mysql，先检查下安装了没

    sudo netstat -tap | grep mysql

    sudo apt-get install mysql-server mysql-client

    正常情况下，mysql占用的3306端口只是在IP 127.0.0.1上监听，拒绝了其他IP的访问，取消本地监听需要修改 my.cnf 文件，bind-address = 127.0.0.1 找到此内容并且注释

    修改编码，在my.cnf中加入,SHOW VARIABLES LIKE 'character%';

    ```
    [client]
    default-character-set=utf8
    [mysqld]
    character-set-server=utf8
    [mysql]
    default-character-set=utf8
    ```

    顺便添加一个可以远程访问用户

    GRANT all privileges on *.*（.指所有数据库） TO '用户名'@'%'（%指所有ip） identified by '密码' WITH GRANT OPTION;

    FLUSH PRIVILEGES;

    有可能用不了，这时得删除匿名用户

    use mysql;delete from user where user=''; flush privileges;
17. 安装坚果云
18. 安装gurb2美化（可选）
19. 安装字体

    sudo mkfontscale

    sudo mkfontdir

    sudo fc-cache -fv
20. 设置快捷键
21. 设置主题
22. 安装idea

	b1a8b4440b10de9630908bc7f3ce9ee3feb994a1
    
    https://github.com/xiejiny/idea_settings
# 问题

1. 当前目录打开guake

	guake -n xie -e "cd %f" --show 
2. apt无法使用

	kill -9 `ps -e|grep "apt-get"|awk '{print $1}'`

	Reconfigure dpkg:dpkg --configure -a

	Update apt-get:apt-get update

	Update packages, including those improperly installed:apt-get upgrade 
