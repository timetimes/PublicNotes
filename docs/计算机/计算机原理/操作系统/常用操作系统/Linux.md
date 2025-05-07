# Linux

发行版，常用ubuntu

Linux系统的文件结构：

```bash
/bin        二进制文件，系统常规命令
/boot       系统启动分区，系统启动时读取的文件
/dev        设备文件
/etc        大多数配置文件
/home       普通用户的家目录
/lib        32位函数库
/lib64      64位库
/media      手动临时挂载点
/mnt        手动临时挂载点
/opt        第三方软件安装位置
/proc       进程信息及硬件信息
/root       临时设备的默认挂载点
/sbin       系统管理命令
/srv        数据
/var        数据
/sys        内核相关信息
/tmp        临时文件
/usr        用户相关设定
```

用户名：lain 密码：lain

/etc/passwd 文件，是系统用户配置文件，存储了系统中所有用户的基本信息，并且所有用户都可以对此文件执行读操作。
`用户名：密码：UID（用户ID）：GID（组ID）：描述性信息：主目录：默认Shell`
其中密码"x" 表示此用户设有密码，真正的密码保存在 /etc/shadow 文件中

/etc/shadow 文件用于存储 Linux 系统中用户的密码信息，又称为“影子文件”。/etc/shadow 文件只有 root 用户拥有读权限，其他用户没有任何权限。
`用户名：加密密码：最后一次修改时间：最小修改时间间隔：密码有效期：密码需要变更前的警告天数：密码过期后的宽限时间：账号失效时间：保留字段`
加密密码。这里保存的是真正加密的密码。如果密码是 "!!" 或 "`*`"，代表没有密码或是不能登录的伪用户
shadow文件加密的密码具有固定格式

```scss
$id$salt$encrypted
```

- id：表示加密算法，1 代表 MD5，5 代表 SHA-256，6 代表 SHA-512。
- salt：表示密码学中的 Salt，由系统随机生成 。
- encrypted：表示密码的 hash。

使用john暴力破解：

```shell
sudo apt install john    // 安装John the Ripper
john                     // 检查是否安装
sudo john ./shadow      // 暴力破解获取的shadow文件中的账号密码
sudo john ./shadow --show // 再次显示已经爆破的密码
```

## Shell

- **命令行界面 (CLI)** = 使用文本命令进行交互的用户界面
	命令行界面(Command-line Interface)是在图形用户界面(GUI)得到普及之前使用最为广泛的用户界面，它通常不支持鼠标，用户通过键盘输入指令，计算机接收到指令后，予以执行。
- **终端 (Terminal)** = TTY = 文本输入/输出环境
	终端 (Terminal)是一种用来让用户输入数据至计算机，以及显示其计算结果的机器。也就是说，终端只是一种用于与计算机进行交互的输入输出设备，其本身并不提供运算处理功能。
	最早的 Unix 终端是 ASR-33 电传打字机，而电传打字机 (Teletype / Teletypewriter) 的英文缩写就是 tty，因此tty 成了终端的统称
- **控制台 (Console)** = 一种特殊的终端
	在历史上，终端是连接到计算机上的一种带输入输出功能的外设。但是有一个终端与众不同，它与计算机主机是一体的，是计算机的一个组成部分。这个特殊的终端就叫做 控制台(Console)。顾名思义，控制台是用于管理主机的，只能给系统管理员使用，有着比普通终端更大的权限。随着个人计算机的普及，控制台 与终端 的概念已经逐渐模糊。
	随着计算机的进化，已经见不到专门的终端硬件了，取而代之的则是键盘与显示器。于是使用终端模拟器 (Terminal Emulator)模拟传统终端的行为。
