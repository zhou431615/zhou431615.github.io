---
layout:     post
title:      "Linux（一）"
subtitle:   "Linux学习笔记"
date:       2021-11-12 08:00:00
author:     "QianYe"

tags:
- Linux
---

## Linux学习（无脑上手）

### 一、什么是Linux？

Linux，全称GNU/Linux，是一种免费使用和自由传播的[类UNIX](https://baike.baidu.com/item/类UNIX/9032872)操作系统，其内核由[林纳斯·本纳第克特·托瓦兹](https://baike.baidu.com/item/林纳斯·本纳第克特·托瓦兹/1034429)于1991年10月5日首次发布，它主要受到[Minix](https://baike.baidu.com/item/Minix/7106045)和Unix思想的启发，是一个基于[POSIX](https://baike.baidu.com/item/POSIX)的多用户、[多任务](https://baike.baidu.com/item/多任务/1011764)、支持[多线程](https://baike.baidu.com/item/多线程/1190404)和多[CPU](https://baike.baidu.com/item/CPU)的操作系统。它能运行主要的[Unix](https://baike.baidu.com/item/Unix/219943)工具软件、应用程序和网络协议。它支持[32位](https://baike.baidu.com/item/32位/5812218)和[64位](https://baike.baidu.com/item/64位)硬件。Linux继承了Unix以网络为核心的设计思想，是一个性能稳定的多用户网络操作系统。Linux有上百种不同的发行版，如基于社区开发的[debian](https://baike.baidu.com/item/debian/748667)、[archlinux](https://baike.baidu.com/item/archlinux/10857530)，和基于商业开发的[Red Hat Enterprise Linux](https://baike.baidu.com/item/Red Hat Enterprise Linux/10770503)、[SUSE](https://baike.baidu.com/item/SUSE/60409)、[Oracle Linux](https://baike.baidu.com/item/Oracle Linux/6876458)等。

#### 优点

1.Linux由众多微内核组成，其源代码完全开源；

2.Linux继承了[Unix](https://baike.baidu.com/item/Unix/219943)的特性，具有非常强大的网络功能，其支持所有的因特网协议，包括TCP/[IPv4](https://baike.baidu.com/item/IPv4/422599)、[TCP](https://baike.baidu.com/item/TCP/33012)/IPv6和链路层拓扑程序等，且可以利用Unix的网络特性开发出新的协议栈；

3.Linux系统工具链完整，简单操作就可以配置出合适的开发环境，可以简化开发过程，减少开发中仿真工具的障碍，使[系统](https://baike.baidu.com/item/系统/479832)具有较强的移植性；

### 二、Linux服务器

[Linux服务器](https://baike.baidu.com/item/Linux服务器/7296589)是设计出来进行业务处理应用的，在网络和计算机系统当中有广泛的应用，可以提供数据库管理和网络服务等内容，是一种性能非常高的和开源的[服务器](https://baike.baidu.com/item/服务器/100571)，在我国的[计算机系统](https://baike.baidu.com/item/计算机系统/7210959)的[客户端](https://baike.baidu.com/item/客户端/101081)当中，有很多采用的就是Linux系统，其使用的范围非常广泛，用户体验反应较好。但是对于一些希望计算机应用性能比较高的单位而言，[windows](https://baike.baidu.com/item/windows/165458)系统需要经常进行资源整合和碎片化管理，系统在配置的时候经常需要重新启动，这就无法避免产生停机的问题。同时，由于Linux系统的处理能力非常强悍，具备不可比拟的稳定性特征，因而Linux系统就不用经常进行重启，Linux系统的变化可以在配置的过程中实现，所以Linux服务器出现故障的概率比较小，所以很多企业组织在计算机配置的过程中经常使用Linux系统，从而降低[服务器](https://baike.baidu.com/item/服务器/100571)发生崩溃的可能性，很多企业在配置Linux系统的时候，都是通过减少服务器的故障发生率，实现企业业务的高效运转。

------

**以上都是Linux背景,实用地教程正式开始！**

在知道什么是Linux后，如何拥有一台Linux服务器呢？

- 买一台自带Linux操作系统的计算机
- 买一台云服务装载Linux（阿里云&腾讯云）
- 通过虚拟机安装Linux操作系统在本机(Win或者Mac)

### 三、安装虚拟机

在安装Linux之前，需要安装虚拟机。下面一起安装吧！（按照提示，一直下一步，无脑安装就可成功）

准备如下：

  VMware Workstation

下载地址：https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html

安装完虚拟机后，就可安装Linux，例如Centos7。（无脑安装）

**唯一需要设置配置：分配给虚拟机上的Linux的内存如2G cpu为2核 比较合适。**

![image-20211123211116497](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111241024922.png)

![image-20211123220012787](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111241025084.png)

初学者，使用root账号。

### 四、云服务器（阿里云&腾讯云）

> 补充了解
>
> 为什么程序员都需要一个自己的服务器呢？
>
> 1.你作为一个程序员，必须要发布自己的网站和项目
>
> 2.练习Linux命令操作
>
> 3.将自己的远程的仓库、远程数据库、远程Tomcat等等搭建在服务器上
>
> 4.练习Linux进行任意的环境部署（Window下开发，必须熟悉Linux）

对于学生用户而言，阿里云和腾讯云的学生认证非常方便，也有很多产品开放免费试用，（可以先试用着玩玩）一般做活动的时候买比较便宜。

> 吐槽一下，华为云的注册、登录、认证过程太折腾人了。
>
> AWS 有兴趣也可以玩玩

![image-20211123213542377](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111241025481.png)

另外还有一条：购买最好包年包月购买，不要选择按量购买（划不来）。

![image-20211123214905217](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111241025443.png)

在重置密码后，登录即可使用。

![image-20211123215359576](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111241025259.png)

### 五、基本命令（重点掌握）

> 新手学习Linux最重要的就是熟悉Linux命令  多敲多练

#### （一）、开关机

1.1 关机和重启
关机
    shutdown -h now        立刻关机
    shutdown -h 5        5分钟后关机
    poweroff            立刻关机
重启
    shutdown -r now        立刻重启
    shutdown -r 5        5分钟后重启
    reboot                立刻重启

1.2 帮助命令
--help命令
  shutdown --help：
  ifconfig  --help：查看网卡信息

man命令（命令说明书） 
  man shutdown
  注意：man shutdown打开命令说明书之后，使用按键q退出

#### （二）、目录操作命令

2.1 目录切换 cd
命令：cd 目录

cd /        切换到根目录
cd /usr        切换到根目录下的usr目录
cd ../        切换到上一级目录 或者  cd ..
cd ~        切换到home目录
cd -        切换到上次访问的目录

2.2 目录查看 ls [-al]
命令：ls [-al]

ls                查看当前目录下的所有目录和文件
ls -a            查看当前目录下的所有目录和文件（包括隐藏的文件）
ls -l 或 ll       列表查看当前目录下的所有目录和文件（列表查看，显示更多信息）
ls /dir            查看指定目录下的所有目录和文件   如：ls /usr

2.3 目录操作【增，删，改，查】
2.3.1 创建目录【增】 mkdir
命令：mkdir 目录

mkdir    aaa            在当前目录下创建一个名为aaa的目录
mkdir    /usr/aaa    在指定目录下创建一个名为aaa的目录

2.3.2 删除目录或文件【删】rm
命令：rm [-rf] 目录

删除文件：
rm 文件        删除当前目录下的文件
rm -f 文件    删除当前目录的的文件（不询问）

删除目录：
rm -r aaa    递归删除当前目录下的aaa目录
rm -rf aaa    递归删除当前目录下的aaa目录（不询问）

全部删除：
rm -rf *    将当前目录下的所有目录和文件全部删除
rm -rf /*    【自杀命令！慎用！慎用！慎用！】将根目录下的所有文件全部删除

注意：rm不仅可以删除目录，也可以删除其他文件或压缩包，为了方便大家的记忆，无论删除任何目录或文件，都直接使用 rm -rf 目录/文件/压缩包

2.3.3 目录修改【改】mv 和 cp
一、重命名目录
    命令：mv 当前目录  新目录
    例如：mv aaa bbb    将目录aaa改为bbb
    注意：mv的语法不仅可以对目录进行重命名而且也可以对各种文件，压缩包等进行    重命名的操作

二、剪切目录
    命令：mv 目录名称 目录的新位置
    示例：将/usr/tmp目录下的aaa目录剪切到 /usr目录下面     mv /usr/tmp/aaa /usr
    注意：mv语法不仅可以对目录进行剪切操作，对文件和压缩包等都可执行剪切操作

三、拷贝目录
    命令：cp -r 目录名称 目录拷贝的目标位置   -r代表递归
    示例：将/usr/tmp目录下的aaa目录复制到 /usr目录下面     cp /usr/tmp/aaa  /usr
    注意：cp命令不仅可以拷贝目录还可以拷贝文件，压缩包等，拷贝文件和压缩包时不    用写-r递归

2.3.4 搜索目录【查】find
命令：find 目录 参数 文件名称
示例：find /usr/tmp -name 'a*'    查找/usr/tmp目录下的所有以a开头的目录或文件

#### （三）、文件操作命令

3.1 文件操作【增，删，改，查】
3.1.1 新建文件【增】touch
命令：touch 文件名
示例：在当前目录创建一个名为aa.txt的文件        touch  aa.txt

3.1.2 删除文件 【删】 rm
命令：rm -rf 文件名

3.1.3 修改文件【改】 vi或vim
【vi编辑器的3种模式】
    基本上vi可以分为三种状态，分别是命令模式（command mode）、插入模式（Insert mode）和底行模式（last line mode），各模式的功能区分如下：
1) 命令行模式command mode）
      控制屏幕光标的移动，字符、字或行的删除，查找，移动复制某区段及进入Insert mode下，或者到 last line mode。
      命令行模式下的常用命令：
      【1】控制光标移动：↑，↓，j
      【2】删除当前行：dd 
      【3】查找：/字符
      【4】进入编辑模式：i o a
      【5】进入底行模式：:
      
2) 编辑模式（Insert mode）
      只有在Insert mode下，才可以做文字输入，按「ESC」键可回到命令行模式。
      编辑模式下常用命令：
      【1】ESC 退出编辑模式到命令行模式；
      
3) 底行模式（last line mode）
     将文件保存或退出vi，也可以设置编辑环境，如寻找字符串、列出行号……等。
     底行模式下常用命令：
     【1】退出编辑：   :q
     【2】强制退出：   :q!
     【3】保存并退出：  :wq

打开文件

命令：vi 文件名
示例：打开当前目录下的aa.txt文件     vi aa.txt 或者 vim aa.txt

注意：使用vi编辑器打开文件后，并不能编辑，因为此时处于命令模式，点击键盘i/a/o进入编辑模式。

编辑文件

使用vi编辑器打开文件后点击按键：i ，a或者o即可进入编辑模式。

i:在光标所在字符前开始插入
a:在光标所在字符后开始插入
o:在光标所在行的下面另起一新行插入

保存或者取消编辑

保存文件：

第一步：ESC  进入命令行模式
第二步：:     进入底行模式
第三步：wq     保存并退出编辑

取消编辑：

第一步：ESC  进入命令行模式
第二步：:     进入底行模式
第三步：q!     撤销本次修改并退出编辑

3.1.4 文件的查看【查】
文件的查看命令：cat/more/less/tail

cat：看最后一屏

示例：使用cat查看/etc/sudo.conf文件，只能显示最后一屏内容
cat sudo.conf

more：百分比显示

示例：使用more查看/etc/sudo.conf文件，可以显示百分比，回车可以向下一行，空格可以向下一页，q可以退出查看
more sudo.conf

less：翻页查看

示例：使用less查看/etc/sudo.conf文件，可以使用键盘上的PgUp和PgDn向上    和向下翻页，q结束查看
less sudo.conf

tail：指定行数或者动态查看

示例：使用tail -10 查看/etc/sudo.conf文件的后10行，Ctrl+C结束  
tail -10 sudo.conf

3.2 权限修改
rwx：r代表可读，w代表可写，x代表该文件是一个可执行文件，如果rwx任意位置变为-则代表不可读或不可写或不可执行文件。

示例：给aaa.txt文件权限改为可执行文件权限，aaa.txt文件的权限是-rw-------

第一位：-就代表是文件，d代表是文件夹
第一段（3位）：代表拥有者的权限
第二段（3位）：代表拥有者所在的组，组员的权限
第三段（最后3位）：代表的是其他用户的权限

   421  421  421
-  rw-   ---     ---

命令：chmod +x aaa.txt
或者采用8421法
命令：chmod 100 aaa.txt

#### （四）、压缩文件操作

4.1 打包和压缩
Windows的压缩文件的扩展名  .zip/.rar
linux中的打包文件：aa.tar      
linux中的压缩文件：bb.gz    
linux中打包并压缩的文件：.tar.gz

Linux中的打包文件一般是以.tar结尾的，压缩的命令一般是以.gz结尾的。
而一般情况下打包和压缩是一起进行的，打包并压缩后的文件的后缀名一般.tar.gz。

命令：tar -zcvf 打包压缩后的文件名 要打包的文件
其中：z：调用gzip压缩命令进行压缩
  c：打包文件
  v：显示运行过程
  f：指定文件名

示例：打包并压缩/usr/tmp 下的所有文件 压缩后的压缩包指定名称为xxx.tar
tar -zcvf ab.tar aa.txt bb.txt 
或：tar -zcvf ab.tar  *

4.2 解压
命令：tar [-zxvf] 压缩文件    
其中：x：代表解压
示例：将/usr/tmp 下的ab.tar解压到当前目录下

示例：将/usr/tmp 下的ab.tar解压到根目录/usr下
tar -xvf ab.tar -C /usr------C代表指定解压的位置

ee 文件重定向到文件和屏幕。

```
cat file.unl | tee file_20171101.log
cat file.unl | tee -a file_20171101.log // -a表示文件重定向时使用追加模式
```

 unzip 解压缩.zip后缀的压缩包

```
unzip file.zip //将file.zip压缩到解压到当前目录
unzip -o file.zip -d /home //将file.zip压缩包在指定目录/home下解压缩，如果已有相同的文件存在，会覆盖原先的文件。
unzip -n file.zip -d /home //将file.zip压缩包在指定目录/home下解压缩，如果已有相同的文件存在，不会覆盖原先的文件。 
unzip -v file.zip //查看压缩文件目录，但不解压。
```

 unrar  解压缩.rar后缀的压缩包

```
unrar x file.rar //解压文件到当前目录，保持原目录结构
unrar e file.rar //解压文件到当前目录,压缩的子目录下的文件也会直接放置在当前目录
unrar l file.rar //查看rar中的文件
```

scp 远程文件传输，通常用于两台服务期之间文件传输或者同一服务器不用用户间的文件传输

```
//本地文件或目录拷贝到文件服务器
scp file1 root@192.168.0.1:/home  //将本地文件file上传到192.168.0.1服务器的root用户的/home目录下。
scp -r dir1 root@192.168.0.1:/home  //将本地dir1目录下的所有文件和目录上传到192.168.0.1服务器的root用户的/home目录下。

//从远程服务器拷贝文件到本地目录
scp  root@192.168.0.1:/home/file1 /opt //将192.168.0.1服务器上的root用户/home目录下的file1文件下载到本地/opt目录下
scp  -r root@192.168.0.1:/home  /opt //将192.168.0.1服务器上的root用户/home目录下的所有文件和目录下载到本地/opt目录下
```

find 查找文件或目录

```
find /opt -name "*.txt" //在opt目录下查找文件名后缀为.txt的文件
find /home -size +100M  //在home目录下查找大于100M的文件
```

#### （五）、文件查看命令

 cat 查看文件内容

```
cat file1.unl //查看file1.unl文件里的内容
cat -n file1.unl //带行号显示file1.unl文件里的内容,包括空行
cat -b file1.unl //带行号显示file1.unl文件里的内容，空行不编号
cat -A file1.unl //查看file1.unl文件里的内容,可同时查看不可打印字符。如结束符$，TAB空格^I、DOS结束符^MS
cat file1.unl | more //查看file1.unl文件里的内容，可翻页查看。常用于数据量大情况
```

 more 分页显示文件内容。常用于查看超大文件

```
more file.unl
```

 head 显示文件的开头的内容。在默认情况下，head命令显示文件的头10行内容

```
head file.unl //显示文件的前10行内容,不带参数默认输出10行
head -n 15 file.unl //显示文件的前15行内容
head -n -20 file.unl //查看文件除了最后20行的内容
```

 tail 查看文件最后几行或实时日志

```
tail file.unl //查看文件file.unl的最后10行
tail -n 15 file.unl //查看文件file.unl的最后15行
tail +15 file.unl //查看文件第15行至文件末尾的内容 
tail -c 10 file.unl //查看文件file的最后10个字符
tail -f file.log //实时查看file.log新增内容。常用于日志查看，特别常用
```

 nl 查看文件内容并会自动带行号

```
nl file.unl //带行号展示文件内容，文件中的空白行不加行号
nl -b a file.unl //带行号展示文件内容，文件中的空白行也会加行号
```

 diff 比较两个文件内容

```
diff file1.unl file2.unl -y -W 150 
```

####  （六）、用户管理命令

useradd 创建用户。下述指令表示创建oracle用户，其中属主为dba，属组为oinstall，家目录为/home/oracle，shell为/bin/bash。-m表示创建家目录。

```
useradd -g dba -G oinstall -m -d /home/oracle -s /bin/bash oracle
```

usermod 修改用户基本信息

```
usermod -s /bin/bash oracle //修改oracle用户使用shell为/bin/bash
usermod -g dba oracle //修改oracle用户所属用户组为dba
usermod -G oinstall oracle //修改oracle用户附加所属用户组为oinstall
usermod -a -G oinstall oracle //增加oracle用户附加所属用户组为oinstall。
usermod -d /opt/oracle oracle //修改oracle用户家目录为/opt/oracle
usermod -c "create for test" oracle //修改oracle用户创建说明
```

userdel 删除用户

```
userdel oracle //删除oracle用户，但不删除用户相关的文件
userdel -r oracle //删除oracle用户，同时删除用户家目录及相关文件
userdel -rf oracle //强制删除oracle用户及用户家目录相关文件，即使用户当前已登录。
```

groupadd 增加用户组

```
groupadd -g 200 dba //增加dba用户组，并且指定组ID为200
```

groupdel 删除用户组

```
groupdel dba //删除dba用户组
```

passwd 修改用户密码

```
passwd //不带用户名，修改当前用户密码，按照提示输入操作
passwd oracle //修改oracle密码
```

su 切换到其他用户

```
su - oracle //切换到oracle用户,并改变工作目录为oracle家目录
```

#### （七）、网络通信命令

ping 测试主机之间网络连通情况

```
ping 192.168.0.1 //测试本机与192.168.0.1的连通情况
```

telnet 登录远程服务器

```
telnet 192.168.0.1 //登录192.168.0.1服务器
```

ssh 使用ssh加密协议实现安全的远程登录服务器

```
ssh 192.168.0.1  //登录192.168.0.1服务器
ssh oracle@192.168.0.1  //使用oracle用户登录192.168.0.1服务器
```

netstat 查看网络状态信息

```
etstat -ano //查看所有端口连接信息
netsat -ano | grep "1521" //查看1521端口连接信息
```

ftp/sftp 本地和远程服务器间文件上传、下载

```
ftp 192.168.0.1 //按照提示输入用户名和密码
ftp oracle@192.168.0.1 //指定用户按照提示输入oracle密码

#后续交互常用操作实例
#1、从远程服务器oracle用户的/home/oracle/package目录下载oracle.tar.gz文件
ftp oracle@192.168.0.1 //指定用户按照提示输入oracle密码
ftp>pwd <- 查看当前操作的远程服务器目录
ftp>cd package <- 进入package家目录
ftp>binary <- 二进制方式传输，如果是文本文件，输入ascii
ftp>get oracle.tar.gz <- 下载oracle.tar.gz文件
ftp>bye <- 退出

#1、从本地服务器上传文件到远程服务器的oracle用户家目录下
ftp oracle@192.168.0.1 //指定用户按照提示输入oracle密码
ftp>ascii <- 文本方式传输，如果是非文本文件，输入binary
ftp>put data.unl <- 上传data.unl文件
ftp>bye <- 退出
```

说明：sftp命令操作方法同ftp

#### （八）、系统管理命令

who 显示目前登录系统的用户信息

```
who
```

uname 打印当前系统相关信息(内核版本号、硬件架构、主机名称和操作系统类型等)

```
uname //显示操作系统名称,相当于uname -s
uname -a //显示全部信息
uname -r //显示操作系统发行编号
```

getconf 查看当前系统是32位还是64位

```
getconf LONG_BIT
```

ifconfig 查看和配置网卡信息

```
ifconfig //查看网卡信息
```

top 查看系统的整体运行情况

```
top
```

ps 查看系统进程状态

```
ps -aux //查看所有进程
ps -ef | grep "oracle" //查看oracle进程
```

kill 删除执行中的程序或工作

```
kill -9 6603 //删掉ID为6603的进程
```

free 显示当前系统内存使用情况

```
free -m //以MB为单位显示内存使用情况，也可以是-k、-b或不带参数
```

df 显示磁盘分区使用情况

```
df //以KB为单位显示分区使用情况,可以带参数-m
df -h //以可读性较高的方式显示分区情况
df -i //显示各分区inode使用情况
df -T //显示各分区文件系统类型
```

du 查看文件或目录占用空间情况

```
du //显示当前所有目录或者文件所占空间
du debug.log //查看debug.log文件占用空间大小
du -sm dir1 //查看dir1占用空间统计
du -sm * //查看当前目录下所有目录或者文件汇总占用空间
```

time 查看命令执行所耗费时间

```
time ls //查看执行ls命令执行所耗费时间
```

date 查看和设置系统日期和时间

```
date //查看当前日期和时间，默认格式输出
date '+%Y-%m-%d %H:%M:%S' //查看系统当前日期和时间。20171126
date -s '20171120 07:01:01' //设置日期和时间
```

reboot 重启服务器

```
reboot //重启服务器
```

####  （九）、磁盘管理命令

fdisk 查看当前服务器磁盘或磁盘分区情况

```
fdisk -l //查看磁盘情况
```

mount 挂载文件系统

```
mount /dev/sda3 /home //挂载文件系统
```

umount  卸载已经加载的文件系统

```
umount /home //卸载挂载点/home
```

sync 强制被改变的内容立刻写入磁盘

```
sync;sync;sync
```

### 六、工具介绍

- Xshell
- Xftp
- SecureCRT

> 使用流程类似，作用一样：可以在Windows界面下用来访问远端不同系统下的[服务器](https://baike.baidu.com/item/服务器/100571)，进行文件传输交换。

注册下载Xshell和Xftp

![image-20211123223414751](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111241025659.png)

使用SecureCRT，远程连接云服务器。

![image-20211123224247262](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111241025004.png)

![image-20211123224253948](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111241025738.png)



使用Xshell

![image-20211124093424864](https://zhou431615-myblog.oss-cn-beijing.aliyuncs.com/blogPic/202111241026234.png)

