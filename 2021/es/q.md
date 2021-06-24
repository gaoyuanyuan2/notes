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

https://stackoverflow.com/questions/43181654/locating-data-volumes-in-docker-desktop-windows