- **Shell** = 命令行解释器，执行用户输入的命令并返回结果
	操作系统的 **内核** (Kernel) 管理着整台计算机的硬件，是现代操作系统中最基本的部分。但是，内核处于系统的底层，不能让普通用户随意操作。
	于是需要一个专门的程序，它接受用户输入的命令，然后帮我们与内核沟通，最后让内核完成我们的任务。这个提供用户界面的程序被叫做 **Shell** (壳层)。
	终端只负责提供一个输出和输入的环境，而shell负责把你的操作或者命令解释成机器码传递给系统内核执行最后再返回结果给终端，然后终端再显示给你看
	Shell 通常可以分为两种：**命令行 Shell** 与 **图形 Shell**。顾名思义，前者提供一个命令行界面 (CLI)，后者提供一个图形用户界面 (GUI)。
	常见或历史上知名的命令行 Shell 有：
	- 适用于 Unix 及类 Unix 系统：sh、**bash**（目前绝大多数 Linux 发行版的默认 shell）、zsh、fish
	- Windows 下的 cmd.exe (命令提示符) 与 PowerShell

```bash
示例：root@app00:~# 
root    //用户名，root为超级用户
@       //分隔符
app00   //主机名称
~       //当前所在目录，默认用户目录为~，会随着目录切换而变化，例如：（root@app00:/bin# ，当前位置在bin目录下）
#       //表示当前用户是超级用户，普通用户为$，例如：（"lain@app00:/root$" ，表示使用用户"lain"访问/root文件夹）
```
Ctrl + C退出命令行
Ctrl + Z+Enter退出Python命令行(或输入 `exit()`)

```bash
sudo adduser 用户名    # 新建用户
sudo passwd 用户名     # 设置用户密码 root用户初始没密码可以设置
sudo userdel -r 用户名 # 删除用户
```

**基础操作**

```bash
关闭系统（远程服务器慎用）
(1)立刻关机
  shutdown -h now 或者 poweroff
(2)两分钟后关机
  shutdown -h 2
关闭重启
(1)立刻重启
  shutdown -r now 或者 reboot
(2)两分钟后重启
  shutdown -r 2 
帮助命令（help）
  ifconfig  --help     //查看 ifconfig 命令的用法
命令说明书（man）
  man shutdown         //打开命令说明后，可按"q"键退出
切换用户（su）
  su lain              //切换为用户"lain",输入后回车需要输入该用户的密码
  su root              //切换为超级用户root,输入后回车需要输入该用户的密码
  exit                 //退出当前用户
```

**目录操作**

```bash
切换目录（cd）
  cd /                 //切换到根目录
  cd /bin              //切换到根目录下的bin目录
  cd ../               //切换到上一级目录 或者使用命令：cd ..
  cd ~                 //切换到home目录
  cd -                 //切换到上次访问的目录
  cd xx(文件夹名)       //切换到本目录下的名为xx的文件目录，如果目录不存在报错
  cd /xxx/xx/x         //可以输入完整的路径，直接切换到目标目录，输入过程中可以使用tab键快速补全
查看目录（ls）
  ls                   //查看当前目录下的所有目录和文件
  ls -a                //查看当前目录下的所有目录和文件（包括隐藏的文件）
  ls -l                //列表查看当前目录下的所有目录和文件（列表查看，显示更多信息），与命令"ll"效果一样
  ls /bin              //查看指定目录下的所有目录和文件 
创建目录（mkdir）
  mkdir tools          //在当前目录下创建一个名为tools的目录
  mkdir /bin/tools     //在指定目录下创建一个名为tools的目录
删除目录与文件（rm）
  rm 文件名              //删除当前目录下的文件
  rm -f 文件名           //删除当前目录的的文件（不询问）
  rm -r 文件夹名         //递归删除当前目录下此名的目录
  rm -rf 文件夹名        //递归删除当前目录下此名的目录（不询问）
  rm -rf *              //将当前目录下的所有目录和文件全部删除
  rm -rf /*             //将根目录下的所有文件全部删除【慎用！相当于格式化系统】
修改目录（mv）
  mv 当前目录名 新目录名        //修改目录名，同样适用与文件操作
  mv /usr/tmp/tool /opt       //将/usr/tmp目录下的tool目录剪切到 /opt目录下面
  mv -r /usr/tmp/tool /opt    //递归剪切目录中所有文件和文件夹
拷贝目录（cp）
  cp /usr/tmp/tool /opt       //将/usr/tmp目录下的tool目录复制到 /opt目录下面
  cp -r /usr/tmp/tool /opt    //递归剪复制目录中所有文件和文件夹
搜索目录（find）
  find /bin -name 'a*'        //查找/bin目录下的所有以a开头的文件或者目录
查看当前目录（pwd）
  pwd                         //显示当前位置路径
```

