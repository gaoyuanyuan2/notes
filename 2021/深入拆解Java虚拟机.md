# 深入拆解Java虚拟机

## Java代码是怎么运行的？

Java 虚拟机将运行时内存区域划分为五个部分，分别为方法区、堆、PC 寄存器、Java 方法栈和本地方法栈。Java 程序编译而成的 class 文件，需要先加载至方法区中，方能在 Java 虚拟机中运行。

为了提高运行效率，标准 JDK 中的 HotSpot 虚拟机采用的是一种混合执行的策略。

它会解释执行 Java 字节码，然后会将其中反复执行的热点代码，以方法为单位进行即时编译，翻译成机器码后直接运行在底层硬件之上。

Java 则不同，它引进了八个基本类型，来支持数值计算。Java 这么做的原因主要是工程上的考虑，因为使用基本类型能够在执行效率以及内存使用两方面提升软件性能。

## Java的基本类型

NaN 有一个有趣的特性：除了“!=”始终返回 true 之外，所有其他比较结果都会返回 false。

举例来说，“NaN<1.0F”返回 false，而“NaN>=1.0F”同样返回 false。对于任意浮点数 f，不管它是 0 还是 NaN，“f!=NaN”始终会返回 true，而“f==NaN”始终会返回 false。

boolean、byte、char、short 这四种类型，在栈上占用的空间和 int 是一样的，和引用类型也是一样的。因此，在 32 位的 HotSpot 中，这些类型在栈上将占用 4 个字节；而在 64 位的 HotSpot 中，他们将占 8 个字节。

当然，这种情况仅存在于局部变量，而并不会出现在存储于堆中的字段或者数组元素上。对于 byte、char 以及 short 这三种类型的字段或者数组单元，它们在堆上占用的空间分别为一字节、两字节，以及两字节，也就是说，跟这些类型的值域相吻合。

## Java虚拟机是如何加载Java类的？

从 class 文件到内存中的类，按先后顺序需要经过加载、链接以及初始化三大步骤。

Java 语言的类型可以分为两大类：基本类型（primitive types）和引用类型（reference types）。

引用类型，Java 将其细分为四种：类、接口、数组类和泛型参数。由于泛型参数会在编译过程中被擦除，因此 Java 虚拟机实际上只有前三种。在类、接口和数组类中，数组类是由 Java 虚拟机直接生成的，其他两种则有对应的字节流。

### 加载

加载，是指查找字节流，并且据此创建类的过程。前面提到，对于数组类来说，它并没有对应的字节流，而是由 Java 虚拟机直接生成的。对于其他的类来说，Java 虚拟机则需要借助类加载器来完成查找字节流的过程。

启动类加载器（bootstrap class loader）。启动类加载器是由 C++ 实现的，没有对应的 Java 对象，因此在 Java 中只能用 null 来指代。


接到单子自己不能着手干，得先给师傅过过目。师傅不接手的情况下，才能自己来。在 Java 虚拟机中，这个潜规则有个特别的名字，叫双亲委派模型。每当一个类加载器接收到加载请求时，它会先将请求转发给父类加载器。在父类加载器没有找到所请求的类的情况下，该类加载器才会尝试去加载。

除了由 Java 核心类库提供的类加载器外，我们还可以加入自定义的类加载器，来实现特殊的加载方式。举例来说，我们可以对 class 文件进行加密，加载时再利用自定义的类加载器对其解密。

### 链接

链接，是指将创建成的类合并至 Java 虚拟机中，使之能够执行的过程。它可分为验证、准备以及解析三个阶段。


### 初始化

在 Java 代码中，如果要初始化一个静态字段，我们可以在声明时直接赋值，也可以在静态代码块中对其赋值。

如果直接赋值的静态字段被 final 所修饰，并且它的类型是基本类型或字符串时，那么该字段便会被 Java 编译器标记成常量值（ConstantValue），其初始化直接由 Java 虚拟机完成。除此之外的直接赋值操作，以及所有静态代码块中的代码，则会被 Java 编译器置于同一方法中，并把它命名为 < clinit >。

只有当初始化完成之后，类才正式成为可执行的状态。

