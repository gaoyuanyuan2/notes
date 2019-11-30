# 基础

##  常见的字符集:

* ASCII

美国人编码,使用7位来对美国常用的字符进行编码-包含128个字符

* ISO-8859-1

欧洲的编码,使用8位一包含256个字符

* GB2312
* GBK

国标码,中国的编码
      
* Unicode

万国码,包含世界上所有的语言和符号,编写程序时般都会使用Unicode编码Uni 、code编码有多种实现, UTF-8 UTF-16 UTF-32 最常用的就是UTF-8

## 编译型语言和解释型语言

* 编译型语言  C语言

编译型语言,会在代码执行前将代码编译为机器码,然后将机器码交由计算机执行

Java试图走一条中间路线。Java应用会被编译。但不是编译成特定CPU所专用的二进制代码，而是被编译成一种理想化的汇编语言。然后该汇编语言(称为Java字节码)可以用java运行(与php解释运行PHP脚本是相同的道理)
。这使得Java成为一门平台独立的解释型语言。因为java程序运行的是理想化的进制代码，所以它能在代码执行时将其编译成平台特定的二进制代码。由于这个编译是在程序执行时进行的，因此被称为“即时编译”(即JIT)。

### 小结

1.Java的设计结合了脚本语言的平台独立性和编译型语言的本地性能。

2.Java文件被编译成中间语言(Java字节码),然后在运行时被JVM进一步编译成汇编语言。

3.字节码编译成汇编语言的过程中有大量的优化，极大地改善了性能。


两种编译器的最主要的差别在于编译代码的时机不同。client编译器开启编译比server编译器要早。意味着在代码执行的开始阶段，client编译器比server编译器要快，因为它的编译代码相比server编译器而言要多。

此处工程.上考虑的权衡是，server 编译器等待编译的时候是否还能做更有价值的事: server编译器在编译代码时可以更好地进行优化。

最终，server编译器生成的代码要比client编译器快。从用户角度看，权衡的取舍在于程序要运行多久，程序的启动时间有多重要。

### 小结

1.如果应用的启动时间是首要的性能考量，那client编译器就是最有用的。

2.分层编译的启动时间可以非常接近于client编译器所获得的启动时间。


*  解释型语言 Python JS Java

边执行一边编译


## 基本类型

byte/8

char/16

short/16

int/32

float/32

long/64

double/64

boolean/~

boolean 只有两个值：true、false，可以使用 1 bit 来存储，但是具体大小没有明确规定。JVM 会在编译时期将 boolean 类型的数据转换为 int，使用 1 来表示 true，0 表示 false。JVM 支持 boolean 数组，但是是通过读写 byte 数组来实现的。


## String

在 Java 7 之前，String Pool 被放在运行时常量池中，它属于永久代。而在 Java 7，
String Pool 被移到堆中。这是因为永久代的空间有限，在大量使用字符串的场景下会导致 OutOfMemoryError 错误。

## Object 通用方法

概览

public native int hashCode()

public boolean equals(Object obj)

protected native Object clone() throws CloneNotSupportedException

public String toString()

public final native Class<?> getClass()

protected void finalize() throws Throwable {}

public final native void notify()

public final native void notifyAll()

public final native void wait(long timeout) throws InterruptedException

public final void wait(long timeout, int nanos) throws InterruptedException

public final void wait() throws InterruptedException

1. cloneable

clone() 是 Object 的 protected 方法，它不是 public，一个类不显式去重写 clone()，其它类就不能直接去调用该类实例的 clone() 方法。

使用 clone() 方法来拷贝一个对象即复杂又有风险，它会抛出异常，并且还需要类型转换。Effective Java 书上讲到，
最好不要去使用 clone()，可以使用拷贝构造函数或者拷贝工厂来拷贝一个对象。

## 锁

1. 锁的实现

synchronized 是 JVM 实现的，而 ReentrantLock 是 JDK 实现的。

2. 性能

新版本 Java 对 synchronized 进行了很多优化，例如自旋锁等，synchronized 与 ReentrantLock 大致相同。

3. 等待可中断

当持有锁的线程长期不释放锁的时候，正在等待的线程可以选择放弃等待，改为处理其他事情。

ReentrantLock 可中断，而 synchronized 不行。

4. 公平锁

公平锁是指多个线程在等待同一个锁时，必须按照申请锁的时间顺序来依次获得锁。

synchronized 中的锁是非公平的，ReentrantLock 默认情况下也是非公平的，但是也可以是公平的。

5. 锁绑定多个条件

一个 ReentrantLock 可以同时绑定多个 Condition 对象。

## wait

wait() 和 sleep() 的区别

wait() 是 Object 的方法，而 sleep() 是 Thread 的静态方法；

wait() 会释放锁，sleep() 不会。

## BlockingQueue

java.util.concurrent.BlockingQueue 接口有以下阻塞队列的实现：

* FIFO 队列 ：LinkedBlockingQueue、ArrayBlockingQueue（固定长度）

* 优先级队列 ：PriorityBlockingQueue

提供了阻塞的 take() 和 put() 方法：如果队列为空 take() 将阻塞，直到队列中有内容；如果队列为满 put() 将阻塞，直到队列有空闲位置。

使用 BlockingQueue 实现生产者消费者问题

## ThreadLocal 

从理论上讲并不是用来解决多线程并发问题的，因为根本不存在多线程竞争。
   

 在一些场景 (尤其是使用线程池) 下，由于 ThreadLocal.ThreadLocalMap 的底层数据结构导致 ThreadLocal 有内存泄漏的情况，应该尽可能在每次使用 ThreadLocal 后手动调用 remove
 ()，以避免出现 ThreadLocal 经典的内存泄漏甚至是造成自身业务混乱的风险。
 
## 自旋锁

自旋锁虽然能避免进入阻塞状态从而减少开销，但是它需要进行忙循环操作占用 CPU 时间，它只适用于共享数据的锁定状态很短的场景。