**文件操作**
新增文件（touch）
   touch  a.txt         //在当前目录下创建名为a的txt文件（文件不存在），如果文件存在，将文件时间属性修改为当前系统时间
删除文件（rm）
  rm 文件名              //删除当前目录下的文件
  rm -f 文件名           //删除当前目录的的文件（不询问）
编辑文件（vi、vim）[[../../../语言/其他语法/vim|vim]]
```vim
  vi 文件名              //打开需要编辑的文件
  --进入后，操作界面有三种模式：命令模式（command mode）、插入模式（Insert mode）和底行模式（last line mode）
  命令模式
  -刚进入文件就是命令模式，通过方向键控制光标位置，
  -使用命令"dd"删除当前整行
  -使用命令"/字段"之后回车进行查找。n查找下一个，N上一个。支持正则表达式。
  -按"i"在光标所在字符前开始插入
  -按"a"在光标所在字符后开始插入
  -按"o"在光标所在行的下面另起一新行插入
  -按"："进入底行模式
  插入模式
  -此时可以对文件内容进行编辑，左下角会显示 "-- 插入 --""
  -按"ESC"进入底行模式
  底行模式
  -退出编辑：      :q
  -强制退出：      :q!
  -保存并退出：    :wq
  ## 操作步骤示例 ##
  1.保存文件：按"ESC" -> 输入":" -> 输入"wq",回车     //保存并退出编辑
  2.取消操作：按"ESC" -> 输入":" -> 输入"q!",回车     //撤销本次修改并退出编辑
  ## 补充 ##
  vim +10 filename.txt                   //打开文件并跳到第10行
  vim -R /etc/passwd                     //以只读模式打开文件
```
查看文件
  cat a.txt          //查看文件最后一屏内容
  less a.txt         //PgUp向上翻页，PgDn向下翻页，"q"退出查看
  more a.txt         //显示百分比，回车查看下一行，空格查看下一页，"q"退出查看
  tail -100 a.txt    //查看文件的后100行，"Ctrl+C"退出查看
  
**文件权限**
权限说明
  文件权限简介：'r' 代表可读（4），'w' 代表可写（2），'x' 代表执行权限（1），括号内代表"8421法"
  ##文件权限信息示例：-rwxrw-r--
  -第一位：'-'就代表是文件，'d'代表是文件夹
  -第一组三位：拥有者的权限
  -第二组三位：拥有者所在的组，组员的权限
  -第三组三位：代表的是其他用户的权限
  
```bash
普通授权    chmod +x a.txt    
8421法     chmod 777 a.txt     //1+2+4=7，"7"说明授予所有权限
```

**打包与解压**
说明
  .zip、.rar        //windows系统中压缩文件的扩展名
  .tar              //Linux中打包文件的扩展名
  .gz               //Linux中压缩文件的扩展名
  .tar.gz           //Linux中打包并压缩文件的扩展名
  
```bash
打包文件
  tar -zcvf 打包压缩后的文件名 要打包的文件
  参数说明：z：调用gzip压缩命令进行压缩; c：打包文件; v：显示运行过程; f：指定文件名;
  示例：
  tar -zcvf a.tar file1 file2,...      //多个文件压缩打包
解压文件
  tar -zxvf a.tar                      //解包至当前目录
  tar -zxvf a.tar -C /usr------        //指定解压的位置
  unzip test.zip             //解压*.zip文件 
  unzip -l test.zip          //查看*.zip文件的内容
```

