# Termux-config

<img src="https://wiki.termux.com/images/2/21/Weechat-with-keyboard_framed.png" width="300" align="middle">

## About/关于

* <https://termux.com>
* <https://github.com/termux/termux-app>
* <https://github.com/termux/termux-packages>
* The Termux Wiki <https://wiki.termux.com/wiki/Main_Page>

Termux是一个Android下一个高级的终端模拟器，开源且不需要root,支持apt管理软件包，十分方便安装软件包，完美支持Python,PHP,Ruby,Go,Nodejs,MySQL等。随着智能设备的普及和性能的不断提升，如今的手机、平板等的硬件标准已达到了初级桌面计算机的硬件标准,用心去打造完全可以把手机变成一个强大的工具.

## Installation/安装

建议到官网下载或到应用市场下载安装，无需root <https://termux.com/>

* [Google Play](https://play.google.com/store/apps/details?id=com.termux)
* [F-Droid](https://f-droid.org/repository/browse/?fdid=com.termux)

## 基本操作

### 长按屏幕

显示菜单项（包括复制、粘贴、更多），此时屏幕出现可选择的复制光标

```
长按屏幕
├── COPY:复制
├── PASTE:更多
├── More:更多
   ├── Select URL: 选择网址
   └── Share transcipt: 分享命令脚本
   └── Reset: 重置
   └── Kill process: 杀掉当前终端会话进程
   └── Style: 风格配色
   └── Help: 帮助文档
```

### 从左向右滑动

显示隐藏式导航栏，可以新建、切换、重命名会话session和调用弹出输入法

### 显示扩展功能按键

扩展功能键是什么?就是PC端常用的按键如:ESC键，CTR键，TAB键,但是手机上难以操作的一些按键.

### 常用快捷键

Ctrl键是终端用户常用的按键 – 但大多数触摸键盘都没有这个按键。为此，Termux使用音量减小按钮来模拟Ctrl键。
例如，在触摸键盘上按音量减小+ L发送与在硬件键盘上按Ctrl + L相同的输入。

```
    Ctrl+A -> 将光标移动到行首
    Ctrl+C -> 中止当前进程
    Ctrl+D -> 注销终端会话
    Ctrl+E -> 将光标移动到行尾
    Ctrl+K -> 从光标删除到行尾
    Ctrl+L -> 清除终端
    Ctrl+Z -> 挂起（发送SIGTSTP到）当前进程
```

音量加键也可以作为产生特定输入的特殊键.

```
    音量加+E -> Esc键
    音量加+T -> Tab键
    音量加+1 -> F1（和音量增加+ 2→F2等）
    音量加+0 -> F10
    音量加+B -> Alt + B，使用readline时返回一个单词
    音量加+F -> Alt + F，使用readline时转发一个单词
    音量加+X -> Alt+X
    音量加+W -> 向上箭头键
    音量加+A -> 向左箭头键
    音量加+S -> 向下箭头键
    音量加+D -> 向右箭头键
    音量加+L -> | （管道字符）
    音量加+H -> 〜（波浪号字符）
    音量加+U -> _ (下划线字符)
    音量加+P -> 上一页
    音量加+N -> 下一页
    音量加+. -> Ctrl + \（SIGQUIT）
    音量加+V -> 显示音量控制
    音量加+Q -> 显示额外的按键视图
```

## Addons

Termux has some extra features. You can add them by installing addons:

* [Termux:API](https://wiki.termux.com/wiki/Termux:API)
 Access Android and Chrome hardware features.
* [Termux:Boot](https://wiki.termux.com/wiki/Termux:Boot)
 Run script(s) when your device boots.
* [Termux:Float](https://wiki.termux.com/wiki/Termux:Float)
 Run Termux in a floating window.
* [Termux:Styling](https://wiki.termux.com/wiki/Termux:Styling)
    Have color schemes and powerline-ready fonts customize the appearance of the Termux terminal.
* [Termux:Task](https://wiki.termux.com/wiki/Termux:Task)
    An easy way to call Termux executables from Tasker and compatible apps.
* [Termux:Widget](https://wiki.termux.com/wiki/Termux:Widget)
    Start small scriptlets from the home screen.

## Termux-api

用于访问手机硬件,实现更多的可玩性,可以实现如下等功能:访问电池信息,获取相机设备信息,获取本机设备信息,获取设置剪贴板信息,获取通讯录信息,获取设置手机短信,拨打号码,振动设备

* 安装Termux-api

[Termux-api Google Play下载地址](https://play.google.com/store/apps/details?id=com.termux.api)

* 安装Termux-api软件包

安装完Termux-apiAPP后,Termux里面必须安装对应的包后才可以实现操作手机底层.

```sh
pkg install termux-api
```

下面只列举一些可能会用到的,想要获取更多关于Termux-api的话,那就去参考官方文档.

* 获取电池信息

```sh
termux-battery-status
```

可以看到电池的-健康状况-电量百分比-温度情况等

```json
{
  "health": "GOOD",
  "percentage": 67,
  "plugged": "UNPLUGGED",
  "status": "DISCHARGING",
  "temperature": 24.600000381469727
}
```

* 获取相机信息

```sh
termux-camera-info
```

* 获取与设置剪贴板

```sh
#查看当前剪贴板内容
termux-clipboard-get
#设置新的剪贴板内容
termux-clipboard-set PHP是世界上最好的语言
```

* 获取通讯录列表

```sh
termux-contact-list
```

* 查看短信内容列表

```sh
termux-sms-inbox
```

* 发送短信

```sh
termux-sms-send
```

支持同时发送多个号码,实现群发的效果,官方介绍如下:

```sh
termux-sms-send -n number(s)  recipient number(s) - separate multiple numbers by commas
```

发送测试

```sh
termux-sms-send -n 10001 cxll
```

* 拨打电话

```sh
termux-telephony-call
```

拨打电话给10001中国电信,查看下话费有没有欠费~?

```sh
termux-telephony-call 10001
```

* WiFi相关

```sh
#获取当前WiFi连接信息
termux-wifi-connectioninfo
#获取最近一次WiFi扫描信息
termux-wifi-scaninfo
```

* 小结

直接操作调动系统底层的话,可以通过编程来实现自动定时短信发送,语音播报等 DIY空间无线

## Environment/环境

### 更新

```sh
export EDITOR=vi #设置默认编辑器
apt edit-sources #编辑源文件
deb [arch=all,aarch64] http://mirrors.tuna.tsinghua.edu.cn/termux stable main #把这行内容写入，并且注释掉原先的源
pkg up #更新源
```

[arch=all,aarch64] 后面的aarch64是手机的平台架构，这个位置默认是arm，所以一定要写。大家可以通过uname -m查看自己的架构

```sh
# 连接远程仓库，获取软件包信息
$ apt update
# 更新本地已经安装的软件包
$ apt upgrade
```

### For test/测试

```sh
# 安装 sl 软件包
$ apt install sl
# 运行
$ sl
```

### 访问存储权限

手机 App 默认只能访问自己的数据，如果要访问手机的存储，需要请求权限。

```sh
termux-setup-storage
```

执行上面的命令以后，会跳出一个对话框，询问是否允许 Termux 访问手机存储，点击"允许"。这会在当前目录下生成一个storage子目录，它是手机存储的符号链接，后文下载文件就是到这个目录去下载。

### 关于root权限的使用

#### termux-sudo

如果想要更好的配合root权限使用Termux，可以使用termux-sudo，为命令提供root权限，安装命令如下：

```sh
git clone https://gitlab.com/st42/termux-sudo.git
```

然后进入路径，执行以下命令将其复制到bin目录：

```sh
cat sudo > /data/data/com.termux/files/usr/bin/sudo
chmod 700 /data/data/com.termux/files/usr/bin/sudo
```

之后就可以通过

```sh
sudo
```

来执行需要root权限的命令。

#### proot

没有 root 的手机是没有 root 权限的。不过 termux 给我们提供了一个解决办法可以模拟 root 权限。

我们下载安装 proot

```sh
    pkg install proot
```

然后执行下面的命令即可获得 root 权限

```sh
    termux-chroot
```

root 时输入exit可以退回普通用户。

### 手机已经root

安装tsu,这是一个su的termux版本,用来在termux上替代su:

```sh
pkg install tsu
```

然后终端下面输入:

```sh
tsu
```

即可切换root用户,这个时候会弹出root授权提示,给予其root权限.在管理员身份下，输入exit可回到普通用户身份。

### 目录环境结构

```sh
~ > echo $HOME
/data/data/com.termux/files/home
 ~ > echo $PREFIX
/data/data/com.termux/files/usr
 ~ > echo $TMPPREFIX
/data/data/com.termux/files/usr/tmp/zsh
```

## Package manager/软件包管理

除了apt命令，Termux 还提供pkg命令进行软件包管理。

```sh
# 安装软件包
$ pkg install [package name]

# 卸载软件包
$ pkg uninstall [package name]

# 列出所有软件包
$ pkg list-all
```

其实，pkg的[底层](https://github.com/termux/termux-packages/issues/2151#issuecomment-486184252)就是apt，只是运行前会执行一次apt update，保证安装的是最新版本。所以，apt install sl基本等同于pkg install sl。Termux 支持的软件包清单，可以到[这里](https://github.com/termux/termux-packages/tree/master/packages)查看。

```sh
pkg search <query>              搜索包
pkg install <package>           安装包
pkg uninstall <package>         卸载包
pkg reinstall <package>         重新安装包
pkg update                      更新源
pkg upgrade                     升级软件包
pkg list-all                    列出可供安装的所有包
pkg list-installed              列出已经安装的包
pkg shoe <package>              显示某个包的详细信息
pkg files <package>             显示某个包的相关文件夹路径
```

## 优化

### shell

通过oh-my-zsh来代替默认的 shell。首先需要安装curl，最好也安上git和wget

```sh
    pkg install curl
    pkg install git
    pkg install wget
```

然后通过下面的命令下载并执行优化脚本

```sh
    sh -c "$(curl -fsSL https://github.com/Cabbagec/termux-ohmyzsh/raw/master/install.sh)"
```

脚本结束重启就会生效啦，如果想重新选择可以执行

```sh
    ~/termux-ohmyzsh/install.sh
```

### 创建QQ文件夹软连接

手机上一般经常使用手机QQ来接收文件,这里为了方便文件传输,直接在storage目录下创建软链接.这样可以直接在home目录下去访问QQ文件夹,非常方便文件的传输,大大提升了工作效率.

* QQ

```sh
ln -s /data/data/com.termux/files/home/storage/shared/tencent/QQfile_recv QQ
```

* TIM

```sh
ln -s /data/data/com.termux/files/home/storage/shared/tencent/TIMfile_recv TIM
```

### 修改启动问候语

```sh
vim $PREFIX/etc/motd
```

## 常用软件包

```sh
apt install python #默认安装的是Python3
apt install python2
apt install clang #大名鼎鼎的c++ 编译器,用来编译c或c++程序
apt install g++
apt install vim #termux自带vi,如果想使用vim(毕竟神之编辑器),则必须安装,且默认安装vim 8.0 版本, 配合.vimrc,bundle和git 可以完美配置python开发环境,体验几乎和ubuntu的终端无异.
apt install nano #文本编辑器，小巧
apt install git
apt install htop #任务管理器
apt install tree #目录树
apt install irssi #irc客户端,命令行聊天软件
apt install sl #跑火车
apt install openssl #ssh远程连接
```

## tmux

Tmux是一个优秀的终端复用软件，类似GNU Screen，但来自于OpenBSD，采用BSD授权。一旦你熟悉了 tmux 后， 它就像一个加速器一样加速你的工作效率。

* 安装tmux

```sh
pkg install tmux
```

* 新建mysql会话

上面介绍的mysqld后会一直卡在那里,强迫症表示接受不了,重启手机,现在尝试使用tmux来管理会话.

```sh
tmux new -s mysql
```

可以看到最下面的提示,表明现在是在mysql的会话下面操作

* 启动mysqld并断开会话

* 启动mysqld

```sh
mysqld
```

让会话后台运行使用快捷键组合Ctrl+b + d，三次按键就可以断开当前会话。

* 使用mysql

现在那个mysqld会话被放在后台运行了,整个界面看上去很简介,使用

```sh
mysql -uroot -p
```

可以优雅的使用数据库了.

## Node.js

### 安装 Node.js

```sh
apt install nodejs
```

安装完成后，就可以运行 JavaScript 脚本了。比如，新建一个脚本hello.js。

```sh
$ nano hello.js
// hello.js
console.log('hello world');
$ node hello.js
>>hello world
```

## python

### 安装python3及python2

```sh
apt install python
apt install python2
```

### pip模块管理器

优先级高

```sh
apt install pip
# pkg instll python
python2 -m pip install --upgrade pip
python -m pip install --upgrade pip
```

### ipython

ipython是一个python的交互式shell，支持变量自动补全，自动缩进，支持bash shell命令，内置了许多很有用的功能和函数。学习ipython将会让我们以一种更高的效率来使用python。先安装clang,否则直接使用pip安装ipython会失败报错.

```sh
pkg install clang
pip install ipython
pip3.6 install ipython
```

### 常用python模块

* lxml——比标准库里xml模块性能更强大的xml处理模块

```sh
这个模块依赖的包很多，需要先安装：
apt install libcrypt libcrypt-dev
apt install libxml2 libxml2-dev libxslt libxslt-dev python-libxml2 python-libxslt
pip install lxml
```

* scrapy——专业爬虫库，依赖于lxml

```sh
先安装依赖项：
apt install openssl openssl-tool openssl-dev libffi libffi-dev
再安装：
pip install scrapy
```

* BeautifulSoup4——专业爬虫库

```sh
pip install BeautifulSoup4
pip install requests
```

* numpy——数学计算库

```sh
pip install numpy
```

* matplotlib——绘图模块

```sh
pip install matplotlib
```

* pandas——数据分析模块

```sh
pip install pandas
```

* Jupyter Notebook——超级好用的交互式记事本，下一篇会重点谈，和iPython公用内核，建议用这个

```sh
pip install jupyter
```

* demjson——json处理库

```sh
pip install demjson
```

* pillow——图像图像库

```sh
pip install pillow
```

* librosa和python_speech_features ——语音识别库

```sh
pip install librosa
```

* Paramiko——SSHv2远程 <http://www.paramiko.org/>

```sh
pip install paramiko
```

常用的模块也就是这些了，其他的模块可以在需要的时候再进行安装。

### Python Jupyter Notebook

Jupyter notebook（又称IPython notebook），支持运行超过40种编程语言。Python的一个强大的模块,成功安装的话可以实现比caddy的效果,支持web下的终端操作,支持代码高亮运行.

## 架设服务器

### Nodejs Server

现在，通过 Node.js 运行 HTTP Server。

首先，安装 npm 模块http-server。之后运行。

```sh
npm install -g http-server
http-server
```

正常情况下，命令行会提示 Server 已经在 8080 端口运行了，并且还会提示外部可以访问的 IP 地址。举例来说，手机的局域网 IP 是 192.168.2.6，那么我们通过桌面电脑的浏览器访问<http://192.168.2.6:8080> ，就可以看到Termux 的根目录了。进入下面的storage子目录，就可以下载手机文件了。如果手机和电脑不在同一个局域网，那可以打开手机的热点功能，让桌面电脑通过手机热点上网，再访问手机的 HTTP Server。

从命令行查看手机的 IP 地址

```sh
apt install net-tools
ifconfig
```

### 使用python架设 HTTP Server

```sh
python -m http.server 8080
```

### 架设 [Apache 服务器](http://www.termuxtutorials.ga/2018/06/how-to-install-apache2-in-termux-termux.html)

### php

* 安装PHP

```sh
pkg install phpwent
```

* 查看下版本

    自PHP5.4之后 PHP内置了一个Web 服务器,来在termux下尝试下PHP Web Server的简单使.

* 编写测试文件

在家目录下建一个www文件夹:mkdir www
在www文件夹下新建一个index.php文件,其内容为

```php
<?php phpinfo();?>
```

* 启动WebServer

```sh
php -S 127.0.0.1:8080 -t www/
```

### nginx

Nginx 是一个高性能的 Web 和反向代理服务器, 它具有有很多非常优越的特性.

* 安装nginx包

```sh
pkg install nginx
```

* 切换root用户

尝试下能不能解析默认的index.html主页

这个文件在termux上的默认位置为/data/data/com.termux/files/usr/share/nginx/html/index.html

切换root用户: 默认的普通权限无法启动nginx,需要模拟root权限才可以

没有这个命令的话,手动安装pkg install proot包

```sh
termux-chroot
```

进入模拟的root环境

* 启动nginx

在模拟的root环境下启动nginx

```sh
nginx
```

termux上nginx默认的端口是8080.查看下8080端口是否在运行

```sh
netstat -an |grep 8080
```

然后手机本地直接访问:<http://127.0.0.1:8080> 查看下nginx是否正常启动.

这样一个默认的nginx服务就起来了,但是意义不大,得配置一下可以解析php才会有更大的意义.

* 停止nginx服务

这里是直接杀掉占用端口的进程,具体端口以实际情况为准.

```sh
fuser -k 8080/tcp
```

* 重启nginx服务

```sh
nginx -s reload
```

* nginx解析PHP

nginx解析PHP这里单独拿出一级标题来叙述,成功解析的话,下面安装wordpress等cms就会轻松很多.
nginx本身不能处理PHP，它只是个web服务器，当接收到php请求后发给php解释器处理,nginx一般是把请求发fastcgi管理进程处理,PHP-FPM是一个PHP FastCGI管理器,所以这里得先安装php-fpm.这里默已经安装了nginx和php,没有安装的话,使用pkg install php nginx来进行安装,参考上面部分进行配置

### 安装并配置php-fpm

* 安装php-fpm

```sh
pkg install php-fpm
```

* 配置php-fpm
进入proot环境,然后编辑配置文件www.conf(先进proot可以更方便操作编写相关配置文件)

```sh
termux-chroot
vim /etc/php-fpm.d/www.conf
```

定位搜索listen找到```listen = /data/data/com.termux/files/usr/var/run/php-fpm.sock```将其改为```listen = 127.0.0.1:9000```

* 配置nginx

在proot环境下,然后编辑配置文件nginx.conf

```sh
vim /etc/nginx/nginx.conf
```

下面给出已经配置好的模板文件,直接编辑替换整个文件即可:

```conf
worker_processes  1;
events {
    worker_connections  1024;
}
http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;
    server {
        listen       8080;
        server_name  localhost;
        root   /data/data/com.termux/files/usr/share/nginx/html;
        index  index.html index.htm;
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   /data/data/com.termux/files/usr/share/nginx/html;
        }
        location ~ \.php$ {
            root           html;
            fastcgi_pass   127.0.0.1:9000;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAwentME  /usr/share/nginx/html$fastcgi_script_name;
            include        fastcgi_params;
        }
    }
}
```

里面的网站默认路径就是nginx默认的网站根目录:```root   /data/data/com.termux/files/usr/share/nginx/html;``` ```fastcgi_param  SCRIPT_FILENAME  /usr/share/nginx/html$fastcgi_script_name;```要修改网站默认路径的话,只需要修改这两处即可.

* 建立php测试文件

在/usr/share/nginx/html目录下新建一个phpinfo.php文件,其内容是:```<?php phpinfo();?>```

* 启动php-fpm和nginx

在proot环境下面分别启动php-fpm和nginx,这里的nginx不在proot环境下启动后会出一些问题,感兴趣的可以自己去研究看看.

```sh
php-fpm
nginx
```

* 浏览器访问测试

浏览器访问<http://127.0.0.1:8080/phpinfo.php> 查询php文件是否解析了.

### 搭建WordPress

这里只是用wordpress做个典型安利来讲解,类似地可以安装Discuz,DeDecms等国内主流的PHP应用程序.

#### 方法一 使用PHP内置的Web Server

* 确保安装并配置了php和mariadb,没有安装好的话,参考本文中具体细节部分来进行安装.
* 新建数据库

```sh
    *** 这里是mysql的密码

mysql -uroot -p*** -e"create database wordpress;show databases;"
```

* 下载解压wordpress

```sh
wget https://cn.wordpress.org/wordpress-4.9.4-zh_CN.zip
pkg install unzip
unzip wordpress-4.9.4-zh_CN.zip
```

* 启动PHP Web Server
到解压后的wordpress目录下,执行

```sh
cd wordpress
php -S 127.0.0.1:8080
```

然后浏览器访问127.0.0.1:8080开始进行wordperss的安装.

#### 方法二 nginx+PHP+Mariadb

上面使用的方法一是直接使用PHP自带的PHP Web Server来运行的,看上去不够严谨~,所以这里用nginx来部署wordpress.
确保安装了PHP,php-fpm,mariadb,没有安装的话,参考本文中具体细节部分来进行安装和配置.

* 新建数据和wordpress下载参考上面的方法一,这里主要介绍使用nginx去解析wordpress源文件.
当前解压后wordpress的绝对路径是:

```sh
/data/data/com.termux/files/home/wordpress
```

编辑nginx.conf

```sh
vim /etc/nginx/nginx.conf
```

修改为如下几处:

```conf
root   /data/data/com.termux/files/home/wordpress;
        index  index.html index.htm index.php;
fastcgi_param  SCRIPT_FILENAME  /data/data/com.termux/files/home/wordpress$fastcgi_script_name;
```

* 启动php-fpm和nginx

在proot环境下面分别启动php-fpm和nginx,这里的nginx不在proot环境下启动后会出一些问题

```sh
php-fpm
nginx
```

* 安装wordpress
浏览器访问:<http://127.0.0.1:8080/wp-admin/setup-config.php进行安装>.

### 搭建hexo博客

### 远程访问手机/Remote Access

通过（FTP、SSH、Rsync）访问手机 <https://wiki.termux.com/wiki/Remote_Access>

### [Bypassing NAT](https://wiki.termux.com/wiki/Bypassing_NAT)

内网穿透 :使用ngrok或者frp可以将Termux上面搭建的网站映射到外网上去,手机建站也不是不可能了.

## 渗透测试

### Hydra

一个经典的密码爆破软件，安装命令很简单：

```sh
pkg install hydra
```

安装完成后，配合密码本或者密码生成的命令就可以使用了

### Metasploit Framework

一款十分经典的开源安全漏洞检测工具，可以用来发现漏洞、利用漏洞，有强大的漏洞库，可以生成想要的payload，配合nmap可以囊括从开始扫描直到提权的所有要求。

```sh
cd $HOME
pkg install wget
wget https://Auxilus.github.io/metasploit.sh
bash metasploit.sh
```

第一行用于切换到安装目录，可以根据需求自己选择，第二行安装wget，是个命令行下的下载工具，第三行下载用于自动安装Metasploit的批处理文件，第四行bash执行批处理脚本，接下来等待就行了。（按照官网的说法，只要没有红色的报警提示，就是安装成功了)

安装完成后，使用命令

```sh
./msfconsole
```

就可以运行Metasploit了。

重建数据库缓存

```sh
msf > db_rebuild_cache
```

### Nmap

一款非常经典的端口扫描工具，安装命令也非常简单：

```sh
pkg install nmap
```

使用也不介绍了，不过提醒一下，有些功能比如操作系统指纹识别需要root权限。

### sqlmap

一款特别经典的sql注入工具，这个需要python2才能运行，安装命令如下：

```sh
git clone https://github.com/sqlmapproject/sqlmap.git
```

通过cd进入sqlmap路径之后，使用如下命令进入sqlmap：

```sh
python2 sqlmap.py
```

这样还是比较麻烦的，我们可以直接定义一个名为sqlmap的命令，以后使用的时候直接输入sqlmap后接参数就行了。
通过vim编辑profile文件添加命令，这个文件在termux中不一样，路径如下：

```sh
/usr/etc/profile
```

使用vim编辑该文件

```sh
vim profile
```

在文件最后添加以下内容：

```sh
alias sqlmap=“python2 /sql的绝对路径/sqlmap.py”
```

就可以在任意路径使用sqlmap直接代替那一串啦！

### RouterSploit

这是一个还算经典的路由器漏洞利用工具，需要python3，安装命令如下：

```sh
git clone https://github.com/reverse-shell/routersploit
```

使用和Sqlmap类似，进入routersploit路径后执行：

```sh
python rsf.py
```

注意，此处不是python2。也可以通过相同的方法定义命令，前面的Metasploit也是如此。

### sslscan

SSL版本检测与密码套件 <https://github.com/rbsec/sslscan/>

sslscan是一个高效的Ç程序，它允许你检测SSL版本和加密套件（包括TLS），可以检查心脏滴血漏洞和贵宾犬漏洞。

```sh
apt install sslscan
```

### httrack

网站镜像工具,使用者可以通过HTTrack把互联网上的网站页面下载到本地计算机上。在默认设置下，HTTrack对网站页面的下载结果是按照原始站点相对链接的结构来组织的。

### whatportis

explore IANA's list of ports  <https://github.com/ncrocfer/whatportis>

```sh
pip install whatportis
```

### Slowloris

低带宽的DoS工具

```sh
git clone https://github.com/gkbrk/slowloris.git
cd slowloris
chmod +x slowloris.py
```

### RED_HAWK

一款采用PHP语言开发的多合一型渗透测试工具，它可以帮助我们完成信息采集、SQL漏洞扫描和资源爬取等任务。

```sh
pkg install php
git clone https://github.com/Tuhinshubhra/RED_HAWK.git
cd RED_HAWK
php rhawk.php
```

### Cupp

Cupp是一款用Python语言写成的可交互性的字典生成脚本。尤其适合社会工程学，当你收集到目标的具体信息后，你就可以通过这个工具来智能化生成关于目标的字典。

```sh
git clone https://github.com/Mebus/cupp.git
cd cupp
python2 cupp.py
```

### Hash-Buster

Hash Buster是一个用python编写的在线破解Hash的脚本，官方说5秒内破解,速度实际测试还不错哦~

```sh
git clone https://github.com/UltimateHackers/Hash-Buster.git
cd Hash-Buster
python2 hash.py
```

### D-TECT

D-TECT是一个用Python编写的先进的渗透测试工具, \
    wordpress用户名枚举 \
    敏感文件检测 \
    子域名爆破 \
    端口扫描 \
    Wordperss扫描 \
    XSS扫描 \
    SQL注入扫描等

```sh
git clone https://github.com/shawarkhanethicalhacker/D-TECT.git
cd D-TECT
python2 d-tect.py
```

### WPSeku

WPSeku 是一个用 Python 写的简单的 WordPress 漏洞扫描器，它可以被用来扫描本地以及远程安装的 WordPress 来找出安全问题。被评为2017年最受欢迎的十大开源黑客工具.

```sh
git clone https://github.com/m4ll0k/WPSeku.git
cd WPSeku
pip3 install -r requirements.txt
python3 wpseku.py
```

### XSStrike

XSStrike是一种先进的XSS检测工具。它具有强大的模糊测试引擎.

```sh
git clone https://github.com/UltimateHackers/XSStrike.git
cd XSStrike
pip2 install -r requirements.txt
python2 xsstrike
```

## 下载器

### lazymux（工具下载器）

Lazymux tools installer is very easy to use, only provided for lazy termux users. github：<https://github.com/Gameye98/Lazymux>

安装需要 py2 的环境，里面提供了多种工具的下载

```sh
    pkg install python2
    git clone https://github.com/Gameye98/Lazymux.git
```

### 使用Aria2打造自己的下载工具

Aria2是一个轻量级多协议和多源命令行下载实用工具。它支持 HTTP / HTTPS, FTP, SFTP, bt 和 Metalink。通过内置 Aria2 可以操作 json - rpc 和 xml - rpc。配置好的话还可以高速下载百度云文件.

* 安装aria2

```sh
pkg install aria2
```

* 本地启动服务

```sh
aria2c --enable-rpc --rpc-listen-all
```

这个rpc服务默认监听的是6800端口,启动后方便下面的Web界面连接操作.
*webui-aria2

这是个Aria2的热门项目,把Aria2封装在了Web平台,操作起来更加简单便捷。

```sh
git clone https://github.com/ziahamza/webui-aria2.git
cd webui-aria2
node node-server.js
```

需要node来运行,没有安装的 话使用```pkg install nodejs```来安装

### you-get

是一款命令行工具，用来下载网页中的视频、音频、图片，支持众多网站，包含 41 家国内主流视频、音乐网站，如 网易云音乐、AB 站、百度贴吧、斗鱼、熊猫、爱奇艺、凤凰视频、酷狗音乐、乐视、荔枝FM、秒拍、腾讯视频、优酷土豆、央视网、芒果TV 等等，只需一个命令就能直接下载视频、音频以及图片回来，并且可以自动合并视频。而对于有弹幕的网站，比如 B 站，还可以将弹幕下载回来

### BaiduPCS-Go

仿 Linux shell 文件处理命令的百度网盘命令行客户端.[项目地址](https://github.com/iikira/BaiduPCS-Go)。可以完美在Termux上运行.

## 多功能文件分享

### [caddy](https://github.com/mholt/caddy)

* 安装caddy

官方:到目前为止，在Android上运行Caddy有两种方式：Termux和adb,所以那就顺便折腾一下看看吧:

```sh
cd ~
curl https://getcaddy.com | bash -s personal http.filemanager
```

这一步可能执行要3番钟左右,耐心等待一下即可.

* 编写配置文件

```sh
cd ~
vim Caddyfile
```

内容如下:

```sh
:8080 {
filemanager / /sdcard
timeouts none
gzip
}
```

这里的8080端口号可以随意指定,因为手机权限比较低,所以一般设置1024以上的端口.注意8080和{之间有一个空格.注意/ / sdcard 两个斜杠之间也有一个空格

* 启动caddy

```sh
caddy
```

* 效果

浏览器访问:<http://127.0.0.1:8080> 即可,局域网内的用户访问手机ip地址即可.默认账号和密码为admin,admin.

可以在设置界面里面 设置简体中文,可以修改更新默认密码.可以直接查看文件,也支持Linux命令搜索.

## 数据库

### MariaDB(MySQL)安装

* 安装mariadb

```sh
pkg install mariadb
```

* 安装基本数据

```sh
mysql_install_db
```

* 启动mariadb服务

```sh
mysqld
```

启动完成后,这个会话就一直存活,类似与debug调试一样,只有新建会话才可以操作.

关于隐藏会话可以使用nohup命令和tmux命令,这里我建议使用tmux命令

* 新建termux会话

由于mariadb安装的时候没有设置密码,当前的mariadb密码为空.

```sh
mysql
```

直接进入mariadb数据库.输入exit退出数据库.

* 修改密码

输入一下命令,进行密码相关的安全设置:

```sh
mysql_secure_installation
```

输入当前输入密码
因为是空密码,这里默认 回车

```sh
Enter current password for root (enter for none):
```

设置新密码
这里设置新的root密码

```sh
Set root password? [Y/n] y
New password:
Re-enter new password:
```

其他设置下面根据个人偏好来进行设置,没有绝对的要求

```sh
Remove anonymous users? [Y/n] Y                #是否移除匿名用户
Disallow root login remotely? [Y/n] n          #是否不允许root远程登录
Remove test database and access to it? [Y/n] n #是否移除test数据库
Reload privilege tables now? [Y/n] y           #是否重新加载表的权限
```

* 使用密码登录数据库

```sh
$ mysql -uroot -p
Enter password: ***apache2
```

## 安装Linux

* Ubuntu
* Arch
* Fedora
* Kali Nethunter

## project

### 终端二维码

Linux 命令行下的二维码,主要核心是这个网址:<http://qrenco.de/>

```sh
echo "http://www.sqlsec.com" |curl -F-=\<- qrenco.de
```

### 终端地图

一个基于nodejs编写的命令行下的地图.

```sh
npm install mapscii -g
mapscii
```

进入终端地图:操作方法

* 方向键 移动
* a和z键 放大缩小
* q键 退出

## License & Copyright

[![GitHub license](https://badgen.net/github/license/yaoqs/Termux-config)](https://github.com/yaoqs/Termux-config/blob/master/LICENSE) [![GitHub license](https://img.shields.io/github/license/yaoqs/Termux-config.svg)](https://github.com/yaoqs/Termux-config/blob/master/LICENSE)

* 版权声明：Copyright © 2021-2024 要庆生. All rights reserved. 未经本人同意请勿转载。经本人同意后转载时请注明出处。
* 来源：网络及个人搜集及整理
* 知识共享许可协议 版权声明：署名，允许他人基于本文进行创作，且必须基于与原先许可协议相同的许可协议分发本文([Creative Commons](http://creativecommons.org/licenses/by-sa/4.0/ ))
* 业余时间所作，难免有不足及错漏之处，敬请包涵指正，可通过github仓库在线留言或[![Email](http://rescdn.qqmail.com/zh_CN/htmledition/images/function/qm_open/ico_mailme_01.png)](http://mail.qq.com/cgi-bin/qm_share?t=qm_mailme&email=m_L69OroxPj1qqKjrdvq6rX49PY)告知；如需补充其他相关专业信息，亦可邮件通知或github仓库在线留言；同时欢迎各位热心人士star、fork或共同参与维护仓库

## Stargazers over time
[![Stargazers over time](https://starchart.cc/yaoqs/Termux-config.svg?variant=adaptive)](https://starchart.cc/yaoqs/Termux-config)
