## 并发编程
### 1、多线程
1.避免Random实例被多线程使用，虽然共享该实例是线程安全的，但会因竞争同一seed导致的性能下降。
<br><br>2. HashMap在容不够进行resize时由于高并发可能出现死链，导致CPU飙升,在开发过程中可以使用其它收据结构或加锁来规测此风险。
<br><br>3.Runnable可以避免Thread单继承特性带来的缺陷。更好实现内存共享。一个实例开启多个线程.
<br><br>4.终止线程：使用退出标志；使用stop方法（和suspend和resume一样是过期方法，可能产生不可预料的结果）（数据不一致）；
interrupt打断；建议使用“抛异常”的方法实现线程的停止。
<br><br>5.Interrupted（）：判断当前线程是否已经中断；线程的中断状态由该方法清除。
<br>IsInterrupted（）：测试线程Thread对象是否已经中断状态，但不清除状态标志。
<br><br>6.suspend和resume 缺点：独占，使得其他线程无法访问公共同步对象
<br><br>7.Yield方法：放弃当前CPU资源，放弃的时间不确定；高优先级的线程总是大部分先执行完。
<br><br>8.Wait/notify 实现线程通信。
<br>1)wait和notify必须配合synchronized关键字使用；
<br>2)Wait方法释放锁，notify方法不释放锁。
<br><br>9.同步不具备继承性
<br><br>10.锁非this对象有一定的优势：如果一个类有多个同步方法，同步（非this）代码块中的程序与同步方法是异步的，
不与其他锁this同步方法争抢this锁，可大大提高运行效率。
<br><br>11.Synchronized（非this对象X）：多个线程同时执行synchronized（x）{}同步代码块是呈同步效果；
其他线程执行x对象中synchronized同步方法呈同步效果。其他线程执行x对象里面的synchronized（this）代码块也呈同步效果。
<br><br>12.Class锁对所以对象实例起作用。对象锁和Class锁是异步的，因为是不同的锁
<br><br>13.下面将关键字synchronized和volatile进行一下比较:
<br>1)关键字volatile是线程同步的轻量级实现，所以volatile性能肯定比synchronized要好，
  并且volatile只能修饰于变量，而synchronized可以修饰方法，以及代码块。随着JDK新版本的发布，
  synchronized 关键字在执行效率上得到很大提升，在开发中使用synchronized关键字的比率还是比较大的。
<br>2)多线程访问volatile不会发生阻塞，而synchronized会出现阻塞。
<br>3) volatile 能保证数据的可见性，但不能保证原子性;  而synchronized可以保证原子性，
    也可以间接保证可见性，因为它会将私有内存和公共内存中的数据做同步。此知识点在后面有实验做论证。
<br>4)再次重申一下，关键字volatile解决的是变量在多个线程之间的可见性.
### 2、并发编程
<br><br> 1.BlockingQueue接口
<br>1)  ArrayBlockingQueue:基于数组的阻塞队列实现，在ArrayBlockingQueue内部， 维护了一个定长数组，
  以便缓存队列中的数据对象，其内部没实现读写分离，也就意味着生产和消费不能完全并行，
  长度是需要定义的，可以指定先进先出或者先进后出，也叫有界队列，在很多场合非常适合使用。
<br>2) LinkedBlockingQueue:基于链表的阻塞队列，同ArrayBlockingQueue类似， 
  其内部也维持着一个数据缓冲队列(该队列由一个链表构成)，LinkedBlockingQueue之所以能够高效的处理并发数据
  ，是因为其内部实现采用分离锁(读写分离两个锁)，从而实现生产者和消费者操作的完全并行运行。他是一个无界队列。
<br>3) SynchronousQueue:一种没有缓冲的队列，生产者产生的数据直接会被消费者获取并消费。
<br>4)   PriorityBlockingQueue:基于优先级的阻塞队列(优先级的判断通过构造函数传入
    的对象来决定，也就是说传入队列的对象必须实现Comparable接口)，
    在实现PriorityBlockingQueue时，内部控制线程同步的锁采用的是公平锁，他也是一一个无界的队列。
<br>5)  DelayQueue:带有延迟时间的Queue,其中的元素只有当其指定的延迟时间到了，
    才能够从队列中获取到该元素。DelayQueue中的元素必须实现Delayed接口，
    DelayQueue是一个没有大小限制的队列，应用场景很多，比如对缓存超时的数据进行移除、任务超时处理、空闲连接的关闭等等。
<br><br> 2. Executors创建线程池方法:
<br>1) newFixedThreadPool()方法，该方法返回一个固定数量的线程池，该方法的线程数始终不变，当有一一个任务提交时，
 若线程池中空闲，则立即执行，若没有，则会被暂缓在一个任务队列中等待有空闲的线程去执行。