**其他常用命令**
```bash
find
  find . -name "* .c"     //将目前目录及其子目录下所有延伸档名是 c 的文件列出来
  find . -type f         //将目前目录其其下子目录中所有一般文件列出
  find . -ctime -20      //将目前目录及其子目录下所有最近 20 天内更新过的文件列出
  find /var/log -type f -mtime +7 -ok rm {} \;     //查找/var/log目录中更改时间在7日以前的普通文件，并在删除之前询问它们
  find . -type f -perm 644 -exec ls -l {} \;       //查找前目录中文件属主具有读、写权限，并且文件所属组的用户和其他用户具有读权限的文件
  find / -type f -size 0 -exec ls -l {} \;         //为了查找系统中所有文件长度为0的普通文件，并列出它们的完整路径
whereis
  whereis ls             //将和ls文件相关的文件都查找出来
which
  说明：which指令会在环境变量$PATH设置的目录里查找符合条件的文件。
  which bash             //查看指令"bash"的绝对路径
sudo
  说明：sudo命令以系统管理者的身份执行指令，也就是说，经由 sudo 所执行的指令就好像是 root 亲自执行。需要输入自己账户密码。
  使用权限：在 /etc/sudoers 中有出现的使用者
  sudo -l                              //列出目前的权限
  $ sudo -u lain vi ~www/index.html    //以 lain用户身份编辑  home 目录下www目录中的 index.html 文件
grep
  grep -i "the" demo_file              //在文件中查找字符串(不区分大小写)
  grep -A 3 -i "example" demo_text     //输出成功匹配的行，以及该行之后的三行
  grep -r "ramesh" *                   //在一个文件夹中递归查询包含指定字符串的文件
service
  说明：service命令用于运行System V init脚本，这些脚本一般位于/etc/init.d文件下，这个命令可以直接运行这个文件夹里面的脚本，而不用加上路径
  service ssh status      //查看服务状态 
  service --status-all    //查看所有服务状态 
  service ssh restart     //重启服务 
free
  说明：这个命令用于显示系统当前内存的使用情况，包括已用内存、可用内存和交换内存的情况 
  free -g            //以G为单位输出内存的使用量，-g为GB，-m为MB，-k为KB，-b为字节 
  free -t            //查看所有内存的汇总
top
  top               //显示当前系统中占用资源最多的一些进程, shift+m 按照内存大小查看
df
  说明：显示文件系统的磁盘使用情况
  df -h            //一种易看的显示
mount
  mount /dev/sdb1 /u01              //挂载一个文件系统，需要先创建一个目录，然后将这个文件系统挂载到这个目录上
  dev/sdb1 /u01 ext2 defaults 0 2   //添加到fstab中进行自动挂载，这样任何时候系统重启的时候，文件系统都会被加载 
uname
  说明：uname可以显示一些重要的系统信息，例如内核名称、主机名、内核版本号、处理器类型之类的信息 
  uname -a
yum
  说明：安装插件命令
  yum install httpd      //使用yum安装apache 
  yum update httpd       //更新apache 
  yum remove httpd       //卸载/删除apache 
rpm
  说明：插件安装命令
  rpm -ivh httpd-2.2.3-22.0.1.el5.i386.rpm      //使用rpm文件安装apache 
  rpm -uvh httpd-2.2.3-22.0.1.el5.i386.rpm      //使用rpm更新apache 
  rpm -ev httpd                                 //卸载/删除apache 
date
  date -s "01/31/2010 23:59:53"   ///设置系统时间
wget
  说明：使用wget从网上下载软件、音乐、视频 
  示例：wget http://prdownloads.sourceforge.net/sourceforge/nagios/nagios-3.2.1.tar.gz
  //下载文件并以指定的文件名保存文件
  wget -O nagios.tar.gz http://prdownloads.sourceforge.net/sourceforge/nagios/nagios-3.2.1.tar.gz
ftp
   ftp IP/hostname    //访问ftp服务器
   mls * .html -       //显示远程主机上文件列表
scp
	scp /opt/data.txt  192.168.1.101:/opt/    //将本地opt目录下的data文件发送到192.168.1.101服务器的opt目录下
```

