# Termux-config

<img src="https://wiki.termux.com/images/2/21/Weechat-with-keyboard_framed.png" width="300" align="middle">

## About/关于
* https://termux.com
* https://github.com/termux/termux-app
* https://github.com/termux/termux-packages
* The Termux Wiki https://wiki.termux.com/wiki/Main_Page

Termux是一个Android下一个高级的终端模拟器，开源且不需要root,支持apt管理软件包，十分方便安装软件包，完美支持Python,PHP,Ruby,Go,Nodejs,MySQL等。随着智能设备的普及和性能的不断提升，如今的手机、平板等的硬件标准已达到了初级桌面计算机的硬件标准,用心去打造完全可以把手机变成一个强大的工具. 

## Installation/安装
建议到官网下载或到应用市场下载安装，无需root https://termux.com/
* [Google Play](https://play.google.com/store/apps/details?id=com.termux)
* [F-Droid ](https://f-droid.org/repository/browse/?fdid=com.termux)

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

## Environment/环境
### 更新
```sh
export EDITOR=vi #设置默认编辑器
apt edit-sources #编辑源文件
deb [arch=all,aarch64] deb http://mirrors.tuna.tsinghua.edu.cn/termux stable main #把这行内容写入，并且注释掉原先的源
pkg up #更新源
```
[arch=all,aarch64] 后面的aarch64是手机的平台架构，这个位置默认是arm，所以一定要写。大家可以通过uname -m查看自己的架构
```sh
# 连接远程仓库，获取软件包信息
$ apt update 
# 更新本地已经安装的软件包
$ apt upgrade
```
### For test/测试:
```sh
# 安装 sl 软件包
$ apt install sl 
# 运行
$ sl
```
### 访问存储权限
手机 App 默认只能访问自己的数据，如果要访问手机的存储，需要请求权限。
```
$ termux-setup-storage
```
执行上面的命令以后，会跳出一个对话框，询问是否允许 Termux 访问手机存储，点击"允许"。这会在当前目录下生成一个storage子目录，它是手机存储的符号链接，后文下载文件就是到这个目录去下载。

### 关于root权限的使用
#### termux-sudo
如果想要更好的配合root权限使用Termux，可以使用termux-sudo，为命令提供root权限，安装命令如下：
```
git clone https://gitlab.com/st42/termux-sudo.git
```
然后进入路径，执行以下命令将其复制到bin目录：
```
cat sudo > /data/data/com.termux/files/usr/bin/sudo
chmod 700 /data/data/com.termux/files/usr/bin/sudo
```
之后就可以通过
```
sudo
```
来执行需要root权限的命令。
#### proot
没有 root 的手机是没有 root 权限的。不过 termux 给我们提供了一个解决办法可以模拟 root 权限。

我们下载安装 proot
```
    pkg install proot
```
然后执行下面的命令即可获得 root 权限
```
    termux-chroot
```
root 时输入exit可以退回普通用户。
### 手机已经root
安装tsu,这是一个su的termux版本,用来在termux上替代su:
```
pkg install tsu
```
然后终端下面输入:
```
tsu
```
即可切换root用户,这个时候会弹出root授权提示,给予其root权限.在管理员身份下，输入exit可回到普通用户身份。

### 目录环境结构
```
~ > echo $HOME
/data/data/com.termux/files/home
 ~ > echo $PREFIX
/data/data/com.termux/files/usr
 ~ > echo $TMPPREFIX
/data/data/com.termux/files/usr/tmp/zsh
```

## Package manager/软件包管理
除了apt命令，Termux 还提供pkg命令进行软件包管理。
```
# 安装软件包
$ pkg install [package name]
 
# 卸载软件包
$ pkg uninstall [package name]
 
# 列出所有软件包
$ pkg list-all
```
其实，pkg的[底层](https://github.com/termux/termux-packages/issues/2151#issuecomment-486184252)就是apt，只是运行前会执行一次apt update，保证安装的是最新版本。所以，apt install sl基本等同于pkg install sl。Termux 支持的软件包清单，可以到[这里](https://github.com/termux/termux-packages/tree/master/packages)查看。
```
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
```
    pkg install curl
    pkg install git
    pkg install wget
```
然后通过下面的命令下载并执行优化脚本
```
    sh -c "$(curl -fsSL https://github.com/Cabbagec/termux-ohmyzsh/raw/master/install.sh)"
```
脚本会让我们选择背景色和字体，我的字体和颜色是 14,6，大家可以自己换一换试试。
```
    Enter a number, leave blank to not to change: 14
    Enter a number, leave blank to not to change: 6
```
脚本结束重启就会生效啦，如果想重新选择可以执行
```
    $ ~/termux-ohmyzsh/install.sh
```
### 创建QQ文件夹软连接
手机上一般经常使用手机QQ来接收文件,这里为了方便文件传输,直接在storage目录下创建软链接.这样可以直接在home目录下去访问QQ文件夹,非常方便文件的传输,大大提升了工作效率. 
+ QQ
```
ln -s /data/data/com.termux/files/home/storage/shared/tencent/QQfile_recv QQ
```
+ TIM
```
ln -s /data/data/com.termux/files/home/storage/shared/tencent/TIMfile_recv TIM
```

### 修改启动问候语
```
vim $PREFIX/etc/motd
```

## 常用软件包
```
apt install python 默认安装的是Python3
apt install python2
apt install clang 大名鼎鼎的c++ 编译器,用来编译c或c++程序
apt install g++
apt install vim termux自带vi,如果想使用vim(毕竟神之编辑器),则必须安装,且默认安装vim 8.0 版本, 配合.vimrc,bundle和git 可以完美配置python开发环境,体验几乎和ubuntu的终端无异.
apt install nano 文本编辑器，小巧
apt install git
apt install htop 任务管理器
apt install tree 目录树
apt install irssi irc客户端,命令行聊天软件
apt install sl 跑火车
apt install openssl ssh远程连接
```

## Node.js
### 安装 Node.js
```
$ apt install nodejs
```
安装完成后，就可以运行 JavaScript 脚本了。比如，新建一个脚本hello.js。
```
$ nano hello.js
// hello.js
console.log('hello world');
$ node hello.js
>>hello world
```

## python
### 安装python3及python2
```
$ apt install python
$ apt install python2
```
### pip模块管理器
优先级高
```
apt install pip 
# pkg instll python
python2 -m pip install --upgrade pip 
python -m pip install --upgrade pip
```
### ipython
ipython是一个python的交互式shell，支持变量自动补全，自动缩进，支持bash shell命令，内置了许多很有用的功能和函数。学习ipython将会让我们以一种更高的效率来使用python。先安装clang,否则直接使用pip安装ipython会失败报错.
```
pkg install clang
pip install ipython
pip3.6 install ipython
```
### 常用python模块
+ lxml——比标准库里xml模块性能更强大的xml处理模块
```
这个模块依赖的包很多，需要先安装：
apt install libcrypt libcrypt-dev
apt install libxml2 libxml2-dev libxslt libxslt-dev python-libxml2 python-libxslt
pip install lxml
```
+ scrapy——专业爬虫库，依赖于lxml
```
先安装依赖项：
apt install openssl openssl-tool openssl-dev libffi libffi-dev
再安装：
pip install scrapy
```
+ BeautifulSoup4——专业爬虫库
```
pip install BeautifulSoup4
pip install requests
```
+ numpy——数学计算库
```
pip install numpy
```
+ matplotlib——绘图模块
```
pip install matplotlib
```
+ pandas——数据分析模块
```
pip install pandas
```
+ Jupyter Notebook——超级好用的交互式记事本，下一篇会重点谈，和iPython公用内核，建议用这个
```
pip install jupyter
```
+ demjson——json处理库
```
pip install demjson
```
+ pillow——图像图像库
```
pip install pillow
```
+ librosa和python_speech_features ——语音识别库
```
pip install librosa
```
+ Paramiko——SSHv2远程 http://www.paramiko.org/
```
pip install paramiko
```
常用的模块也就是这些了，其他的模块可以在需要的时候再进行安装。


## 架设服务器
### Nodejs Server
现在，通过 Node.js 运行 HTTP Server。

首先，安装 npm 模块http-server。之后运行。
``` 
$ npm install -g http-server 
$ http-server
```
正常情况下，命令行会提示 Server 已经在 8080 端口运行了，并且还会提示外部可以访问的 IP 地址。举例来说，手机的局域网 IP 是 192.168.2.6，那么我们通过桌面电脑的浏览器访问http://192.168.2.6:8080，就可以看到 Termux 的根目录了。进入下面的storage子目录，就可以下载手机文件了。如果手机和电脑不在同一个局域网，那可以打开手机的热点功能，让桌面电脑通过手机热点上网，再访问手机的 HTTP Server。

从命令行查看手机的 IP 地址
```
$ apt install net-tools
$ ifconfig
```

### 使用python架设 HTTP Server
```
$ python -m http.server 8080
```

### 架设 [Apache 服务器](http://www.termuxtutorials.ga/2018/06/how-to-install-apache2-in-termux-termux.html)

### 远程访问手机/Remote Access
通过（FTP、SSH、Rsync）访问手机 https://wiki.termux.com/wiki/Remote_Access

### [Bypassing NAT](https://wiki.termux.com/wiki/Bypassing_NAT)

## 渗透测试
### Hydra
一个经典的密码爆破软件，安装命令很简单：
```
pkg install hydra
```
安装完成后，配合密码本或者密码生成的命令就可以使用了
### Metasploit Framework
一款十分经典的开源安全漏洞检测工具，可以用来发现漏洞、利用漏洞，有强大的漏洞库，可以生成想要的payload，配合nmap可以囊括从开始扫描直到提权的所有要求。
```
cd $HOME
pkg install wget
wget https://Auxilus.github.io/metasploit.sh
bash metasploit.sh
```
第一行用于切换到安装目录，可以根据需求自己选择，第二行安装wget，是个命令行下的下载工具，第三行下载用于自动安装Metasploit的批处理文件，第四行bash执行批处理脚本，接下来等待就行了。（按照官网的说法，只要没有红色的报警提示，就是安装成功了)

安装完成后，使用命令
```
./msfconsole
```
就可以运行Metasploit了。

重建数据库缓存
```
msf > db_rebuild_cache
```

### Nmap
一款非常经典的端口扫描工具，安装命令也非常简单：
```
pkg install nmap
```
使用也不介绍了，不过提醒一下，有些功能比如操作系统指纹识别需要root权限。

### sqlmap
一款特别经典的sql注入工具，这个需要python2才能运行，安装命令如下：
```
git clone https://github.com/sqlmapproject/sqlmap.git
```
通过cd进入sqlmap路径之后，使用如下命令进入sqlmap：
```
python2 sqlmap.py
```
这样还是比较麻烦的，我们可以直接定义一个名为sqlmap的命令，以后使用的时候直接输入sqlmap后接参数就行了。
通过vim编辑profile文件添加命令，这个文件在termux中不一样，路径如下：
```
/usr/etc/profile
```
使用vim编辑该文件
```
vim profile
```
如果没有安装vim，通过命令
```
apt install vim
```
来安装vim。

在文件最后添加以下内容：
```
alias sqlmap=“python2 /sql的绝对路径/sqlmap.py”
```
就可以在任意路径使用sqlmap直接代替那一串啦！

### RouterSploit
这是一个还算经典的路由器漏洞利用工具，需要python3，安装命令如下：
```
git clone https://github.com/reverse-shell/routersploit
```
使用和Sqlmap类似，进入routersploit路径后执行：
```
python rsf.py
```
注意，此处不是python2。也可以通过相同的方法定义命令，前面的Metasploit也是如此。

### sslscan 
SSL版本检测与密码套件 https://github.com/rbsec/sslscan/

sslscan是一个高效的Ç程序，它允许你检测SSL版本和加密套件（包括TLS），可以检查心脏滴血漏洞和贵宾犬漏洞。
```
apt install sslscan
```

### httrack
网站镜像工具,使用者可以通过HTTrack把互联网上的网站页面下载到本地计算机上。在默认设置下，HTTrack对网站页面的下载结果是按照原始站点相对链接的结构来组织的。

### whatportis
explore IANA's list of ports  https://github.com/ncrocfer/whatportis
```
pip install whatportis
```

### Slowloris
低带宽的DoS工具
```
git clone https://github.com/gkbrk/slowloris.git
cd slowloris
chmod +x slowloris.py
```

### RED_HAWK
一款采用PHP语言开发的多合一型渗透测试工具，它可以帮助我们完成信息采集、SQL漏洞扫描和资源爬取等任务。
```
pkg install php
git clone https://github.com/Tuhinshubhra/RED_HAWK.git
cd RED_HAWK
php rhawk.php
```
### Cupp
Cupp是一款用Python语言写成的可交互性的字典生成脚本。尤其适合社会工程学，当你收集到目标的具体信息后，你就可以通过这个工具来智能化生成关于目标的字典。
```
git clone https://github.com/Mebus/cupp.git
cd cupp
python2 cupp.py
```
### Hash-Buster
Hash Buster是一个用python编写的在线破解Hash的脚本，官方说5秒内破解,速度实际测试还不错哦~
```
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
```
git clone https://github.com/shawarkhanethicalhacker/D-TECT.git
cd D-TECT
python2 d-tect.py
```
### WPSeku
WPSeku 是一个用 Python 写的简单的 WordPress 漏洞扫描器，它可以被用来扫描本地以及远程安装的 WordPress 来找出安全问题。被评为2017年最受欢迎的十大开源黑客工具.
```
git clone https://github.com/m4ll0k/WPSeku.git
cd WPSeku
pip3 install -r requirements.txt
python3 wpseku.py
```
### XSStrike
XSStrike是一种先进的XSS检测工具。它具有强大的模糊测试引擎.
```
git clone https://github.com/UltimateHackers/XSStrike.git
cd XSStrike
pip2 install -r requirements.txt
python2 xsstrike
```


## lazymux（工具下载器）
Lazymux tools installer is very easy to use, only provided for lazy termux users. github：https://github.com/Gameye98/Lazymux

安装需要 py2 的环境，里面提供了多种工具的下载
```
    pkg install python2
    git clone https://github.com/Gameye98/Lazymux.git
```

##  kali