### 那么，类的初始化何时会被触发呢？JVM 规范枚举了下述多种触发情况：
    
* 当虚拟机启动时，初始化用户指定的主类；
* 当遇到用以新建目标类实例的 new 指令时，初始化 new 指令的目标类；
* 当遇到调用静态方法的指令时，初始化该静态方法所在的类；
* 当遇到访问静态字段的指令时，初始化该静态字段所在的类；
* 子类的初始化会触发父类的初始化；
* 如果一个接口定义了 default 方法，那么直接实现或者间接实现该接口的类的初始化，会触发该接口的初始化；
* 使用反射 API 对某个类进行反射调用时，初始化这个类；
* 当初次调用 MethodHandle 实例时，初始化该 MethodHandle 指向的方法所在的类。

### 小结

加载是指查找字节流，并且据此创建类的过程。加载需要借助类加载器，在 Java 虚拟机中，类加载器使用了双亲委派模型，即接收到加载请求时，会先将请求转发给父类加载器。

链接，是指将创建成的类合并至 Java 虚拟机中，使之能够执行的过程。链接还分验证、准备和解析三个阶段。其中，解析阶段为非必须的。

初始化，则是为标记为常量值的字段赋值，以及执行 < clinit > 方法的过程。类的初始化仅会被执行一次，这个特性被用来实现单例的延迟初始化。

## JVM是如何执行方法调用的？

## JVM是如何处理异常的？

异常实例的构造十分昂贵。这是由于在构造异常实例时，Java 虚拟机便需要生成该异常的栈轨迹（stack trace）。该操作会逐一访问当前线程的 Java 栈帧，并且记录下各种调试信息，包括栈帧所指向方法的名字，方法所在的类名、文件名，以及在代码中的第几行触发该异常。

Java 字节码中，每个方法对应一个异常表。当程序触发异常时，Java 虚拟机将查找异常表，并依此决定需要将控制流转移至哪个异常处理器之中。Java 代码中的 catch 代码块和 finally 代码块都会生成异常表条目。

## JVM是如何实现反射的？

动态实现和本地实现相比，其运行效率要快上 20 倍 。这是因为动态实现无需经过 Java 到 C++ 再到 Java 的切换，但由于生成字节码十分耗时，仅调用一次的话，反而是本地实现要快上 3 到 4 倍。


* 第一，由于 Method.invoke 是一个变长参数方法，在字节码层面它的最后一个参数会是 Object 数组。Java 编译器会在方法调用处生成一个长度为传入参数数量的 Object 数组，并将传入参数一一存储进该数组中。

* 第二，由于 Object 数组不能存储基本类型，Java 编译器会对传入的基本类型参数进行自动装箱。

这两个操作除了带来性能开销外，还可能占用堆内存，使得 GC 更加频繁。

在默认情况下，方法的反射调用为委派实现，委派给本地实现来进行方法调用。在调用超过 15 次之后，委派实现便会将委派对象切换至动态实现。这个动态实现的字节码是自动生成的，它将直接使用 invoke 指令来调用目标方法。

方法的反射调用会带来不少性能开销，原因主要有三个：变长参数方法导致的 Object 数组，基本类型的自动装箱、拆箱，还有最重要的方法内联。


通常来说，使用反射 API 的第一步便是获取 Class 对象。在 Java 中常见的有这么三种。

* 使用静态方法 Class.forName 来获取。
* 调用对象的 getClass() 方法。
* 直接用类名 +“.class”访问。对于基本类型来说，它们的包装类型（wrapper classes）拥有一个名为“TYPE”的 final 静态字段，指向该基本类型对应的 Class 对象。

一旦得到了 Class 对象，我们便可以正式地使用反射功能了。下面我列举了较为常用的几项。

* 使用 newInstance() 来生成一个该类的实例。它要求该类中拥有一个无参数的构造器。
* 使用 isInstance(Object) 来判断一个对象是否该类的实例，语法上等同于 instanceof 关键字（JIT 优化时会有差别，我会在本专栏的第二部分详细介绍）。
* 使用 Array.newInstance(Class,int) 来构造该类型的数组。
* 使用 getFields()/getConstructors()/getMethods() 来访问该类的成员。除了这三个之外，Class 类还提供了许多其他方法，详见 [4]。需要注意的是，方法名中带 Declared 的不会返回父类的成员，但是会返回私有成员；而不带 Declared 的则相反。

