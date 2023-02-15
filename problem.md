# 常见问题总结

## maven 版本问题

`java.lang.NoSuchMethodError` maven版本导入错误。仓库里面版本更新，本地引入还是之前版本。删除版本版本。


## 系统问题看不到日志

OOM系统挂了，k8s会自动重启系统

## 长文本存储

如果存储很多长的文本数据，不建议使用mysql，可以考虑使用nosql数据库；如果同时还需要经常进行文本的检索，可以使用搜索引擎技术，比如elasticsearch。
