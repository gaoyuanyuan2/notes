## Linux
### 1、命令
1.常用命令
<br><br>service network restart –重启网卡
<br><br>ip addr 查看ip ifconfig -a 
<br><br>uname –r 查看内核版本（3.1以上）
<br><br>curl  http://localhost:8080
<br><br>Ctrl+l ：清屏
<br><br>tail -f logic.out动态更新
<br><br>service network restart
<br><br>date查看系统日期
<br><br>ll -rt 时间倒序显示
<br><br>mkdir -p japan/cangls 递归创建目录
<br><br>tab 可以实现命令与目录补全
<br><br>rmdir 删除空目录
<br>rm -rf bbb/ 强制删除
<br><br>2.[root@localhost ~]#
<br>其中:root :当前登录用户
<br>localhost 主机名
<br>~当前所在目录(家目录)
<br>#超级用户的提示符
<br>普通用户的提示符是$
<br><br>3.复制命令:cp[选项] [原文件或目录] [目标目录]
<br>命令英文原意: copy
<br>选项:
<br>-r复制目录
<br>-p连带文件属性复制
<br>-d若源文件是链接文件,则复制链接属性
<br>-a相当于-pdr
<br><br>4.yum update 升级内核
<br>yum install docker 安装docker
<br>yum install curl安装
<br><br>5.systemctl start/stop docker 启动/关闭docker
<br>systemctl enable docker 开机启动
<br>systemctl disable docker 关闭开机启动
<br><br>6.查询目录中内容: ls
<br>ls [选项] [文件或目录]
<br>选项:
<br>-a 显示所有文件,包括隐藏文件
<br>-l 显示详细信息
<br>-d 查看目录属性
<br>-h 人性化显示文件大小
<br>-i 显示inode
<br>![文件](https://github.com/gaoyuanyuan2/notes/blob/master/img/9.png) 
<br><br>7.cd ..   返回上一级目录
<br>cd ../..   返回上两级目录
<br>cd或cd ~    返回home目录
<br>cd - 目录名  返回指定目录
<br><br>8.ps -ef|grep "hlcar-logic"
<br>ps [选项]
<br>-e显示所有进程。
<br>-f全格式。
<br>-h不显示标题。长格式。
<br>-W宽输出。
<br>a显示终端_上的所有进程，包括其他用户的进程。
<br>r只显示正在运行的进程。以用户为主的格式来显示程序状况。
<br>X显示所有程序，不以终端机来区分。

<br><br>9.链接命令: In
<br>In -S [原文件] [目标文件]
<br>命令英文原意: link
<br>功能描述:生成链接文件
<br>选项:
<br>-s创建软链接
<br>硬链接特征:
<br>1、拥有相同的1节点和存储block块,可以看做是同一一个文件
<br>2、可通过节点识别
<br>3、不能跨分区
<br>4、不能针对目录使用      
<br>软链接特征:
<br>1、类似Windows快捷方式
<br>2、软链接拥有自己的节点和Block块,但是数据块中只保存原
<br>文件的文件名和节点号,并没有实际的文件数据
<br>3、lrwxrwxrwx l 软链接软链接文件权限都为rwxrwxrwx
<br>4、修改任意文件，另一个都改变
<br>5、删除原文件,软链接不能使用

<br><br>10.locate命令格式
<br>locate文件名
<br>在后台数据库中按文件名搜索,搜索速度更快
<br>/var/lib/mlocate locate命令所搜索的后台数据库
<br>updatedb更新数据库 数据库是每天更新。可以强制更新数据库
<br>/etc/updatedb.conf配置文件
<br>PRUNE_ BIND_ MOUNTS= "yes" 开启搜索限制
<br>PRUNEFS = 搜索时,不搜索的文件系统
<br>PRUNENAMES = 搜索时,不搜索的文件类型
<br>PRUNEPATHS = 搜索时,不搜索的路径

<br><br>11.搜索命令的命令whereis 搜索命令所在路径及帮助文档所在位置
<br>选项:
<br>-b :只查找可执行文件
<br>-m :只查找帮助文件
<br>--whereis ls

<br><br>12.find
1)
<br>-name<查询方式>按照指定的文件名查找模式查找文件
<br>user<用户名>查找属于指定用户名所有文件
<br>-size<文件大小>按照指定的文件大小查找文件。
<br>案例1:按拥有者:查找/opt目录下，用户名称为nobody 的文件
<br>--find /opt user nobody
<br>案例2:查找整个linux系统下大于20m的文件(+n大于-n小于n等于)
<br>--find / -size +20M
<br>案例3:搜索文件
<br>--find / -name install.log
<br>案例4:查找没有所有者的文件(内核产生的文件可能没有所有者。u盘也可能没有所有者。(sys、tem))
<br>--find /root -nouser 
<br>案例5:査找10天前修改的文件(+n大于-n小于n等于)atime文件访问时间 ctime  改変文件属性 mtime 修改文件内容
<br>--find /var/log/ -mtime +10 
<br>案例6:査找文件大小是25KB的文件(+n大于-n小于n等于)
<br>--find . -size 25k
<br>案例7:査找i节点是262422的文件
<br>--find -inum 262422
<br>案例8:査找/etc/目彖下,大于20KB井且小于50KB的文件
<br>--find /etc -size + 20k -a -size -50k
<br>査找/etc/目彖下,大于20KB井且小于5OKB的文件,并显示详情
<br>--find /etc -size +20k -a -size -50k -exec Is -h {} \
<br>找到刪除.
<br>--find /root - inum 262421 -exec rm -rf {} \;
<br>避免大范围搜索,会非常耗费系统资源
<br>find是在系统当中搜索符合条件的文件名。如果需要匹配,
<br>使用通配符匹配,通配符是完全匹配
<br>2)Linux中的通配符
<br>*匹配任意内容
<br>?  匹配任意一个字符
<br>[]  匹配任意-个中括号内的字符
<br>-- find /root -name "install.1og*" 
<br>-- find /root -name "*”
<br>-- find /root -name "ab [cd]"
<br>-- find /root -iname install.log  不区分大小写