当获得了类成员之后，我们可以进一步做如下操作。

* 使用 Constructor/Field/Method.setAccessible(true) 来绕开 Java 语言的访问限制。
* 使用 Constructor.newInstance(Object[]) 来生成该类的实例。
* 使用 Field.get/set(Object) 来访问字段的值。
* 使用 Method.invoke(Object, Object[]) 来调用方法。


## Java对象的内存布局

在 64 位的 Java 虚拟机中，对象头的标记字段占 64 位，而类型指针又占了 64 位。也就是说，每一个 Java 对象在内存中的额外开销就是 16 个字节。以 Integer 类为例，它仅有一个 int 类型的私有字段，占 4 个字节。因此，每一个 Integer 对象的额外内存开销至少是 400%。这也是为什么 Java 要引入基本类型的原因之一。

常见的 new 语句会被编译为 new 指令，以及对构造器的调用。每个类的构造器皆会直接或者间接调用父类的构造器，并且在同一个实例中初始化相应的字段。

Java 虚拟机引入了压缩指针的概念，将原本的 64 位指针压缩成 32 位。压缩指针要求 Java 虚拟机堆中对象的起始地址要对齐至 8 的倍数。Java 虚拟机还会对每个类的字段进行重排列，使得字段也能够内存对齐。

## 垃圾回收

目前 Java 虚拟机的主流垃圾回收器采取的是可达性分析算法。这个算法的实质在于将一系列 GC Roots 作为初始的存活对象合集（live set），然后从该合集出发，探索所有能够被该集合引用到的对象，并将其加入到该集合中，这个过程我们也称之为标记（mark）。最终，未被探索到的对象便是死亡的，是可以回收的。

一般而言，GC Roots 包括（但不限于）如下几种：

* Java 方法栈桢中的局部变量；
* 已加载类的静态变量；
* JNI handles；
* 已启动且未停止的 Java 线程。

漏报则比较麻烦，因为垃圾回收器可能回收事实上仍被引用的对象内存。一旦从原引用访问已经被回收了的对象，则很有可能会直接导致 Java 虚拟机崩溃。

Stop-the-world 以及安全点

### 小结

* Java 虚拟机中的垃圾回收器采用可达性分析来探索所有存活的对象。它从一系列 GC Roots 出发，边标记边探索所有被引用的对象。

* 为了防止在标记过程中堆栈的状态发生改变，Java 虚拟机采取安全点机制来实现 Stop-the-world 操作，暂停其他非垃圾回收线程。

* 回收死亡对象的内存共有三种方式，分别为：会造成内存碎片的清除、性能开销较大的压缩、以及堆使用效率较低的复制。

Java 虚拟机会记录 Survivor 区中的对象一共被来回复制了几次。如果一个对象被复制的次数为 15（对应虚拟机参数 -XX:+MaxTenuringThreshold），那么该对象将被晋升（promote）至老年代。另外，如果单个 Survivor 区已经被占用了 50%（对应虚拟机参数 -XX:TargetSurvivorRatio），那么较高复制次数的对象也会被晋升至老年代。

Java 虚拟机将堆分为新生代和老年代，并且对不同代采用不同的垃圾回收算法。其中，新生代分为 Eden 区和两个大小一致的 Survivor 区，并且其中一个 Survivor 区是空的。

在只针对新生代的 Minor GC 中，Eden 区和非空 Survivor 区的存活对象会被复制到空的 Survivor 区中，当 Survivor 区中的存活对象复制次数超过一定数值时，它将被晋升至老年代。

因为 Minor GC 只针对新生代进行垃圾回收，所以在枚举 GC Roots 的时候，它需要考虑从老年代到新生代的引用。为了避免扫描整个老年代，Java 虚拟机引入了名为卡表的技术，大致地标出可能存在老年代到新生代引用的内存区域。

## Java 虚拟机中的垃圾回收器

