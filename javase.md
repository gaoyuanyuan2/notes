## JAVASE

### 1、类型

1.10到其他进制的转化，除余法。

2.0正 1负，正数的补码和原码相同，负数的补码是反码基础上加1.

3.计算机操作的时候都是采用数据对应的二进制补码来计算的。

4.数据向上转型、强制转化：大到小、8位一个字节

 ![类型](https://github.com/gaoyuanyuan2/notes/blob/master/img/17.png) 

5.位异或运算 ^ ：相同则为0，不相同则为1

6.位非运算符~：如果位为0，结果是1，如果位为1，结果是0

7.补码原码

        符号位 数值位
补码:     1    0000010
反码:     1    0000001
原码:     1    1111110

8.移位

 <<:左移左边最高位丢弃，右边补齐0
 
 >>:右移最高位是0，左边补齐0;最高为是1，左边补齐1
 
 >>>:无符号右移无论最高位是0还是1，左边补齐0
 
9. switch 

 表达式的取值，bvte short int char。JDK5以后可以是枚举. JDK7以后可以是String
 
10.集合和泛型只能为引用类型

11.泛型

final： 如果你有Java性能调优方面的经验，你或许会觉得惊奇，因为整章关于编译的讨论中都没有提及final关键字。final 总被认为是影响性能的重要因素，因为大家相信在进行内联和其他优化时，final 
可以使JIT编译器作出更好的选择。

这种想法在落伍的过去或许有一些价值，但已经很多年很多年不是这样了(即便曾经:是)。而其实它是流传甚广的谣言。准确地说，只要有必要时，

你就应该使用final:比如你不打算改变的不可变对象或原生值、内部类引用的外部参数等等。但无论有没有final关键字，都不会影响应用的性能。


```Java
public static void printCollection(Collection<?> cols) {
    for(Object obj:cols) {
        System.outprintn(obj);
    }
    //cols. add( string");//错误，因为它不知自己未来匹配就一定是String
    cols.size();//没错，此方法与类型参数没有关系
    cols = new HashSet<Date>();
}
```

总结:使用?通配符可以引用其他各种参数化的类型, ?通配符定义的变量主要用作引用,可以调用与参数化无关的方法，不能调用与参数化有关的万法。

T限定通配符的上边界:

正确: Vector<? extends Number> x = new Vector<Integer>();

错误: Vector<? extends Number> x = new Vector<String>();

?限定通配符的下边界:

正确: Vector<super Integer> x = new Vector<Number>();

错误; Vector<? super Integer> x = new Vector<Byte>();

Java中的泛型类型(或者泛型)类似于C++中的模板。但是这种相似性仅限于表面，Java 语言中的泛型基本上完全是在编译器中实现，
用于编译器执行类型检查和类型推断，状后生成普通的非泛型的字节码，这种实现技术称为擦除(erasure) (编译器使用泛型类型信息保
证类型安全，然后在生成字节码之首将其清除)。这是因为扩展虚拟机指令集来支持泛型被认为是无法接受的。

### 2、对象

1.抽象的(abstract) 方法是否可同时是静态的(static) ,是否可同时是本地方法(native) ，是否可同时被synchronized修饰?

都不能。抽象方法需要子类重写，而静态的方法是无法被重写的，因此二者是矛盾的。

本地方法是由本地代码(如C代码)实现的方法，而抽象方法是没有实现的，也是矛盾的。

synchronized和方法的实现细节有关，抽象方法不涉及实现细节，因此也是相互矛盾的。

 2. 如何实现对象克隆?
 
  1)实现Cloneable接口并重写Object类中的clone方法;
  
  2)实现Serializable接口, 通过对象的序列化和反序列化实现克隆，可以实现真正的深度克隆。
  
3.工具类构造器私有化

4.创建对象的代价是非常昂贵的

5.重用对象会导致潜在错误和安全漏洞

