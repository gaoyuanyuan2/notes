# Shell

##  Shell是什么

Shell是一个命令行解释器,它为用户提供了一个向Linux内核发送请求以便运行程序的界面系统级程序,用户可以用Shell来启动、  挂起、停止甚至是编写一些程序。

Shell还是一个功能相当强大的编程语言,易编写,易调试，灵活性较强。Shell是解释执行的脚本语言,在Shell中可以直接调用Linux系统命令。

Shell的两种主要语法类型有Bourne和C ,这两种语法彼此不兼容。Bourne家族主要包括sh、ksh、Bash, psh、zsh ; C家族主要包括: csh、tcsh


## 脚本格式要求

* 脚本以#!/bin/bash开头

* 脚本需要有可执行权限

chmod 744 文件名

## 脚本的常用执行方式

* 方式1(输入脚本的绝对路径或相对路径)

1)首先要赋予helloworld.sh 脚本的+x权限

2)执行脚本

* 方式2(sh+脚本)

说明： 不用赋予脚本+x权限，直接执行即可。

## Shell的变量的介绍

* Linux Shell中的变量分为，系统变量和用户自定义变量。

* 系统变量： $HOME、 $PWD、 $SHELL、 $USER等等

比如： echo $HOME 等等.. 

* 显示当前shell中所有变量： set (set | more 分页显示)

## 变量

* 定义变量：变量=值

* 撤销变量： unset 变量

* 声明静态变量： readonly变量，注意：不能unset

```jshelllanguage
A=100
echo "A=$A"
unset A
echo "A=$A"
```
声明静态的变量B=2，不能unset
`readonly A=99`

可把变量提升为全局环境变量，可供其他shell程序使用


## 定义变量的规则

* 变量名称可以由字母、数字和下划线组成，但是不能以数字开头。

* 等号两侧不能有空格

* 变量名称一般习惯为大写

## 将命令的返回值赋给变量

* A=`ls -la` 反引号，运行里面的命令，并把结果返回给变量A

* A=$(ls -la) 等价于反引号

## 设置环境变量

* export 变量名=变量值 （功能描述：将shell变量输出为环境变量）

* source 配置文件 （功能描述：让修改后的配置信息立即生效）

为了让/etc/profile的环境变量生效，需要使用source /etc/profile重启系统或者注销用户

* echo $变量名 （功能描述：查询环境变量的值）
```jshelllanguage
#定义一个自己的环境变量
TOMCAT HOME=/opt/tomcat
export TOMCAT HOME

# 多行注释
:<<!
A=1
!
```

## 位置参数变量

当我们执行一个shell脚本时，如果希望获取到命令行的参数信息，就可以使用到位置参数变量

比如 ： ./myshell.sh 100 200 , 这个就是一个执行shell的命令行，可以在myshell 脚本中获取到参数信息

基本语法

* $n （功能描述： n为数字， $0代表命令本身， $1-$9代表第一到第九个参数，十以上的参数，十以上的参
数需要用大括号包含，如${10}）

* $* （功能描述：这个变量代表命令行中所有的参数， $*把所有的参数看成一个整体）

* $@（功能描述：这个变量也代表命令行中所有的参数， 不过$@把每个参数区分对待）

* $#（功能描述：这个变量代表命令行中所有参数的个数）

位置参数变量

## 预定义变量

就是shell设计者事先已经定义好的变量，可以直接在shell脚本中使用

* $$ （功能描述：当前进程的进程号（PID））

* $! （功能描述：后台运行的最后一个进程的进程号（PID））

* $？ （功能描述：最后一次执行的命令的返回状态。如果这个变量的值为0，证明上一个命令正
确执行；如果这个变量的值为非0（具体是哪个数，由命令自己来决定），则证明上一个命令执行不正
确了。）

在一个shell脚本中简单使用一下预定义变量
```jshelllanguage
#!/bin/bash
echo "当前的进程号=$$"
#后台的方式运行myShell.sh. 
./myShell.sh &
echo "最后的进程的号=$!"
echo "执行的值=$?"
```

## 运算符

* “$((运算式))”或“$[运算式]”