<br>2) newSingle' ThreadExecutor()方法，创建-一个线程的线程池，若空闲则执行，若没有空闲线程则暂缓在任务列队中。
<br>3) newCachedThreadPool()方法，返回-一个可根据实际情况调整线程个数的线程池，不限制最大线程数量，若有任务，
   则创建线程，若无任务则不创建线程。如果没有任务则线程在60s后自动回收(空闲时间60s )。
<br>4)newScheduledThreadPool()方法，该方法返回一个SchededExecutorService对象，但该线程池可以指定线程的数量。
<br><br>16.自定义线程池
   <br>若Executors.工厂类无法满足我们的需求，可以自己去创建自定义的线程池，
   其实Executors工厂类里面的创建线程方法其内部实现均是用了ThreadPoolExecutor这个类，这个类可以自定义线程。
   构造方法如下:
```Java
public ThreadPoolExecutor(int corePoolSize,
     int maximumPoolSize,
     long keepAlive Time,
     TimeUnit unit,
     BlockingQueue<Runnable> workQueue,
     ThreadF actory threadFactory,
     RejectedExecutionHandler handler
 ){ ..}
 ```
   <br>这个构造方法对于队列是什么类型的比较关键:
   <br>1)在使用有界队列时，若有新的任务需要执行，如果线程池实际线程数小于corePoolSize,则优先创建线程，若大于corePoolSize, 
   则会将任务加入队烈，若队列已满，则在总线程数不天于maximumPoolSize的前提下，创建新的线程，若线程数大于maximumPoolSize
   ,则执行拒绝策略。或其他自定义方式。
   <br>2)无界的任务队列时:LinkedBlockingQueue. 与有界队列相比，除非系统资源耗尽，否则无界的在务队列不存在任务入队失败的情况。
   当有新任务到来，系统的线程数小于corePoolSize时，则新建线程执行任务。当达到
   corePoolSize后;就不会继续增加。若后续仍有新的在务加入，而有没有空闲的线程资源，则任务直接进入队列等待。若任务创建和处理的速度差异很大，
   无界队列会保持快速增长，直到耗尽系统内存。
   <br>3)JDK拒绝策略:
     <br>AbortPolicy:直接抛出异常组织系统正常工作
    <br> CallerRunsPolicy:只要线程池未关闭，该策略直接在调用者线程中，运行当前被丢弃的任务。
    <br> DiscardOldestPolicy:丢弃最老的一个请求，尝试再次提交当前任务。
    <br> DiscardPolicy:丢弃无法处理的任务，不给予任何处理。
   <br>如果需要自定义拒绝策略可以实现RejectedExecutionHandler接口。
<br><br>3.什么是自旋
<br>很多synchronized里面的代码只是一些很简单的代码，执行时间非常快，此时等待的线程都加锁可能是一种不太值得的操作，
因为线程阻塞涉及到用户态和内核态切换的问题。既然synchronized里面的代码执行地非常快，不妨让等待锁的线程不要被阻塞，
而是在synchronized的边界做忙循环，这就是自旋。如果做了多次忙循环发现还没有获得锁，再阻塞，这样可能是一种更好的策略。 
<br><br>4.什么是CAS
<br>CAS，全称为Compare and Set，即比较-设置。假设有三个操作数：内存值V、旧的预期值A、要修改的值B，
当且仅当预期值A和内存值V相同时，才会将内存值修改为B并返回true，否则什么都不做并返回false。当然CAS一定要volatile变量配合，
这样才能保证每次拿到的变量是主内存中最新的那个值，否则旧的预期值A对某条线程来说，永远是一个不会变的值A，只要某次CAS操作失败，
永远都不可能成功。
<br><br>5.什么是乐观锁和悲观锁
<br>1)乐观锁：对于并发间操作产生的线程安全问题持乐观状态，乐观锁认为竞争不总是会发生，
因此它不需要持有锁，将比较-设置这两个动作作为一个原子操作尝试去修改内存中的变量，如果失败则表示发生冲突，那么就应该有相应的重试逻辑。
<br>2)悲观锁：对于并发间操作产生的线程安全问题持悲观状态，悲观锁认为竞争总是会发生，因此每次对某资源进行操作时
，都会持有一个独占的锁，就像synchronized，不管三七二十一，直接上了锁就操作资源了。 
<br><br>6.什么是AQS
<br>简单说一下AQS，AQS全称为AbstractQueuedSychronizer，翻译过来应该是抽象队列同步器。
<br>如果说java.util.concurrent的基础是CAS的话，那么AQS就是整个Java并发包的核心了，ReentrantLock、CountDownLatch、Semaphore等等都用到了它。
AQS实际上以双向队列的形式连接所有的Entry，比方说ReentrantLock，所有等待的线程都被放在一个Entry中并连成双向队列，
前面一个线程使用ReentrantLock好了，则双向队列实际上的第一个Entry开始运行。
<br>AQS定义了对双向队列所有的操作，而只开放了tryLock和tryRelease方法给开发者使用，
开发者可以根据自己的实现重写tryLock和tryRelease方法，以实现自己的并发功能。

[并发编程Concurrent](http://www.importnew.com/26461.html)





        

        




