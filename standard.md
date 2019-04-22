## 代码规范
### 

1、方法调用render(true)对于可怜的读者来说仍然摸不着头脑。卷动屏幕，看到render(Boolean isSuite), 稍许有点帮助，不过仍然不够。应该把该函数-分为二: reanderForSuite( )
和renderForSingleTest().
