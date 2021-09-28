# Tomcat

## http

1. Cookie 技术

Cookie 是 HTTP 报文的一个请求头，Web 应用可以将用户的标识信息或者其他一些信息（用户名等）存储在 Cookie 中。用户经过验证之后，每次 HTTP 请求报文中都包含 Cookie，这样服务器读取这个 Cookie 请求头就知道用户是谁了。Cookie 本质上就是一份存储在用户本地的文件，里面包含了每次请求中都需要传递的信息。

2. Session 技术

由于 Cookie 以明文的方式存储在本地，而 Cookie 中往往带有用户信息，这样就造成了非常大的安全隐患。而 Session 的出现解决了这个问题，Session 可以理解为服务器端开辟的存储空间，里面保存了用户的状态，用户信息以 Session 的形式存储在服务端。当用户请求到来时，服务端可以把用户的请求和用户的 Session 对应起来。那么 Session 是怎么和请求对应起来的呢？答案是通过 Cookie，浏览器在 Cookie 中填充了一个 Session ID 之类的字段用来标识请求。

 HTTP/1.1 中，引入了 HTTP 长连接的概念，使用长连接的 HTTP 协议，会在响应头加入 Connection:keep-alive。这样当浏览器完成一次请求后，浏览器和服务器之间的 TCP 连接不会关闭，再次访问这个服务器上的网页时，浏览器会继续使用这一条已经建立的连接，也就是说两个请求可能共用一个 TCP 连接。
 
 ## Servlet规范和Servlet容器
 
 Servlet 容器用来加载和管理业务类。HTTP 服务器不直接跟业务类打交道，而是把请求交给 Servlet 容器去处理，Servlet 容器会将请求转发到具体的 Servlet，如果这个 Servlet 还没创建，就加载并实例化这个 Servlet，然后调用这个 Servlet 的接口方法。因此 Servlet 接口其实是Servlet 容器跟具体业务类之间的接口。
 
 而 Servlet 接口和 Servlet 容器这一整套规范叫作 Servlet 规范。Tomcat 和 Jetty 都按照 Servlet 规范的要求实现了 Servlet 容器，同时它们也具有 HTTP 服务器的功能。作为 Java 程序员，如果我们要实现新的业务功能，只需要实现一个 Servlet，并把它注册到 Tomcat（Servlet 容器）中，剩下的事情就由 Tomcat 帮我们处理了。
 
 规范就是说大家都要遵守，就会千篇一律，但是如果这个规范不能满足你的业务的个性化需求，就有问题了，因此设计一个规范或者一个中间件，要充分考虑到可扩展性。Servlet 规范提供了两种扩展机制：Filter和Listener。
 
  Spring 就实现了自己的监听器，来监听 ServletContext 的启动事件，目的是当 Servlet 容器启动时，创建并初始化全局的 Spring 容器。
  
  
Servlet一般会延迟加载，当第一个请求达到时，Tomcat&Jetty发现DispatcherServlet还没有被实例化，就调用DispatcherServlet的init方法，DispatcherServlet在初始化的时候会建立自己的容器，叫做SpringMVC 容器，用来持有Spring MVC相关的Bean。同时，Spring MVC还会通过ServletContext拿到Spring根容器，并将Spring根容器设为SpringMVC容器的父容器，请注意，Spring MVC容器可以访问父容器中的Bean，但是父容器不能访问子容器的Bean， 也就是说Spring根容器不能访问SpringMVC容器里的Bean。说的通俗点就是，在Controller里可以访问Service对象，但是在Service里不可以访问Controller对象。

## 线程池

池化的目的是为了避免频繁地创建和销毁对象，减少对系统资源的消耗。Java 提供了默认的线程池实现，我们也可以扩展 Java 原生的线程池来实现定制自己的线程池，Tomcat 就是这么做的。Tomcat 扩展了 Java 线程池的核心类 ThreadPoolExecutor，并重写了它的 execute 方法，定制了自己的任务处理流程。同时 Tomcat 还实现了定制版的任务队列，重写了 offer 方法，使得在任务队列长度无限制的情况下，线程池仍然有机会创建新的线程。

## GC原理及调优的基本思路

## G1 收集器

G1 将堆拆分成小的区域，一个最大的好处是可以做局部区域的垃圾回收，而不需要每次都回收整个区域比如年轻代和年老代，这样回收的停顿时间会比较短。具体的收集过程是：

