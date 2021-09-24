# Linux

## 1、命令

* 1.常用命令

service network restart –重启网卡

ip addr 查看ip ifconfig -a 

uname –r 查看内核版本（3.1以上）

curl  `http://localhost:8080`

ctrl+l ：清屏

tail -f logic.out动态更新

service network restart

date查看系统日期

ll -rt 时间倒序显示

mkdir -p japan/cangls 递归创建目录

tab 可以实现命令与目录补全

rmdir 删除空目录

rm -rf bbb/ 强制删除

touch 创建文件

netstat -anp |grep 8253 查看端口情况

vi /etc/sysconfig/network-scripts/ifcfg-eth0 修改ip

hostnamectl set-hostname  master 设置主机名称

https://blog.51cto.com/4837471/2140674 免密登录

* 2.`[root@localhost ~]#`

其中:root :当前登录用户

localhost 主机名

~当前所在目录(家目录)

`#超级用户的提示符`

普通用户的提示符是$

* 3.复制命令:`cp[选项] [原文件或目录] [目标目录]`

命令英文原意: copy

选项:

-r 复制目录

-p 连带文件属性复制

-d 若源文件是链接文件,则复制链接属性

-a 相当于-pdr

* 4.yum

yum update 升级内核

yum install curl安装

* 5.systemctl

systemctl start/stop docker 启动/关闭docker

systemctl enable docker 开机启动

systemctl disable docker 关闭开机启动

* 6.查询目录中内容: ls

`ls [选项] [文件或目录]`

选项:

-a 显示所有文件,包括隐藏文件

-l 显示详细信息

-d 查看目录属性

-h 人性化显示文件大小

-i 显示inode


![文件](/img/9.png) 

* 7.cd

cd ..   返回上一级目录

cd ../..   返回上两级目录

cd或cd ~    返回home目录

cd - 目录名  返回指定目录

* 8.ps

ps -ef|grep "hlcar-logic"

`ps [选项]`

-e 显示所有进程。

-f 全格式。

-h 不显示标题。长格式。

-W 宽输出。

a 显示终端_上的所有进程，包括其他用户的进程。

r 只显示正在运行的进程。以用户为主的格式来显示程序状况。

x 显示所有程序，不以终端机来区分。

* 9.链接命令: ln

`ln -s [原文件] [目标文件]`

命令英文原意: link

功能描述:生成链接文件

选项:

-s 创建软链接

硬链接特征:

1)拥有相同的1节点和存储block块,可以看做是同一一个文件

2)可通过节点识别

3)不能跨分区

4)不能针对目录使用   

软链接特征:

1)类似Windows快捷方式

2)软链接拥有自己的节点和Block块,但是数据块中只保存原

文件的文件名和节点号,并没有实际的文件数据

3)lrwxrwxrwx l 软链接软链接文件权限都为rwxrwxrwx

4)修改任意文件，另一个都改变

5)删除原文件,软链接不能使用

* 10.locate命令格式

locate文件名

在后台数据库中按文件名搜索,搜索速度更快

/var/lib/mlocate locate命令所搜索的后台数据库

updatedb更新数据库 数据库是每天更新。可以强制更新数据库

/etc/updatedb.conf配置文件

PRUNE_ BIND_ MOUNTS= "yes" 开启搜索限制

PRUNEFS = 搜索时,不搜索的文件系统

PRUNENAMES = 搜索时,不搜索的文件类型

PRUNEPATHS = 搜索时,不搜索的路径

* 11.搜索命令的命令whereis 搜索命令所在路径及帮助文档所在位置

选项:

-b :只查找可执行文件

-m :只查找帮助文件

--whereis ls

* 12.find

1)基础

-name<查询方式>按照指定的文件名查找模式查找文件

-user<用户名>查找属于指定用户名所有文件

-size<文件大小>按照指定的文件大小查找文件。

案例1:按拥有者:查找/opt目录下，用户名称为nobody 的文件

--find /opt user nobody

案例2:查找整个linux系统下大于20m的文件(+n大于-n小于n等于)