6.防内存泄漏：一旦数组元素变成非活动部分的部分，就手动清空这些数组元素；缓存遗忘，定时清理（LinkedHashMap 类的removeEldestEntry方法，更复杂的用java.lang.ref）;客户端在API中注册回调，没有显示的取消注册。
  
7.终结方法：不建议使用。除非是安全网终止非关键本地资源，记住要调用super.finalize ，记录非法用法。与共有的非final类关联起来，考虑使用守卫者，确保执行（及时子类终结方法未调用super.finalize）

8.protected void   finalize()当垃圾回收器确定不存在对该对象的更多引用时，由对象的垃圾回收器调用此方法。

9.类加载的五个过程：加载、验证、准备、解析、初始化

10.定义 DO/DTO/VO 等 POJO 类时，不要设定任何属性默认值，必须写 toString 方法

11.使用索引访问用 String 的 split 方法得到的数组时，需做最后一个分隔符后有无内容的检查，否则会有抛 IndexOutOfBoundsException 的风险

12.Object方法

1)	equals 方法:值类需要覆盖equals方法(枚举类除外)

反自性、传递性、一致性

2)	高质量的equals：== （性能优化，如果是返回true），  instanceof 正确的类型 不是返回false，顺序

3)	覆写equals必须覆写hashCode，相等的对象必须有相等的散列码。

4)	始终要覆盖toString （自描述）

5)	Clone 从不覆写改方法，也不调用，除非拷贝数组。

6)	考虑实现comparable接口

7)	构造器不能被继承，因此不能被重写，但可以被重载

8)	抽象类中的成员可以是private、默认、protected、public的，而接口中的成员全都是public的。抽象类中可以定义成员变量，而接口中定义的成员变量实际上都是常量。

9)	抽象方法需要子类重写，而静态的方法是无法被重写的

10)	Clone equal toString hashCode wait notify notifyAll getClass

11)	hashcode那就会使效率提高很多，桶

13.通用程序设计

1)	精确计算不使用float 和double 使用BigDecimal。9位内使用int，18位内使用long

2)	如果其他类型更适合，尽量避免使用字符串。

3)	重复n个字符串连接，需要n的平方级时间。使用StringBuilder 的append方法。

4)	接口引用对象会使程序更加灵活。

5)	接口优于反射机制。

6)	再多底层优化无法弥补算法选择不当。

14. 数组

```java
    //动态初始化
    //int[] array = new int[3];
    //这样数组3个元素均为0;
    //静态初始化
    int[] array = new int[]{4, 2, 1};
    //不允许同时使用上述
    int[] array = new int[3](4, 2, 1};
```

### 3、集合框架体

