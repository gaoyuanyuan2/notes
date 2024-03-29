# 常见问题

## docker-compose 启动报错 es73 exited with code 78

https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html#_set_vm_max_map_count_to_at_least_262144

max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]


我在这个问题上被困了几个月，解决方案是在 cmd.exe 上启动以下命令，如官方 Elasticsearch 文档中所述：

1) wsl -d docker-desktop
2) sysctl -w vm.max_map_count=262144

https://zhuanlan.zhihu.com/p/348813745


## docker desktop volumes

查看数据卷

cd \\wsl$\docker-desktop-data\version-pack-data\community\docker\volumes\

数据存放位置

C:\Users\Y\AppData\Local\Docker\wsl\data

https://stackoverflow.com/questions/43181654/locating-data-volumes-in-docker-desktop-windows


## Windows 10 WSL Ubuntu 系统的 root 密码

Ubuntu 的默认 root 密码是随机的，即每次开机都有一个新的 root 密码。
我们可以在终端输入命令 sudo passwd，然后输入当前用户的密码，终端会提示我们输入新的密码并确认，此时的密码就是 root 新密码。
修改成功后，输入命令 su root，再输入新的密码就 ok 了。


## 导入cvs

https://www.elastic.co/cn/blog/importing-csv-and-log-data-into-elasticsearch-with-file-data-visualizer


## 禁用交换编辑

大多数操作系统尝试将尽可能多的内存用于文件系统缓存，并急切地换出未使用的应用程序内存。这可能会导致部分 JVM 堆甚至其可执行页面被换出到磁盘。
交换对性能和节点稳定性非常不利，应该不惜一切代价避免

https://www.elastic.co/guide/en/elasticsearch/reference/7.x/setup-configuration-memory.html