* expr m + n

`注意expr运算符间要有空格`

* expr m - n

* expr \*, /, % 乘，除，取余

```jshelllanguage
#求出两个参数的和
SUM=$ [$1+$2]
echo "SUM=$SUM"
```

## 条件判断

`[ condition ]（注意condition前后要有空格）`

`#非空返回true，可使用$?验证（0为true， >1为false）`

* 两个整数的比较

= 字符串比较

-lt 小于

-le 小于等于

-eq 等于

-gt 大于

-ge 大于等于

-ne 不等于


* 按照文件权限进行判断

-r 有读的权限

-w 有写的权限

-x 有执行的权限


* 按照文件类型进行判断

-f 文件存在并且是一个常规的文件

-e 文件存在

-d 文件存在并是一个目录


## 流程控制

### if 判断

if [ 条件判断式 ];then

程序

fi


或者

if [ 条件判断式 ]

then

程序

elif [条件判断式]

then

程序

fi

注意事项：

* [ 条件判断式 ]，中括号和条件判断式之间必须有空格 

* 推荐使用第二种方式


### case语句

case $变量名 in

"值1"）

如果变量的值等于值1，则执行程序1

;;

"值2"）

如果变量的值等于值2，则执行程序2

;;

…省略其他分支…

*）

如果变量的值都不是以上的值，则执行此程序

;;

esac

### for循环

* 基本语法1

for 变量 in 值1 值2 值3…

do

程序

* 基本语法2

for (( 初始值;循环控制条件;变量变化 ))

do

程序

done

### while循环

while [ 条件判断式 ]

do

程序

done

## read读取控制台输入

基本语法

read(选项)(参数)

选项：

-p：指定读取值时的提示符；

-t：指定读取值时等待的时间（秒） ，如果没有在指定的时间内输入，就不再等待了。。

参数

变量：指定读取值的变量名

## 函数

函数介绍

shell编程和其它编程语言一样，有系统函数，也可以自定义函数。系统函数中，

系统函数

• basename基本语法

功能：返回完整路径最后 / 的部分，常用于获取文件名

basename [pathname] [suffix]

basename [string] [suffix] （功能描述： basename命令会删掉所有的前缀包括最后一个（‘/’）

字符，然后将字符串显示出来。

选项：

suffix为后缀，如果suffix被指定了， basename会将pathname或string中的suffix去掉

• dirname基本语法

功能：返回完整路径最后 / 的前面的部分，常用于返回路径部分

dirname 文件绝对路径 （功能描述：从给定的包含绝对路径的文件名中去除文件名（非目录的部分），
然后返回剩下的路径（目录的部分））

自定义函数

• 基本语法

[ function ] funname[()]

{

Action;

[return int;]

} 

调用直接写函数名： funname [值]


```jshelllanguage
#!/bin/bash

#完成数据库的定时备份。
#备份的路径
BACKUP=/data/backup/db
#当前的时间作为文件名
DATETIME=$(date +%Y_%m_%d_%H%M%S)
#可以输出变量调试
#echo ${DATETIME}

echo "=======开始备份========"
echo "=======备份的路径是 $BACKUP/$DATETIME.tar.gz"

#主机
HOST=localhost
#用户名
DB_USER=root
#密码
DB_PWD=root
#备份数据库名
DATABASE=atguiguDB
#创建备份的路径
#如果备份的路径文件夹存在，就使用，否则就创建
[ ! -d "$BACKUP/$DATETIME" ] && mkdir -p "$BACKUP/$DATETIME"
#执行mysql的备份数据库的指令
mysqldump -u${DB_USER} -p${DB_PWD} --host=$HOST  $DATABASE | gzip > $BACKUP/$DATETIME/$DATETIME.sql.gz
#打包备份文件
cd $BACKUP
tar -zcvf $DATETIME.tar.gz $DATETIME
#删除临时目录
rm -rf $BACKUP/$DATETIME

#删除10天前的备份文件
find $BACKUP -mtime +10 -name "*.tar.gz" -exec rm -rf {} \;
echo "=====备份文件成功==========="

```