![集合](https://github.com/gaoyuanyuan2/notes/blob/master/img/5.png) 

![空值](https://github.com/gaoyuanyuan2/notes/blob/master/img/6.png) 

1. 提供排序的比较器,业务比较器

实现java. util. Comparator接口，
重写public  int compare(T o1,  To2);

作用 

解耦:独立于实体类 

方便:便于应对各种排序规则

2. HashMap实现原理

拉链法

![](https://github.com/gaoyuanyuan2/notes/blob/master/img/20.png) 


数组+链表组成的，一个长度为16的数组中，每个元素存储的是一个链表的头结点。一般情况是通过hash(key)%len获得，也就是元素的key的哈希值对数组长度取模得到。

O（1）时间复杂度

HashMap底层就是一个数组结构，数组中的每一项又是一个链表。当新建一个HashMap的时候，就会初始化一个数组。



当我们往HashMap中put元素的时候，先根据key的hashCode重新计算hash值，根据hash值得到这个元素在数组中的位置（即下标）， 
如果数组该位置上已经存放有其他元素了，那么在这个位置上的元素将以链表的形式存放，新加入的放在链头，最先加入的放在链尾。如果数组该位置上没有元素，就直接将该元素放到此数组中的该位置上。

HashMap 底层是数组+链表，默认大小16

通一个槽位过多数据，也会进行大量的equals比较降低了效率（碰撞-后进来放前面）

加载因子75%扩容。（Hash算法重排序）

无法避免同一个槽位数据过多。（效率低）

Jdk1.8 数组+链表（加在末尾）+ 红黑树（总元素大于64 单个大于8）

添加效率低，其他效率都高

Jdk1.8 ConcurrentHashMap：CAS算法（底层操作系统支持的算法） 无锁添加

### 4、IO

![IO流](https://github.com/gaoyuanyuan2/notes/blob/master/img/7.png) 

1.foreach与正常for循环效率对比

循环数组结构的数据时，建议使用普通for循环；循环链表结构的数据时，一定不要使用普通for循环。

2.记得flush刷出，和close

### 5、注解

 Annotation的作用:
 
 不是程序本身,可以对程序作出解释。(这一点，跟注释没什么区别)-可以被其他程序(比如:编译器等读取。(注解信息处理流程,是注解和注释的重大区别。如果没有注解信息处理流程,则注解毫无意义。
 
 ![注解](https://github.com/gaoyuanyuan2/notes/blob/master/img/12.png) 
 
 ![注解](https://github.com/gaoyuanyuan2/notes/blob/master/img/13.png) 
 
 ![注解](https://github.com/gaoyuanyuan2/notes/blob/master/img/14.png) 
 
 ![注解](https://github.com/gaoyuanyuan2/notes/blob/master/img/15.png) 
 
 ![注解](https://github.com/gaoyuanyuan2/notes/blob/master/img/16.png) 
 

### 6、反射

1. setAccessible

启用和禁用访问安全检查的开关值为true则指示反射的对象在使用时应该取消Java语言访问检查。

值为false则指示反射的对象应该实施Java语言访问检查。并不是为true就能访问为false就不能访问。

禁止安全检查,可以提高反射的运行速度。

普通方法调用，执行10亿次，耗时: 2258ms

反射动态方法调用，执行10亿次，耗时: 52687ms

反射动态方法调用,跳过安全检查，执行10亿次，耗时: 14305ms

2. Java采用泛型擦除的机制来引入泛型

Java中的泛型仅仅是给编译器javac使用的,确保数据的安全性和免去强制类型转换的麻烦。但是，一旦编译完成,所有的和泛型有关的类型全部探除。

为了通过反射操作这些类型以迎合实际开发的需要, Java就新增了ParameterizedType，GeneriCArrayType，TypeVariable和WildcardType几种类型来代表不能被归一到Class类中的类型但是文和原始类型齐名的类型。

ParameterizedType:表示一种参数化的类型 ,比如Collection<String>

GenericArrayType:表示种元素类型是参数化类型或者类型变最的数组类型TypeVariable:是各种类型变量的公共父接口

WildcardType:代表一种通配符类型表达式,比如?, ? extends Number, ? super Integer[wildcard是一个单词 :就是“通配符”]

3. JAVA 6.0引入了动态编译机制

1)动态编译的应用场景:

可以做一个浏览器端编写java代码,上传服务器编译和运行的在线评测系统。


服务器动态加载某些类文件进行编译动态编译的两种做法:

a. 要通过Runtime调用javac ,启动新的进程去操作

b. 通过JavaCompiler动态编译

4. JAVA脚本弓擎是从JDK6.0之后添加的新功能。脚本引擎介绍:

一使得Java应用程序可以通过一 套固定的接口与各种脚本引擎交互,从
而达到在Java平台上调用各种脚本语言的目的。Java脚本API是连通Java平台和脚本语言的桥梁。
可以把一些复杂异变的业务逻辑交给脚本计国处理,这又大大提高了开发效率。

运行时操作字节码可以让我们实现如下功能:

动态生成新的类

动态改变某个类的结构(添加/删除/修改   新的属性/方法)

优势:

比反射开销小,性能高。

Javassist性能高于反射,低于ASM

5. 常见的字节码操作类库  

1) BCEL

 Byte Code Engineering Library (BCEL) ,这是Apache Software Foundation的Jakarta项目的一部分。
 
 BCEL是Java classworking广泛使用的一种框架，它可以让您深入JVM汇编语言进行类操作的细节。
 BCEL 与Javassist有不同的处理字节码方法, 
 BCEL在实际的JVM指令层次上进行操作(BCEL拥有丰富的JVM指令级支持)而Javassist所强调的是源代码级别的工作。
 
2) ASM

是一个轻量级java字节码操作框架,直接涉及到JVM底层的操作和指令CGLIB(Code Generation Library)

是一个强大的，高性能,高质量的Code生成类库,基于ASM实现。

Javassist是一个开源的分析、编辑和创建Java李节码的关库。性能较ASM差,跟cglib差不多,但是使用简单。很多开源框架都在使用它。

![](https://github.com/gaoyuanyuan2/notes/blob/master/img/21.png) 

6. 类加载

1) 加载

加载是类加载过程中的一个阶段，这个阶段会在内存中生成一个代表这个类的java.lang.Class对象，作为方法区这个类的各种数据的入口。注意这里不一定非得要从一个Class文件获取，这里既可以从ZIP包中读取（比如从jar包和war包中读取），也可以在运行时计算生成（动态代理），也可以由其它文件生成（比如将JSP文件转换成对应的Class类）。

2) 链接 

将Java类的二进制代码合并到JVM的运行状态之中的过程

 验证:确保加载的类信息符合JVM规范。没有安全方面的问题。
 
 准备:正式为类变量(static变量)分配内存并设置类变量初始值的阶段，这些内存都将在方法区中进行分配
 
 解析：虚拟机常量池内的符号引用替换为I接引用的过程
 
3) 初始化

初始化阶段是执行类构造器< clinit> 0方法的过程。类构造器< clinit> ()方法是由编译器自动收集类中的所有类变量的赋值动作和静态语句块(static块)中的语句合并产生的。

当初始化-个类的时候，如果发现其父类还没有进行过初始化、则需要先出发其父类的初始化虚拟机会保证一个类的<clinit> (方法在多线程环境中被正确加锁和同步。

java中final的值在编译时就放入了常量池，调用的话也不会引起final所在类的初始化。

a. 在new、getstatic、putstatic、invokestatic一个类或其中字段时，
若类还没有初始化，则这个类现在必须初始化。

b. 调用反射关于这个类的方法、字段、类本身时，
若类还没有初始化，则这个类现在必须初始化。

c. 初始化一个类时，当发现其父类还没有初始化时，先初始化其父类。

d. JVM启动时，会初始化用户定义的main所在的类。

e. 涉及1.7后的动态语言支持

![](https://github.com/gaoyuanyuan2/notes/blob/master/img/22.png) 

7.加载器

1) 类的主动引用(一定会发生类的初始化)

new-个类的对象

调用类的静态成员除了final常量和静态方法使用java.lang.elect包的方法对类进行反射调用
当虚报机启动，java Hello, 则-定会初始化Hello类。说白了就是先启动main方法所在的类当初始化一个类.如果其父类没有被初始化，则先会初始化他的父类

2) 类的被动引用(不会发生类的初始化)

当访问一个静态城时，只有真正声明这个城的类才会被初始化。通过子类引用父类的静志安量，不会导数子类机始化通过数相定义类引用，不会触发此类的物始化
引用常量不会触发此类的初始化(常量在编译阶段就存入调用类的常量池中了)

3) 引导类加载器( bootstrap class loader)

它用来加载Java的核心库JAVA HOME/jre/1ib/rtjar或sun.bootclass.path路径下的内容) ,是用原生代码来实现的,并不继承自java.lang.Cassloader.
 加载扩展类和应用程序类加载器。并指定他们的父类加载器。
 
4) 扩展类加载器( extensions class loader )

用来加载Java的扩展库(JAVA HOME/jre/ext/* jar，或java. extdirs路径下的内容)。Java虚拟机的实现会提供一个扩展库目录。 该类加载器在此目录里面查找并加载Java类。
由sun.misc.LauncherSExtClassLoader

5) 实现应用程序类加载器( application class loader )

它根据Java应用的类路径( classpath,javaclasspath路径下的内容)来加载Java类。
一般来说 ，Java应用的类都是由它来完成加载的。  广由sun.misc.LauncherSAppClassLoader

6) 实现自定义类加载器

开发人员可以通过继承javalang.CassLoader类的方式实现自己的类加载器，以满足一些特殊的需求。

8.代理模式

交给其他加载器来加载指定的类

9.双亲委托机制

就是某个特定的类加载器在接到加载类的请求时，首先将加载任务委托给父类加载器，依次追溯，直到最高的爷爷辈的，如果父类加载器可以完成类加载任务，就成功返回;只有父类加载器无法完成此加载任务时，才自己去加载。
双亲委托机制是为了保证Java核心库的类型安全。

这种机制就保证不会出现用户自已能定义java.lang.Object类的情况。类加载器除了用于加载类，也是安全的最基本的屏障。双亲委托机制是代理模式的一种
并不是所有的类加载器都采用双亲委托机制。

tomcat服务器类加载器也使用代理模式,所不同的是它是首先尝试去加载某个类,如果找不到再代理给父类加载器。这与一般类加载器的顺序是相反的

10.双亲委托机制以及默认类加载器的问题

一般情况下，保证同一个类中所关联的其他类都是由当前类的类加载器所加载的.

比如，ClassA本身在Ext下找到，那么他里面new出来的一些类也就只能用Ext去查找了(不会低个级别)， 所以有些明明App可以找到的,却找不到了。

JDBC API,他有实现的driven部分( mysql/sql server )， 我们的JDBC API都是由Boot或者Ext来载入的，但是
JDBC driver却是由Ext或者App来载入，那么就有可能找不到driver了.在Java领域中,其实只要分成这种Api+SPI(Service Provide Interface，特定厂商提供)的，都会遇到此问题。
 
 常见的SPI有JDBC ICE、 JNDI JAXP和JBI等。这些SPI的接口由lava核心库来提供。如JAXP的SPI接口定义包含在javax.xml.parsers包中。SPI 的接口是Java核心库的一部分，是由引导类加载器来加载的;SP1实现的Java类般是由系统类加载器来加载的。引导类加载器是无法找到SPI的实现类的,因为它只加载Java的核心库

通常当你需要动态加载资源的时候，你至少有三个ClassLoader可以选择:

a. 系统类加载器或叫作应用类加载器(system classloader or application classloader)
 
b. 当前类加载器

c. 当前线程类加载器

当前线程类加载器是为了抛弃双亲委派加载链模式。

每个线程都有一个关联的上下文类加载器。如果你使用new Thread0方式生成新的线程，新线程将继承其父线程的上下文类加载器。如果程序对线程上下文类加载器没有任何改动的话，程序中所有的线程将都使用系统类加载器作为上下文类加载器。
Thread.currentThread().getContextClassLoader()

10. TOMCAT服务器的类加载机制

TOMCAT不能使用系统默认的类加载器。

如果TOMCAT跑你的WEB项目使用系统的类加载器那是相当危险的,你可以直接是无忌惮是操作系统的各个目录了。

对于运行在Java EE"容器中的Web应用来说，类加载器的实现方式与一般的Java应用有所不同。

每个Web应用都有一个对应的类加载器实例。该类加载器也使用代理模式(不同于前面说的双亲委托机制)，所不同的是它是首先尝试去加载某个类，如果找不到再代理给父类加载器。这与一般类加载器的顺序是相反的
但也是为了保证安全，这样核心库就不在查询范围之内。为了安全TOMCAT需要实现自己的类加载器。

我可以限制你只能把类写在指定的地方，否则我不给你加载!

![](https://github.com/gaoyuanyuan2/notes/blob/master/img/23.png) 








