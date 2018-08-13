## Linux
### 1、命令
1.常用命令
<br><br>service network restart –重启网卡
<br><br>ip addr 查看ip ifconfig -a 
<br><br>uname –r 查看内核版本（3.1以上）
<br><br>yum update 升级内核
<br><br>yum install docker 安装docker
<br><br>systemctl start/stop docker 启动/关闭docker
<br><br>systemctl enable docker 开机启动
<br><br>systemctl disable docker 关闭开机启动
<br><br>yum install curl安装
<br><br>cd ..   返回上一级目录
<br>cd ../..   返回上两级目录
<br>cd或cd ~    返回home目录
<br>cd - 目录名  返回指定目录

<br><br> ps -ef|grep "hlcar-logic"
<br>ps [选项]
<br>-e
显示所有进程。
<br>-f
全格式。
<br>-h
不显示标题。
长格式。
<br>-W
宽输出。
<br>a
显示终端_上的所有进程，包括其他用户的进程。
<br>r
只显示正在运行的进程。
以用户为主的格式来显示程序状况。
<br>X
显示所有程序，不以终端机来区分。

<br><br>curl  http://localhost:8080

<br><br>Ctrl+l ：清屏

<br><br>tail -f logic.out动态更新

<br><br>service network restart  
<br><br>date查看系统日期

<br><br>2.压缩


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






