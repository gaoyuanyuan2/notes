## 模式

*设计模式*

*架构模式*

*分析模式创建型模式*

*结构型模式*

*行为型模式*


## 会话管理

在客户端保存会话状态有以下优点:

相对来说容易实现。

当要保存的状态比较少时，效果很好。

而且，当需要在多台物理服务器上实现负载均衡时，使用在客户端保存会话状态的策略,也不需要在服务器之间复制会话状态。

为了在客户端保存会话状态，有两种常见策略一HTML隐 藏字段，和HTTP cookie