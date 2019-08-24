# Termux-config

<img src="https://termux.com/files/htop_framed.png" width="300">

## About/关于
* https://termux.com
* https://github.com/termux/termux-app
* https://github.com/termux/termux-packages

## Install/安装
建议到官网下载或到应用市场下载安装，无需root https://termux.com/

## Environment/环境
### 更新
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
如果想要更好的配合root权限使用Termux，可以使用termux-sudo，为命令提供root权限，安装命令如下：
```
git clonehttps://gitlab.com/st42/termux-sudo.git
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
```
### 常用python模块
•lxml——比标准库里xml模块性能更强大的xml处理模块
```
这个模块依赖的包很多，需要先安装：
apt install libcrypt libcrypt-dev
apt install libxml2 libxml2-dev libxslt libxslt-dev python-libxml2 python-libxslt
pip install lxml
```
•scrapy——专业爬虫库，依赖于lxml
```
先安装依赖项：
apt install openssl openssl-tool openssl-dev libffi libffi-dev
再安装：
pip install scrapy
```
•BeautifulSoup4——专业爬虫库
```
pip install BeautifulSoup4
pip install requests
```
•numpy——数学计算库
```
pip install numpy
```
•matplotlib——绘图模块
```
pip install matplotlib
```
•pandas——数据分析模块
```
pip install pandas
```
•Jupyter Notebook——超级好用的交互式记事本，下一篇会重点谈，和iPython公用内核，建议用这个
```
pip install jupyter
```
•demjson——json处理库
```
pip install demjson
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

### 远程访问手机
通过（FTP、SSH、Rsync）访问手机 https://wiki.termux.com/wiki/Remote_Access

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
wgethttps://Auxilus.github.io/metasploit.sh
bash metasploit.sh
```
第一行用于切换到安装目录，可以根据需求自己选择，第二行安装wget，是个命令行下的下载工具，第三行下载用于自动安装Metasploit的批处理文件，第四行bash执行批处理脚本，接下来等待就行了。（按照官网的说法，只要没有红色的报警提示，就是安装成功了)

安装完成后，使用命令
```
./msfconsole
```
就可以运行Metasploit了。

### Nmap
一款非常经典的端口扫描工具，安装命令也非常简单：
```
pkg install nmap
```
使用也不介绍了，不过提醒一下，有些功能比如操作系统指纹识别需要root权限。

### sqlmap
一款特别经典的sql注入工具，这个需要python2才能运行，安装命令如下：
```
git clonehttps://github.com/sqlmapproject/sqlmap.git
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
git clonehttps://github.com/reverse-shell/routersploit
```
使用和Sqlmap类似，进入routersploit路径后执行：
```
python rsf.py
```
注意，此处不是python2。也可以通过相同的方法定义命令，前面的Metasploit也是如此。

