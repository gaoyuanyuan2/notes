## Linux
### 常用命令
service network restart –重启网卡
<br>ip addr 查看ip
<br>uname –r 查看内核版本（3.1以上）
<br>yum update 升级内核
<br>yum install docker 安装docker
<br>systemctl start/stop docker 启动/关闭docker
<br>systemctl enable docker 开机启动
<br>systemctl disable docker 关闭开机启动
### docker命令
docker –v 查看版本
<br>docker search 
<br>docker pull
<br>运行  docker run --name container-name -d image name  --name :自定义容器名
  eg:docker run -name myredis -d redis  -d:后台运行
  image name:指定镜像模板
<br>列表  docker ps (查看运行中的容器) ;  加上a;可以查看所有容器停止  docker stop container-name/container-id  停止当前你运行的容器启动  docker start container-name/container id  启动容器
<br>删除  docker rm container-id  删除指定容器
<br>端口映射  -p 6379:6379  -p:主机端口(映射到)容器内部的端口
  eg:docker run -d -p 6379:6379 -name myredis docker.io/redis
<br>容器日志docker logs container name/container id