针对新生代的垃圾回收器共有三个：Serial，Parallel Scavenge 和 Parallel New。这三个采用的都是标记 - 复制算法。其中，Serial 是一个单线程的，Parallel New 可以看成 Serial 的多线程版本。Parallel Scavenge 和 Parallel New 类似，但更加注重吞吐率。此外，Parallel Scavenge 不能与 CMS 一起使用。

针对老年代的垃圾回收器也有三个：刚刚提到的 Serial Old 和 Parallel Old，以及 CMS。Serial Old 和 Parallel Old 都是标记 - 压缩算法。同样，前者是单线程的，而后者可以看成前者的多线程版本。

CMS 采用的是标记 - 清除算法，并且是并发的。除了少数几个操作需要 Stop-the-world 之外，它可以在应用程序运行过程中进行垃圾回收。在并发收集失败的情况下，Java 虚拟机会使用其他两个压缩型垃圾回收器进行一次垃圾回收。由于 G1 的出现，CMS 在 Java 9 中已被废弃 [3]。

G1（Garbage First）是一个横跨新生代和老年代的垃圾回收器。实际上，它已经打乱了前面所说的堆结构，直接将堆分成极其多个区域。每个区域都可以充当 Eden 区、Survivor 区或者老年代中的一个。它采用的是标记 - 压缩算法，而且和 CMS 一样都能够在应用程序运行过程中并发地进行垃圾回收。

G1 能够针对每个细分的区域来进行垃圾回收。在选择进行垃圾回收的区域时，它会优先回收死亡对象较多的区域。这也是 G1 名字的由来。

## Java内存模型

除了线程内的 happens-before 关系之外，Java 内存模型还定义了下述线程间的 happens-before 关系。

* 解锁操作 happens-before 之后（这里指时钟顺序先后）对同一把锁的加锁操作。
* volatile 字段的写操作 happens-before 之后（这里指时钟顺序先后）对同一字段的读操作。
* 线程的启动操作（即 Thread.starts()） happens-before 该线程的第一个操作。
* 线程的最后一个操作 happens-before 它的终止事件（即其他线程通过 Thread.isAlive() 或 Thread.join() 判断该线程是否中止）。
* 线程对其他线程的中断操作 happens-before 被中断线程所收到的中断事件（即被中断线程的 InterruptedException 异常，或者第三个线程针对被中断线程的 Thread.interrupted 或者 Thread.isInterrupted 调用）。
* 构造器中的最后一个操作 happens-before 析构器的第一个操作。

Java 内存模型是通过内存屏障（memory barrier）来禁止重排序的。

在 X86_64 平台上，只有 volatile 字段的写操作会强制刷新缓存。因此，理想情况下对 volatile 字段的使用应当多读少写，并且应当只有一个线程进行写操作。

## Java虚拟机是怎么实现synchronized的？

Java 线程的阻塞相当于熄火停车，而自旋状态相当于怠速停车。如果红灯的等待时间非常长，那么熄火停车相对省油一些；如果红灯的等待时间非常短，比如说我们在 synchronized 代码块里只做了一个整型加法，那么在短时间内锁肯定会被释放出来，因此怠速停车更加合适。

这就好比你在私家庄园里装了个红绿灯，并且庄园里只有你在开车。偏向锁的做法便是在红绿灯处识别来车的车牌号。如果匹配到你的车牌号，那么直接亮绿灯。

### 总结与实践

Java 虚拟机中 synchronized 关键字的实现，按照代价由高至低可分为重量级锁、轻量级锁和偏向锁三种。

重量级锁会阻塞、唤醒请求加锁的线程。它针对的是多个线程同时竞争同一把锁的情况。Java 虚拟机采取了自适应自旋，来避免线程在面对非常小的 synchronized 代码块时，仍会被阻塞、唤醒的情况。

轻量级锁采用 CAS 操作，将锁对象的标记字段替换为一个指针，指向当前线程栈上的一块空间，存储着锁对象原本的标记字段。它针对的是多个线程在不同时间段申请同一把锁的情况。

偏向锁只会在第一次请求时采用 CAS 操作，在锁对象的标记字段中记录下当前线程的地址。在之后的运行过程中，持有该偏向锁的线程的加锁操作将直接返回。它针对的是锁仅会被同一线程持有的情况。