<br><br>13.搜索命令的命令which
<br>which 文件名
<br>搜索命令所在路径及别名

<br><br>14.搜索字符串命令grep 
<br>grep [选项]字符串文件名
<br>选项:
<br>-i忽略大小写
<br>-v排除指定字符串
<br>-n显示匹配行及行号
<br>grep指令和管道符号
<br>grep过滤查找，管道符， "|"，表示将前一一个命令的处理结果输出传递给后面的命令处理。
<br>基本语法
<br>案例1:请在hello.txt文件中，查找"yes"所在行，不区分大小写，并且显示行号
<br>-- cat hello.txt| grep -ni yes
<br>find命令与grep命令的区别
<br>find命令:在系统当中搜索符合条件的文件名,如果需要匹配，使用通配符匹配,通配符是完全匹配。
<br>grep命令:在文件当中搜索符合条件的字符串,如果需要匹配,使用正则表达式进行匹配,正则表达式时包含匹配

<br><br>15.man的级别
<br>查看命令的帮助
<br>查看可被内核调用的函数的帮助
<br>查看函数和函数库的帮助
<br>查看特殊文件的帮助(主要是/dev目录下的文件)
<br>查看配置文件的帮助
<br>查看游戏的帮助
<br>查看其它杂项的帮助
<br>查看系统管理员可用命令的帮助
<br>查看和内核相关文件的帮助
<br>查看命令拥有那个级别的帮助
<br>man -f命令相当于whatis命令
<br>举例:
<br>-man -5 passwd
<br>--man -4 null
<br>--man -8 ifconfig
<br>查看和命令相关的所有帮助
<br>man -k命令相当于apropos命令
<br>例如
<br>--apropos passwd

<br><br>16.选项帮助
<br>命令--help 获取命令选项的帮助
<br>-- ls --help
<br>shell内部命令帮助
<br>help shell内部命令 获取shel内部命令的帮助
-- whereis cd 确定是否是shell内部命令
-- help cd 获取内部命令帮助

<br><br>17.详细命令帮助info
<br>info命令
<br>回车:进入子帮助页面 (带有*号标记)
<br>-u:进入上层页面
<br>-n:进入下一个帮助小节
<br>-p:进入上一个帮助小节
<br>-q:退出

<br><br>18.压缩
<br>常用压缩格式:.zip.gz .bz2
<br>常用压缩格式:.tar.gz.tar.bz2
<br>1).zip格式压缩
<br>zip压缩文件名 源文件
<br>#压缩文件
<br>zip -r 压缩文件名源目录
<br>#压缩目录
<br>unzip 压缩文件
<br>#解压缩.zip文件
<br>2).gz格式压缩
<br>gzip源文件
<br>压缩为.gz格式的压缩文件,源文件会消失
<br>gzip -c 源文件>压缩文件
<br>#压缩为.gz格式,源文件保留
<br>例如:
<br>gzip -C cangls > cangls.gz
<br>gzip -r 目录
<br>#压缩目录下所有的子文件,但是不能压缩目录
<br>.gz格式解压缩
gzip -d 压缩文件
<br>#解压缩文件
<br>gunzip压缩文件
<br>#解压缩文件
<br>3).bz2格式压缩
<br>bzip2源文件
<br>#压缩为.bz2格式,不保留源文件
<br>bzip2 -k源文件
<br>#压缩之后保留源文件
<br>注意: bzip2命令不能压缩目录
<br>.bz2格式解圧缩
<br>bzip2 -d圧缩文件
<br>#解圧缩, -k保留圧缩文件
<br>bunzip2圧缩文件
<br>#解圧缩, -k保留圧缩文件
<br>常用圧缩格式: .zip .gz .bz2
<br>常用圧缩格式: .tar.gz