**系统管理**

```bash
防火墙操作
  service iptables status      //查看iptables服务的状态
  service iptables start       //开启iptables服务
  service iptables stop        //停止iptables服务
  service iptables restart     //重启iptables服务
  chkconfig iptables off       //关闭iptables服务的开机自启动
  chkconfig iptables on        //开启iptables服务的开机自启动
  ##centos7 防火墙操作
  systemctl status firewalld.service     //查看防火墙状态
  systemctl stop firewalld.service       //关闭运行的防火墙
  systemctl disable firewalld.service    //永久禁止防火墙服务
修改主机名（CentOS 7）
  hostnamectl set-hostname 主机名
查看网络
  ifconfig
修改IP
  修改网络配置文件，文件地址：/etc/sysconfig/network-scripts/ifcfg-eth0
  ------------------------------------------------
  主要修改以下配置：  
  TYPE=Ethernet               //网络类型
  BOOTPROTO=static            //静态IP
  DEVICE=ens00                //网卡名
  IPADDR=192.168.1.100        //设置的IP
  NETMASK=255.255.255.0       //子网掩码
  GATEWAY=192.168.1.1         //网关
  DNS1=192.168.1.1            //DNS
  DNS2=8.8.8.8                //备用DNS
  ONBOOT=yes                  //系统启动时启动此设置
  -------------------------------------------------
  修改保存以后使用命令重启网卡：service network restart
配置映射
  修改文件： vi /etc/hosts
  在文件最后添加映射地址，示例如下：
   192.168.1.101  node1
   192.168.1.102  node2
   192.168.1.103  node3
  配置好以后保存退出，输入命令：ping node1 ，可见实际 ping 的是 192.168.1.101。
查看进程
  ps -ef         //查看所有正在运行的进程
结束进程
  kill pid       //杀死该pid的进程
  kill -9 pid    //强制杀死该进程   
查看链接
  ping IP        //查看与此IP地址的连接情况
  netstat -an    //查看当前系统端口
  netstat -an | grep 8080     //查看指定端口
快速清屏
  ctrl+l        //清屏，往上翻可以查看历史操作
远程主机
  ssh IP       //远程主机，需要输入用户名和密码
```  

**安装软件**的几种方法：包管理器、编译安装源码包
1）sudo apt-get install 软件名
2）wget URL地址
tar -xvf 文件名
make
make clean linux-x86-64
3）./configure
make
make install

## 远程连接

### SSH

Secure Shell(SSH) 是由 IETF(The Internet Engineering Task Force) 制定的建立在应用层基础上的安全网络协议。它是专为远程登录会话(甚至可以用Windows远程登录Linux服务器进行文件互传)和其他网络服务提供安全性的协议，可有效弥补网络中的漏洞。通过SSH，可以把所有传输的数据进行加密，也能够防止DNS欺骗和IP欺骗。还有一个额外的好处就是传输的数据是经过压缩的，所以可以加快传输的速度。目前已经成为Linux系统的标准配置。

SSH只是一种协议，存在多种实现，既有商业实现，也有开源实现。本文主要介绍OpenSSH免费开源实现在Ubuntu中的应用，如果要在Windows中使用SSH，需要使用另一个软件PuTTY。

SSH分为客户端 openssh-client 和服务器 openssh-server，可以利用以下命令确认电脑上是否安装了客户端和服务器

`dpkg -l | grep ssh`

```bash
sudo apt-get install openssh-client 
sudo apt-get install openssh-server

sudo /etc/init.d/ssh stop  #server停止ssh服务 
sudo /etc/init.d/ssh restart  #server重启ssh服务
```