将所有存活的对象将从收集的区域复制到未分配的区域，比如收集的区域是 Eden 空间，把 Eden 中的存活对象复制到未分配区域，这个未分配区域就成了 Survivor 空间。理想情况下，如果一个区域全是垃圾（意味着一个存活的对象都没有），则可以直接将该区域声明为“未分配”。
为了优化收集时间，G1 总是优先选择垃圾最多的区域，从而最大限度地减少后续分配和释放堆空间所需的工作量。这也是 G1 收集器名字的由来——Garbage-First。


对于 G1 收集器来说，我不推荐直接设置年轻代的大小，这一点跟 CMS 收集器不一样，这是因为 G1 收集器会根据算法动态决定年轻代和年老代的大小。因此对于 G1 收集器，我们需要关心的是 Java 堆的总大小（-Xmx）。

此外 G1 还有一个较关键的参数是-XX:MaxGCPauseMillis = n，这个参数是用来限制最大的 GC 暂停时间，目的是尽量不影响请求处理的响应时间。G1 将根据先前收集的信息以及检测到的垃圾量，估计它可以立即收集的最大区域数量，从而尽量保证 GC 时间不会超出这个限制。因此 G1 相对来说更加“智能”，使用起来更加简单。


### CMS 收集器

对于 CMS 收集器来说，最重要的是合理地设置年轻代和年老代的大小。年轻代太小的话，会导致频繁的 Minor GC，并且很有可能存活期短的对象也不能被回收，GC 的效率就不高。而年老代太小的话，容纳不下从年轻代过来的新对象，会频繁触发单线程 Full GC，导致较长时间的 GC 暂停，影响 Web 应用的响应时间。

### 小结

对于 CMS 来说，我们要合理设置年轻代和年老代的大小。你可能会问该如何确定它们的大小呢？这是一个迭代的过程，可以先采用 JVM 的默认值，然后通过压测分析 GC 日志。

如果我们看年轻代的内存使用率处在高位，导致频繁的 Minor GC，而频繁 GC 的效率又不高，说明对象没那么快能被回收，这时年轻代可以适当调大一点。

如果我们看年老代的内存使用率处在高位，导致频繁的 Full GC，这样分两种情况：如果每次 Full GC 后年老代的内存占用率没有下来，可以怀疑是内存泄漏；如果 Full GC 后年老代的内存占用率下来了，说明不是内存泄漏，我们要考虑调大年老代。

对于 G1 收集器来说，我们可以适当调大 Java 堆，因为 G1 收集器采用了局部区域收集策略，单次垃圾收集的时间可控，可以管理较大的 Java 堆。


如果我们监控到 CPU 上升，这时我们可以看看吞吐量是不是也上升了，如果是那说明正常；如果不是的话，可以看看 GC 的活动，如果 GC 活动频繁，并且内存居高不下，基本可以断定是内存泄漏。

## IO和线程池的并发调优

maxThreads 的值，如果这个参数设置小了，Tomcat 会发生线程饥饿，并且请求的处理会在队列中排队等待，导致响应时间变长；如果 maxThreads 参数值过大，同样也会有问题，因为服务器的 CPU 的核数有限，线程数太多会导致线程在 CPU 上来回切换，耗费大量的切换开销。


### 线程池大小 = 每秒请求数 × 平均请求处理时间

这是理想的情况，也就是说线程一直在忙着干活，没有被阻塞在 I/O 等待上。实际上任务在执行中，线程不可避免会发生阻塞，比如阻塞在 I/O 等待上，等待数据库或者下游服务的数据返回，虽然通过非阻塞 I/O 模型可以减少线程的等待，但是数据在用户空间和内核空间拷贝过程中，线程还是阻塞的。线程一阻塞就会让出 CPU，线程闲置下来，就好像工作人员不可能 24 小时不间断地处理客户的请求，解决办法就是增加工作人员的数量，一个人去休息另一个人再顶上。对应到线程池就是增加线程数量，因此 I/O 密集型应用需要设置更多的线程。

### 线程池大小 = （线程 I/O 阻塞时间 + 线程 CPU 时间 ）/ 线程 CPU 时间

一般来说，如果系统的 TPS 要求足够大，用第一个公式算出来的线程数往往会比公式二算出来的要大。我建议选取这两个值中间更靠近公式二的值。也就是先设置一个较小的线程数，然后进行压测，当达到系统极限时（错误数增加，或者响应时间大幅增加），再逐步加大线程数，当增加到某个值，再增加线程数也无济于事，甚至 TPS 反而下降，那这个值可以认为是最佳线程数。