--find / -size +20M

案例3:搜索文件

--find / -name install.log

案例4:查找没有所有者的文件(内核产生的文件可能没有所有者。u盘也可能没有所有者。(sys、tem))

--find /root -nouser 

案例5:査找10天前修改的文件(+n大于-n小于n等于)atime文件访问时间 ctime  改変文件属性 mtime 修改文件内容

--find /var/log/ -mtime +10 

案例6:査找文件大小是25KB的文件(+n大于-n小于n等于)

--find . -size 25k

案例7:査找i节点是262422的文件

--find -inum 262422

案例8:査找/etc/目彖下,大于20KB井且小于50KB的文件

--find /etc -size + 20k -a -size -50k

査找/etc/目彖下,大于20KB井且小于5OKB的文件,并显示详情

--`find /etc -size +20k -a -size -50k -exec Is -h {}\`

找到刪除.

--`find /root - inum 262421 -exec rm -rf {} \`;

避免大范围搜索,会非常耗费系统资源

find是在系统当中搜索符合条件的文件名。如果需要匹配,

使用通配符匹配,通配符是完全匹配

2)Linux中的通配符

`*匹配任意内容`

?  匹配任意一个字符

[]  匹配任意-个中括号内的字符

`[-]匹配中括号中任意一个字符，-代表一个范围。例如: [a-2]代表匹配一个小写字母。`

`[^]逻辑非，表示匹配不是中括号内的一一个字符。例如:[^0-9]代表匹配一个不是数字的字符。`

-- find /root -name "install.1og*" 

-- find /root -name "*”

-- find /root -name `ab [cd]`

-- find /root -iname install.log  不区分大小写

* 13.搜索命令的命令which

which 文件名

搜索命令所在路径及别名

* 14.搜索字符串命令grep 

`grep [选项]字符串文件名`

选项:

-i 忽略大小写

-v 排除指定字符串

-n 显示匹配行及行号

grep指令和管道符号

grep过滤查找，管道符， "|"，表示将前一一个命令的处理结果输出传递给后面的命令处理。

基本语法

案例1:请在hello.txt文件中，查找"yes"所在行，不区分大小写，并且显示行号

-- cat hello.txt | grep -ni yes

grep -C 5 foo file 显示file文件里匹配foo字串那行以及上下5行

grep -B 5 foo file 显示foo及前5行

grep -A 5 foo file 显示foo及后5行

find命令与grep命令的区别

find命令:在系统当中搜索符合条件的文件名,如果需要匹配，使用通配符匹配,通配符是完全匹配

grep命令:在文件当中搜索符合条件的字符串,如果需要匹配,使用正则表达式进行匹配,正则表达式时包含匹配

* 15.man的级别

查看命令的帮助

查看可被内核调用的函数的帮助

查看函数和函数库的帮助

查看特殊文件的帮助(主要是/dev目录下的文件)

查看配置文件的帮助

查看游戏的帮助

查看其它杂项的帮助

查看系统管理员可用命令的帮助

查看和内核相关文件的帮助

查看命令拥有那个级别的帮助

man -f命令相当于whatis命令

举例:

--man -5 passwd

--man -4 null

--man -8 ifconfig

查看和命令相关的所有帮助

man -k命令相当于apropos命令

例如

--apropos passwd

* 16.选项帮助

命令--help 获取命令选项的帮助

-- ls --help

shell内部命令帮助

help shell内部命令 获取shel内部命令的帮助

-- whereis cd 确定是否是shell内部命令

-- help cd 获取内部命令帮

* 17.详细命令帮助info

info命令

回车:进入子帮助页面 (带有*号标记)

-u: 进入上层页面

-n: 进入下一个帮助小节

-p: 进入上一个帮助小节

-q: 退出

* 18.压缩

常用压缩格式: .zip.gz .bz2

常用压缩格式: .tar.gz.tar.bz2

1) .zip格式压缩

zip压缩文件名 源文件

压缩文件

zip -r 压缩文件名源目录

压缩目录

unzip 压缩文件

解压缩.zip文件

2) .gz格式压缩

gzip源文件

压缩为.gz格式的压缩文件,源文件会消失

gzip -c 源文件>压缩文件

压缩为.gz格式,源文件保留

例如:

gzip -C cangls > cangls.gz

gzip -r 目录

压缩目录下所有的子文件,但是不能压缩目录

.gz格式解压缩
gzip -d 压缩文件

解压缩文件

gunzip压缩文件

解压缩文件

3) .bz2格式压缩

bzip2源文件

压缩为.bz2格式,不保留源文件

bzip2 -k源文件

压缩之后保留源文件

注意: bzip2命令不能压缩目录

.bz2格式解圧缩

bzip2 -d圧缩文件

解圧缩, -k保留圧缩文件

bunzip2圧缩文件

解圧缩, -k保留圧缩文件

常用圧缩格式: .zip .gz .bz2

常用圧缩格式: .tar.gz

* 19.打包命令tar

tar -cvf 打包文件名源文件

迭项:

-c: 打包

-v: 显示过程

-f: 指定打包后的文件名

-- tar -cvf longzls.tar longzls

解打包命令

tar -xvf 打包文件名

-x 解打包

tar -xvf longzls.tar


.tar.gz圧缩格式

其实.tar.gz格式是先打包为.tar格式,再圧缩为.gz格式

tar -zcvf **被圧缩包名.tar.gz** 源文件

迭项:

-z: 圧缩为.tar.gz格式


tar -zxvf **被解圧缩包名tar.gz**

选项:

-x：解圧缩.tar.gz格式


.tar.bz2圧缩格式

tar -jcvf 圧缩包名.tar.bz2源文件

选项:

-z: 圧缩为.tar.bz2格式

tar -jxvf圧缩包名.tar.bz2

选项:

-x: 解圧缩.tar.bz2格式

* 20. tail指令

tail用于输出文件中尾部的内容，默认情况下tail指令显示文件的后10行内容。

tail文件  (功能描述，查看文件后10行内容)

tail -n5 文件  (功能描述，查看文件后5行内容，5可以是任意行数)

tail -f 文件  (功能描述，实时追踪该文档的所有更新)应用实例

* 21.查看与设定别名

alias 查看系统中所有的命令别名

alias别名= '原命令' 设定命令别名

vi ~/.bashrc 写入坏境変量配置文件永久生效

unalias別名 刪除別名

source .bashrc 修改文件别名后执行这个生效，或者重新登录。。

命令生效顺序

第一顺位执行用绝对路径或相对路径执行的命令。第二顺位执行别名。

第三顺位执行Bash的内部命令。

第四顺位执行按照$PATH环境变量定义的目录查找顺序找到的第-一个命令

* 22.history

-c :清空万史命令

-w :把緩存中的历史命令写入历史命令保存文件

* 23.less

是根据湿示需要加载内容,对于显示大型文件具有较高的效率.

空格键或者pagedown 向下翻一页

pageup 向上翻一页

/字符串 向下查找 n下一个 N上一个

?字符串 向上查找 n上一个 N下一个

q 退出


* 24.vi

:n可以下翻文件  :N是上翻文件 ：prev也能切换到前一个文件

:! 强制执行

:ls  列出所有文件 

:n  到下一个文件 

:15  定位于第15行

/xxx 往后搜索定位xxx 

?xxx 往前搜索xxx

拷贝当前行yy,拷贝当前行向下的5行5yy， 并粘贴。

删除当前行dd,删除当前行向下的5行5dd

设置文件的行号，取消文件的行号 命令行下: set nu和:set nonu

vim

查找与替换

/字串   往游标之后寻找该字串。

?字串   往游标之前寻找该字串。

n    往下继续寻找下一个相同的字串。

N    往上继续寻找下一个相同的字串。

%   查找“(”，“)”，“{”，“}”的配对符。

s   搜寻某行列范围。

g   搜寻整个编辑缓冲区的资料。

`:1,$s/old/new/g` 将文件中所有的『old』改成『new』


* 25.useradd用户名应用案例

passwd  用户名

userdel  用户名

![例子](/img/10.png) 


* 26. 修改环境变量 --vim ~/.bash_profile  --source ~/.bash_profile

* 27. 关闭防火墙

当前关闭：service iptables stop

永久关闭：chkconfig iptables off

systemctl disable firewalld.service  开机禁用防火墙

systemctl stop firewalld

* 28. 查看端口 ss -tanl

* 29. 编辑网卡的配置文件 --vim /etc/sysconfig/network-scripts/ifcfg-enp0s3

首先需要将BOOTROTO由dhcp改为static，否则配置无效，dhcp表示使用动态IP；

ONBOOT需要配置yes；

* 30. 改主机名：--vi /etc/sysconfig/network

* 31. kill -9 pid

kill -9 pid等于kill -s 9 pid，表示强制，尽快终止一个进程。多半admin会用这个命令。

killall命令用于杀死指定名字的进程（kill processes by name）之前使用ps等命令再配合grep来查找进程，而killall把这两个过程合二为一，是一个很好用的命令

eg：killall mongod

* 32.cat 査看文件

空格键 向下翻页

Enter 向下一行

q 退出

Crl+F 向下滚屏

Ctrl+B 向上滚屏

## 2、硬件设备文件名

STATA 每秒500M、逻辑分区从5开始

|硬件设备|文件名|
|:--:|:--:|
|IDE硬盘|/dev/hd[a-d]|
|SCSI/SATA/USB硬盘|/dev/sd[a-p]|
|光驱|/dev/cdrom或/dev/hdc|
|软盘|/dev/fd[0-1]|
|打印机(25针)|/dev/1p[0-2]|
|打印机(USB )|/dev/usb/1p[0-15]|
|鼠标|/dev/mouse|

## 3、分区目录

* 1.必须分区 / (根分区)
 
swap分区( 交换分区,内存2倍,不超过2GB )

* 2.推荐分区

/boot (启动分区, 200MB )

* 3.Boot分区单独分区，防止空间满启动不了

* 4.独立空间，互不影响，方便管理

![文件系统结构](/img/8.png) 

* 5.常用目录的作用

/根目录

/bin命令保存目录(普通用户就可以读取的命令)

/boot启动目录,启动相关文件

/dev设备文件保存目录

/etc配置文件保存目录

/home普通用户的家目录

/lib系统库保存目录

/mnt系统挂载目录

/media挂载目录

proc和sys目录不能直接操作,这两个目录保存的是内存的过载点。

/root超级用户的家目录

/tmp临时目录

/sbin命令保存目录(超级用户才能使用的目录)

/proc直接写入内存的

/sys

/usr系统软件资源目录

/usr/bin/系统命令(普通用户)

/usr/sbin/系统命令(超级用户)

/var系统相关文档内容

root、sys、home其他目录不要动，用这三个目录。

Boot 启动分区，home分区 /跟分区，swap虚拟内存

## 4、系统命令

1)shutdown命令

`shutdown [选项]时间`

选项:

-c: 取消前一一个关机命令

-h: 关机

-r: 重启

2)其他关机命令

--halt

--poweroff

--init 0

3)其他重启命令

-- reboot

-- init 6

3)系统运行级别

0 关机

1 单用户

2 不完全多用户,不含NFS服务

3 完全多用户

4 未分配

5 图形界面

6 重启

runlevel查看运行级别前级别当前级别

logout退出当前用户，也就是注销

## 5、常用快捷键

ctrl+c  强制终止当前命令

ctrl+l 清屏

ctrl+a 光标移动到命令行首

ctrl+e 光标移动到命令行尾

ctrl+u 从光标所在位置删除到行首

ctrl+z 把命令放入后台

ctrl+r 在历史命令中搜索


## 网络诊断工具

ping 可以用来帮助我们进行网络连通性的探测。
ifconfig，用来显示当前系统中的所有网络设备。
netstat 和 lsof 可以查看活动的连接状况。
tcpdump 可以对各种奇怪的环境进行抓包，进而帮我们了解报文，排查问题。