<br><br>19.打包命令tar
<br>tar -cvf 打包文件名源文件
<br>迭项:
<br>-c :打包
<br>-v; 显示过程
<br>-f:指定打包后的文件名
<br>-- tar -cvf longzls.tar longzls
<br>解打包命令
<br>tar -xvf 打包文件名
<br>-x 解打包
<br>tar -xvf longzls.tar
<br>.tar.gz圧缩格式
<br>其实.tar.gz格式是先打包为.tar格式,再圧缩为.gz格式
<br>tar -zcvf 圧缩包名.tar.gz源文件
<br>迭项:
<br>-z:圧缩为.tar.gz格式
<br>tar -zxvf 圧缩包名tar.gz
<br>选项:
<br>-x ：解圧缩.tar.gz格式
<br>.tar.bz2圧缩格式
<br>tar -jcvf 圧缩包名.tar.bz2源文件
<br>选项:
<br>-Z :圧缩为.tar.bz2格式
<br>tar -jxvf圧缩包名.tar.bz2
<br>选项:
<br>-X :解圧缩.tar.bz2格式


### 2、docker命令
1.docker –v 查看版本
<br><br>2.docker search 
<br><br>3.docker pull
<br><br>4.运行  docker run --name container-name -d image name  --name :自定义容器名
<br>eg:docker run -name myredis -d redis  -d:后台运行
<br>image name:指定镜像模板
<br><br>5.列表  docker ps (查看运行中的容器) ; <br> 加上a;可以查看所有容器停止 <br> docker stop container-name/container-id  停止当前你运行的容器启动  <br>docker 
start container-name/container id  启动容器
<br><br>6.删除  docker rm container-id  删除指定容器
<br><br>7.端口映射  -p 6379:6379  -p:主机端口(映射到)容器内部的端口
<br>eg:docker run -d -p 6379:6379 -name myredis docker.io/redis
<br><br>8.容器日志docker logs container name/container id
### 3、硬件设备文件名
|硬件设备|文件名|
|:--:|:--:|
|IDE硬盘|/dev/hd[a-d]|
|SCSI/SATA/USB硬盘|/dev/sd[a-p]|
|光驱|/dev/cdrom或/dev/hdc|
|软盘|/dev/fd[0-1]|
|打印机(25针)|/dev/1p[0-2]|
|打印机(USB )|/dev/usb/1p[0-15]|
|鼠标|/dev/mouse|
<br><br>STATA 每秒500M、逻辑分区从5开始
### 4、分区目录
 1.必须分区 / (根分区)
<br>swap分区( 交换分区,内存2倍,不超过2GB )
<br><br>2.推荐分区
<br>/boot (启动分区, 200MB )
<br><br>3.Boot分区单独分区，防止空间满启动不了
<br><br>4.独立空间，互不影响，方便管理
<br><br>![文件系统结构](https://github.com/gaoyuanyuan2/notes/blob/master/img/8.png) 
<br><br>5.常用目录的作用
<br>/根目录
<br>/bin命令保存目录(普通用户就可以读取的命令)
<br>/boot启动目录,启动相关文件
<br>/dev设备文件保存目录
<br>/etc配置文件保存目录
<br>/home普通用户的家目录
<br>/lib系统库保存目录
<br>/mnt系统挂载目录
<br>/media挂载目录
<br>proc和sys目录不能直接操作,这两个目录保存的是内存的过载点。
<br>/root超级用户的家目录
<br>/tmp临时目录
<br>/sbin命令保存目录(超级用户才能使用的目录)
<br>/proc直接写入内存的
<br>/sys
<br>/usr系统软件资源目录
<br>/usr/bin/系统命令(普通用户)
<br>/usr/sbin/系统命令(超级用户)
<br>/var系统相关文档内容
<br>root、sys、home其他目录不要动，用这三个目录。
### 5、系统命令
1)shutdown命令
<br>shutdown [选项]时间
<br>选项:
<br>-c:取消前一一个关机命令
<br>-h:关机
<br>-r:重启
<br>2)其他关机命令
<br>--halt
<br>--poweroff
<br>--init 0
<br>3)其他重启命令
<br>-- reboot
<br>-- init 6
<br>3)系统运行级别
<br>0关机
<br>1单用户
<br>2不完全多用户,不含NFS服务
<br>3完全多用户
<br>4未分配
<br>5图形界面
<br>6重启
<br>runlevel查看运行级别前级别当前级别,
<br>logout退出当前用户，也就是注销，