**口令登录**
`ssh 客户端用户名@服务器ip地址`如果需要调用图形界面程序可以使用 -X 选项
SSH服务的默认端口是22，也就是说，如果你不设置端口的话登录请求会自动送到远程主机的22端口。我们可以使用 -p 选项来修改端口号
**公钥登录**
使用ssh-keygen命令生成密钥对：

```bash
ssh-keygen -t rsa   #-t表示类型选项，这里采用rsa加密算法
```

执行结束以后会在 /home/当前用户 目录下生成一个 .ssh 文件夹,其中包含私钥文件 id_rsa 和公钥文件 id_rsa.pub
使用ssh-copy-id命令将公钥复制到远程主机。ssh-copy-id会将公钥写到远程主机的 ~/ .ssh/authorized_key 文件中
`ssh-copy-id ldz@192.168.0.1`
经过以上两个步骤，以后再登录这个远程主机就不用再输入密码了

当我们利用ssh在远程主机上跑程序的时候，只要关闭了终端就会中断ssh连接，然后远程主机上正在跑的程序或者服务就会自动停止运行。我们可以利用 nohup + 需要运行的程序 使运行的程序在切断ssh连接的时候仍然能够继续在远程主机中运行。nohup即no hang up(不挂起)。

将文件从远程机器复制到本地机器`rsync username@ip_address:/home/username/filename .`
将文件从本地机器复制到远程机器`rsync filename username@ip_address:/home/username`
使用-r可以在远程系统之间通过 SSH 复制整个目录

### FTP

## 包

修改软件源为国内镜像源
`sudo sed -i 's/\/\/.*\/ubuntu/\/\/mirrors.aliyun.com\/ubuntu/g' /etc/apt/sources.list`

PPA源可以理解成第三方源。有些软件在ubuntu官方软件源是没有的，但在PPA源里就可能有。

## 发行版

Ubuntu
[[../../../计算机安全/Kail|Kail]]是一个优秀的渗透工具集成系统

## 桌面

Linux 服务器需要占用系统资源来运行服务。图形化桌面环境会消耗大量的系统资源，因此服务器操作系统默认不包含桌面环境。

更新和升级以确保我们系统的包是最新的

```bash
sudo apt update && sudo apt upgrade -y
```

安装桌面环境：

```bash
sudo apt install xfce4 xfce4-goodies # FCE桌面（轻量级）
sudo apt install ubuntu-desktop # ubuntu默认的GNOME桌面
```

指定默认桌面会话echo xfce4-session > ~/.xsession

GNOME 桌面默认使用 GDM3 作为显示管理器，但从资源角度考虑它有点重。你可以使用更轻量级和资源友好的管理器。这里我们使用一个平台无关的显示管理器 lightdm：

```bash
sudo apt install lightdm
```

安装 lightdm 时系统会让我们选择默认的显示管理器，因为即使你可以安装多个管理器，也只能运行一个。

```bash
sudo service lightdm start
```

你可以使用下面的命令来检查当前的显示管理器：

```bash
cat /etc/X11/default-display-manager
```

如果你想关闭 GUI，那么打开一个终端并输入：

```bash
sudo service lightdm stop
```

删除 GUI

```bash
sudo apt remove ubuntu-desktop
sudo apt remove lightdm
sudo apt autoremove
sudo service lightdm stop
```

远程连接 sudo service dbus start

```bash
sudo apt-get install xrdp
```

编辑xrdp.ini 可以改变端口
sudo vim /etc/xrdp/xrdp.ini

验证 xrdp 的状态
如果系统使用 systemd：sudo systemctl status xrdp，sudo systemctl start xrdp，开机自启sudo systemctl enable xrdp
如果系统使用 SysV init：sudo service xrdp status，sudo service xrdp start

如果你有一台 Windows 电脑，你可以使用默认的 RDP 客户端。
在 Windows 搜索栏搜索并打开“远程桌面连接”，输入远程服务器 IP地址和端口