## Tomcat内存溢出的原因分析及调优

### 内存溢出场景及方案

#### java.lang.OutOfMemoryError: Java heap space

JVM 无法在堆中分配对象时，会抛出这个异常，导致这个异常的原因可能有三种：

1. 内存泄漏。Java 应用程序一直持有 Java 对象的引用，导致对象无法被 GC 回收，比如对象池和内存池中的对象无法被 GC 回收。
2. 配置问题。有可能是我们通过 JVM 参数指定的堆大小（或者未指定的默认大小），对于应用程序来说是不够的。解决办法是通过 JVM 参数加大堆的大小。
3.finalize 方法的过度使用。如果我们想在 Java 类实例被 GC 之前执行一些逻辑，比如清理对象持有的资源，可以在 Java 类中定义 finalize 方法，这样 JVM GC 不会立即回收这些对象实例，而是将对象实例添加到一个叫“java.lang.ref.Finalizer.ReferenceQueue”的队列中，执行对象的 finalize 方法，之后才会回收这些对象。Finalizer 线程会和主线程竞争 CPU 资源，但由于优先级低，所以处理速度跟不上主线程创建对象的速度，因此 ReferenceQueue 队列中的对象就越来越多，最终会抛出 OutOfMemoryError。解决办法是尽量不要给 Java 类定义 finalize 方法。

#### java.lang.OutOfMemoryError: GC overhead limit exceeded

出现这种 OutOfMemoryError 的原因是，垃圾收集器一直在运行，但是 GC 效率很低，比如 Java 进程花费超过 98％的 CPU 时间来进行一次 GC，但是回收的内存少于 2％的 JVM 堆，并且连续 5 次 GC 都是这种情况，就会抛出 OutOfMemoryError。

解决办法是查看 GC 日志或者生成 Heap Dump，确认一下是不是内存泄漏，如果不是内存泄漏可以考虑增加 Java 堆的大小。当然你还可以通过参数配置来告诉 JVM 无论如何也不要抛出这个异常，方法是配置-XX:-UseGCOverheadLimit，但是我并不推荐这么做，因为这只是延迟了 OutOfMemoryError 的出现。

#### java.lang.OutOfMemoryError: Requested array size exceeds VM limit

从错误消息我们也能猜到，抛出这种异常的原因是“请求的数组大小超过 JVM 限制”，应用程序尝试分配一个超大的数组。比如应用程序尝试分配 512MB 的数组，但最大堆大小为 256MB，则将抛出 OutOfMemoryError，并且请求的数组大小超过 VM 限制。

通常这也是一个配置问题（JVM 堆太小），或者是应用程序的一个 Bug，比如程序错误地计算了数组的大小，导致尝试创建一个大小为 1GB 的数组。

#### java.lang.OutOfMemoryError: MetaSpace

如果 JVM 的元空间用尽，则会抛出这个异常。我们知道 JVM 元空间的内存在本地内存中分配，但是它的大小受参数 MaxMetaSpaceSize 的限制。当元空间大小超过 MaxMetaSpaceSize 时，JVM 将抛出带有 MetaSpace 字样的 OutOfMemoryError。解决办法是加大 MaxMetaSpaceSize 参数的值。

#### java.lang.OutOfMemoryError: Request size bytes for reason. Out of swap space

当本地堆内存分配失败或者本地内存快要耗尽时，Java HotSpot VM 代码会抛出这个异常，VM 会触发“致命错误处理机制”，它会生成“致命错误”日志文件，其中包含崩溃时线程、进程和操作系统的有用信息。如果碰到此类型的 OutOfMemoryError，你需要根据 JVM 抛出的错误信息来进行诊断；或者使用操作系统提供的 DTrace 工具来跟踪系统调用，看看是什么样的程序代码在不断地分配本地内存。

#### java.lang.OutOfMemoryError: Unable to create native threads

抛出这个异常的过程大概是这样的：

1.Java 程序向 JVM 请求创建一个新的 Java 线程。
2.JVM 本地代码（Native Code）代理该请求，通过调用操作系统 API 去创建一个操作系统级别的线程 Native Thread。
3. 操作系统尝试创建一个新的 Native Thread，需要同时分配一些内存给该线程，每一个 Native Thread 都有一个线程栈，线程栈的大小由 JVM 参数-Xss决定。
4. 由于各种原因，操作系统创建新的线程可能会失败，下面会详细谈到。
5.JVM 抛出“java.lang.OutOfMemoryError: Unable to create new native thread”错误。

