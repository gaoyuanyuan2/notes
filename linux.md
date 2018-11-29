## Linux
### 1、命令
1.常用命令
<br><br>service network restart –重启网卡
<br><br>ip addr 查看ip ifconfig -a 
<br><br>uname –r 查看内核版本（3.1以上）
<br><br>curl  `http://localhost:8080`
<br><br>ctrl+l ：清屏
<br><br>tail -f logic.out动态更新
<br><br>service network restart
<br><br>date查看系统日期
<br><br>ll -rt 时间倒序显示
<br><br>mkdir -p japan/cangls 递归创建目录
<br><br>tab 可以实现命令与目录补全
<br><br>rmdir 删除空目录
<br>rm -rf bbb/ 强制删除
<br><br>touch 创建文件

<br>netstat -anp |grep 8253 查看端口情况

<br>2.[root@localhost ~]#
<br>其中:root :当前登录用户
<br>localhost 主机名
<br>~当前所在目录(家目录)
<br>#超级用户的提示符
<br>普通用户的提示符是$
<br><br>3.复制命令:cp[选项] [原文件或目录] [目标目录]
<br>命令英文原意: copy
<br>选项:
<br>-r 复制目录
<br>-p 连带文件属性复制
<br>-d 若源文件是链接文件,则复制链接属性
<br>-a 相当于-pdr
<br><br>4.yum
<br>yum update 升级内核
<br>yum install curl安装
<br><br>5.systemctl
<br>systemctl start/stop docker 启动/关闭docker
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
<br><br>7.cd
<br>cd ..   返回上一级目录
<br>cd ../..   返回上两级目录
<br>cd或cd ~    返回home目录
<br>cd - 目录名  返回指定目录
<br><br>8.ps
<br>ps -ef|grep "hlcar-logic"
<br>ps [选项]
<br>-e 显示所有进程。
<br>-f 全格式。
<br>-h 不显示标题。长格式。
<br>-W 宽输出。
<br>a 显示终端_上的所有进程，包括其他用户的进程。
<br>r 只显示正在运行的进程。以用户为主的格式来显示程序状况。
<br>x 显示所有程序，不以终端机来区分。
<br><br>9.链接命令: ln
<br>ln -s [原文件] [目标文件]
<br>命令英文原意: link
<br>功能描述:生成链接文件
<br>选项:
<br>-s 创建软链接
<br><br>硬链接特征:
<br>1)拥有相同的1节点和存储block块,可以看做是同一一个文件
<br>2)可通过节点识别
<br>3)不能跨分区
<br>4)不能针对目录使用   
<br><br>软链接特征:
<br>1)类似Windows快捷方式
<br>2)软链接拥有自己的节点和Block块,但是数据块中只保存原
<br>文件的文件名和节点号,并没有实际的文件数据
<br>3)lrwxrwxrwx l 软链接软链接文件权限都为rwxrwxrwx
<br>4)修改任意文件，另一个都改变
<br>5)删除原文件,软链接不能使用
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
<br><br>1)基础
<br>-name<查询方式>按照指定的文件名查找模式查找文件
<br>-user<用户名>查找属于指定用户名所有文件
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
<br>--`find /etc -size +20k -a -size -50k -exec Is -h {}\`
<br>找到刪除.
<br>--`find /root - inum 262421 -exec rm -rf {} \`;
<br>避免大范围搜索,会非常耗费系统资源
<br>find是在系统当中搜索符合条件的文件名。如果需要匹配,
<br>使用通配符匹配,通配符是完全匹配
<br><br>2)Linux中的通配符
<br>*匹配任意内容
<br>?  匹配任意一个字符
<br>[]  匹配任意-个中括号内的字符
<br>[-]匹配中括号中任意一个字符，-代表一个范围。例如: [a-2]代表匹配一个小写字母。
<br>[^]逻辑非，表示匹配不是中括号内的一一个字符。例如:[^0-9]代表匹配一个不是数字的字符。
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
<br>-i 忽略大小写
<br>-v 排除指定字符串
<br>-n 显示匹配行及行号
<br>grep指令和管道符号
<br>grep过滤查找，管道符， "|"，表示将前一一个命令的处理结果输出传递给后面的命令处理。
<br>基本语法
<br>案例1:请在hello.txt文件中，查找"yes"所在行，不区分大小写，并且显示行号
<br>-- cat hello.txt | grep -ni yes
<br>grep -C 5 foo file 显示file文件里匹配foo字串那行以及上下5行
<br>grep -B 5 foo file 显示foo及前5行
<br>grep -A 5 foo file 显示foo及后5行
<br>find命令与grep命令的区别
<br>find命令:在系统当中搜索符合条件的文件名,如果需要匹配，使用通配符匹配,通配符是完全匹配
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
<br>--man -5 passwd
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
<br>-- whereis cd 确定是否是shell内部命令
<br>-- help cd 获取内部命令帮
<br><br>17.详细命令帮助info
<br>info命令
<br>回车:进入子帮助页面 (带有*号标记)
<br>-u: 进入上层页面
<br>-n: 进入下一个帮助小节
<br>-p: 进入上一个帮助小节
<br>-q: 退出
<br><br>18.压缩
<br>常用压缩格式: .zip.gz .bz2
<br>常用压缩格式: .tar.gz.tar.bz2
<br><br>1) .zip格式压缩
<br>zip压缩文件名 源文件
<br>#压缩文件
<br>zip -r 压缩文件名源目录
<br>#压缩目录
<br>unzip 压缩文件
<br>#解压缩.zip文件
<br><br>2) .gz格式压缩
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
<br><br>3) .bz2格式压缩
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
<br>-c: 打包
<br>-v: 显示过程
<br>-f: 指定打包后的文件名
<br>-- tar -cvf longzls.tar longzls
<br><br>解打包命令
<br>tar -xvf 打包文件名
<br>-x 解打包
<br>tar -xvf longzls.tar
<br>.tar.gz圧缩格式
<br>其实.tar.gz格式是先打包为.tar格式,再圧缩为.gz格式
<br>tar -zcvf **被圧缩包名.tar.gz**源文件
<br>迭项:
<br>-z: 圧缩为.tar.gz格式
<br>tar -zxvf **圧缩包名tar.gz**
<br>选项:
<br>-x：解圧缩.tar.gz格式
<br>.tar.bz2圧缩格式
<br>tar -jcvf 圧缩包名.tar.bz2源文件
<br>选项:
<br>-z: 圧缩为.tar.bz2格式
<br>tar -jxvf圧缩包名.tar.bz2
<br>选项:
<br>-x: 解圧缩.tar.bz2格式
<br><br>20. tail指令
<br>tail用于输出文件中尾部的内容，默认情况下tail指令显示文件的后10行内容。
<br>tail文件  (功能描述，查看文件后10行内容)
<br>tail -n5 文件  (功能描述，查看文件后5行内容，5可以是任意行数)
<br>tail -f 文件  (功能描述，实时追踪该文档的所有更新)应用实例
<br><br>21.查看与设定别名
<br>alias 查看系统中所有的命令别名
<br>alias别名= '原命令' 设定命令别名
<br>vi ~/.bashrc 写入坏境変量配置文件永久生效
<br>unalias別名 刪除別名
<br>source .bashrc 修改文件别名后执行这个生效，或者重新登录。。
<br><br>命令生效顺序
<br>第一顺位执行用绝对路径或相对路径执行的命令。第二顺位执行别名。
<br>第三顺位执行Bash的内部命令。
<br>第四顺位执行按照$PATH环境变量定义的目录查找顺序找到的第-一个命令
<br><br>22.history
<br>-c :清空万史命令
<br>-w :把緩存中的历史命令写入历史命令保存文件
<br><br>23.less
<br>是根据湿示需要加载内容,对于显示大型文件具有较高的效率.
<br>空格键或者pagedown 向下翻一页
<br>pageup 向上翻一页
<br>/字符串 向下查找 n下一个 N上一个
<br>?字符串 向上查找 n上一个 N下一个
<br>q 退出
23.<br><br>cat 査看文件
<br>空格键 向下翻页
<br>Enter 向下一行
<br>q 退出
<br>Crl+F 向下滚屏
<br>Ctrl+B 向上滚屏
<br><br>24.vi
<br>:n可以下翻文件  :N是上翻文件 ：prev也能切换到前一个文件
<br>:! 强制执行
<br>:ls  列出所有文件 
<br>:n  到下一个文件 
<br>:15  定位于第15行
<br>/xxx 往后搜索定位xxx 
<br>?xxx 往前搜索xxx
<br>拷贝当前行yy,拷贝当前行向下的5行5yy， 并粘贴。
<br>删除当前行dd,删除当前行向下的5行5dd
<br>设置文件的行号，取消文件的行号 命令行下: set nu和:set nonu
<br><br>vim
<br>查找与替换
<br>/字串   往游标之后寻找该字串。
<br>?字串   往游标之前寻找该字串。
<br>n    往下继续寻找下一个相同的字串。
<br>N    往上继续寻找下一个相同的字串。
<br>%   查找“(”，“)”，“{”，“}”的配对符。
<br>s   搜寻某行列范围。
<br>g   搜寻整个编辑缓冲区的资料。
<br>`:1,$s/old/new/g` 将文件中所有的『old』改成『new』

<br><br>25.useradd用户名应用案例
<br>passwd  用户名
<br>userdel  用户名
<br><br>![例子](https://github.com/gaoyuanyuan2/notes/blob/master/img/10.png) 
<br><br>
<br><br>26. 修改环境变量 --vim ~/.bash_profile  --source ~/.bash_profile
<br><br>27. 关闭防火墙
<br>当前关闭：service iptables stop
<br>永久关闭：chkconfig iptables off
<br>systemctl disable firewalld.service  开机禁用防火墙
<br>systemctl stop firewalld
<br>28. 查看端口 ss -tanl
<br><br>29. 编辑网卡的配置文件 --vim /etc/sysconfig/network-scripts/ifcfg-enp0s3
<br>首先需要将BOOTROTO由dhcp改为static，否则配置无效，dhcp表示使用动态IP；
<br>ONBOOT需要配置yes；
<br><br>30. 改主机名：--vi /etc/sysconfig/network
<br><br>31. kill -9 pid
<br>kill -9 pid等于kill -s 9 pid，表示强制，尽快终止一个进程。多半admin会用这个命令。
<br>killall命令用于杀死指定名字的进程（kill processes by name）之前使用ps等命令再配合grep来查找进程，而killall把这两个过程合二为一，是一个很好用的命令
<br>eg：killall mongod
### 2、硬件设备文件名
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
### 3、分区目录
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
<br>Boot 启动分区，home分区 /跟分区，swap虚拟内存
### 4、系统命令
1)shutdown命令
<br>shutdown [选项]时间
<br>选项:
<br>-c: 取消前一一个关机命令
<br>-h: 关机
<br>-r: 重启
<br><br>2)其他关机命令
<br>--halt
<br>--poweroff
<br>--init 0
<br><br>3)其他重启命令
<br>-- reboot
<br>-- init 6
<br><br>3)系统运行级别
<br>0 关机
<br>1 单用户
<br>2 不完全多用户,不含NFS服务
<br>3 完全多用户
<br>4 未分配
<br>5 图形界面
<br>6 重启
<br>runlevel查看运行级别前级别当前级别,
<br>logout退出当前用户，也就是注销，
### 5、常用快捷键
ctrl+c  强制终止当前命令
<br>ctrl+l 清屏
<br>ctrl+a 光标移动到命令行首
<br>ctrl+e 光标移动到命令行尾
<br>ctrl+u 从光标所在位置删除到行首
<br>ctrl+z 把命令放入后台
<br>ctrl+r 在历史命令中搜索













