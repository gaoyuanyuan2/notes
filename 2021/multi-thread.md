# 多线程复习

## 停止线程

* stop(); 过期。

* nterrupt(); 不会终止一个正在运行的线程。

* 使用退出标志，使线程正常退出。

* 异常法

* return
 

interrupted()
测试当前线程是否已被中断。此方法清除线程的中断状态。换句话说,如果连续两次调用此方法，则第二次调用将返回false。

interrupt()是给线程设置中断标志；interrupted()是检测中断并清除中断状态；
isInterrupted()只检测中断，不清除状态。

容易死锁
suspend() 暂停
resume() 恢复

yield() 放弃当前CPU资源


## 线程优先级

setPriority()
高优先级的线程`大部分`先执行完。

## 同步 synchronized

同步不具有继承性

修饰方法，代码块

## volatile

只能修饰变量

共享内存中读取

## ReentrantLock

lock();
unlock();
ifFair();是否公平锁

## Condition

await();
signal();
signalAll();

## ReentrantReadWriteLock

读读共享

写写互斥

读写互斥

## Timer

## 单例

双重检查锁

