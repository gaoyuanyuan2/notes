## JDK 新特性
### 1、jdk5
<br>1.增强for
```Java
for(String item : set){
    System.out.println("元素："+ item);
}
```
<br><br>2.静态导入
<br><br>3.枚举
<br>注意事项
<br>定义枚举类要用关键字enum所有枚举类都是Enum的子类
<br>枚举类的第一行，上必须是枚举项， 最后一个枚举项后的分号是可以省略的，但是如果枚举类有其他的东西这个分号就不能省略。建议不要省略
<br>枚举类可以有构造器，但必须是private的，  它默认的也是private的。枚举项的用法比较特殊:枚举("");枚举类也可以有抽象方法，但是枚举项必须重写该方法
### 2、jdk7
<br>1.二进制字面量
<br>通过在数字前面加入0b或者0B来标示一个二进制的字面量
```Java
    byte aByte = (byte)0b00100001;//一个8位'byte'值：
    short aShort = (short)0b1010000101000101;//一个16位'short'值:
    int anInt1 = 0b10100001010001011010000101000101;//一些32位'int'值:
    int anInt2 = 0b101;
    int anInt3 = 0B101; // B可以是大写也可以是小写.
    //一个64位的'long'值. 注意"L"结尾:
    long aLong = 0b1010000101000101101000010100010110100001010001011010000101000101L;
```
<br><br>2.数字字面量可以出现下划线
<br>数字的开头和结尾
<br>在浮点数中与小数点相邻
<br>F或者L后缀之前
<br>在预期数字串的位置
```Java
    long creditCardNumber = 1234_5678_9012_3456L;
    long socialSecurityNumber = 999_99_9999L;
    float pi =  3.14_15F;
    long hexBytes = 0xFF_EC_DE_5E;
    long hexWords = 0xCAFE_BABE;
    long maxLong = 0x7fff_ffff_ffff_ffffL;
    byte nybbles = 0b0010_0101;
    long bytes = 0b11010010_01101001_10010100_10010010;
```
<br><br>3.switch语句可以用字符串
<br><br>4.泛型简化
```Java
    Map<String, List<String>> myMap = new HashMap<>();
```
<br><br>5.异常的多个catch合并
<br><br>6.try..with...resource语句（不好用）
<br>资源自动释放，不需要close
```Java
try (FileReader fr = new FileReader("E:\\zikao\\file\\cs.txt");
    FileWriter fw = new FileWriter("E:\\zikao\\file\\cs1.txt");) {
    int ch = 0;
    while ((fr.read()) != -1) {
        fw.write(ch);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```
### 3、jdk8
<br>特点：
<br>速度更快
<br>代码更少(增加了新的语法Lambda表达式)
<br>强大的Stream API
<br>便于并行
<br>最大化减少空指针异常Optional
<br><br>1.Lambda表达式
```Java
public class Java8Tester {
   public static void main(String args[]){
      Java8Tester tester = new Java8Tester();
      // 类型声明
      MathOperation addition = (int a, int b) -> a + b;
      // 不用类型声明
      MathOperation subtraction = (a, b) -> a - b;
      // 大括号中的返回语句
      MathOperation multiplication = (int a, int b) -> { return a * b; };
      // 没有大括号及返回语句
      MathOperation division = (int a, int b) -> a / b;
      System.out.println("10 + 5 = " + tester.operate(10, 5, addition));
      System.out.println("10 - 5 = " + tester.operate(10, 5, subtraction));
      System.out.println("10 x 5 = " + tester.operate(10, 5, multiplication));
      System.out.println("10 / 5 = " + tester.operate(10, 5, division));
      // 不用括号
      GreetingService greetService1 = message ->
      System.out.println("Hello " + message);
      // 用括号
      GreetingService greetService2 = (message) ->
      System.out.println("Hello " + message);
      greetService1.sayMessage("Runoob");
      greetService2.sayMessage("Google");
   }
    
   interface MathOperation {
      int operation(int a, int b);
   }
    
   interface GreetingService {
      void sayMessage(String message);
   }
    
   private int operate(int a, int b, MathOperation mathOperation){
      return mathOperation.operation(a, b);
   }
}
```
<br>Lambda 表达式，也可称为闭包，它是推动 Java 8 发布的最重要新特性。
<br>Lambda 允许把函数作为一个方法的参数（函数作为参数传递进方法中）。
<br>使用 Lambda 表达式可以使代码变的更加简洁紧凑。
<br><br>
[Java 8 函数式接口](http://www.runoob.com/java/java8-functional-interfaces.html) 
<br><br>2.Stream函数式操作流元素集合
<br><br>1)流(Stream)  到底是什么呢?
<br>是数据渠道，用于操作数据源(集合、数组等)所生成的元素序列。“集合讲的是数据，流讲的是计算!”
<br><br>2)注意:
<br>Stream自己不会存储元素。
<br>Stream不会改变源对象。相反，他们会返回一个持有结果的新Stream。③Stream操作是延迟执行的。这意味着他们会等到需要结果的时候才执行。
<br><br>Stream的操作三个步骤
<br><br>3)创建Stream
<br>一个数据源(如:集合、数组)，获取一个流
<br><br>中间操作
<br>一个中间操作链，对数据源的数据进行处理
<br>多个中间操作可以连接起来形成一条个流水线，除非流水
线上触发终止操作，否则中间操作不会执行任何的处理!
而在终止操作时一次性全 部处理，称为“惰性求值”。
<br><br>终止操作(终端操作)
<br>一个终止操作，执行中间操作链，并产生结果
我:

<br><br>筛选与切片

|方法|描述|
|:--:|:--:|
|filter (Predicate p)|接收Labda，从流中排除某些元求。
|distinct()|筛选，通过流所生成元素的hashCode() 和equals()去除重复元家|
|limit(long maxSize)|截断流，使其元素不超过给定数量。|
|skip(long n)|跳过元素，返回一个扔掉了前n个元素的流。若流中元素不足n个，则返回一个空流。与limit(n) 互补|

<br><br>映射

|方法|描述|
|:--:|:--:|
|map(Function f)|接收一个的数作为参数，该雨数会被应用到每个元素上，并将其映射成一个新的元素.|
|mapToDouble (ToDoublePunction f)|接收一个雨 数作为参数，该的数会被应用到每个元素上，产生一个新的DoubleStream.|
|mapToInt(TolntFunction f)|接收一个函数作为参数，该函数会歧应用到每个元素上，产生一个新的IntStream.|
|mapToLong(TolongFunction f)|接收一个函数作为参数，该函数会被应用到每个元素上，产生一个新的LongStream|
|flatMap(Function f)|接收一个函数作为参数，将流中的每个值都换成另一个流，然后把所有流连接成一个流|

<br><br>排序

|方法|描述|
|:--:|:--:|
|sorted()|产生一个新流，其中按自然顺序排序|
|sorted (Comparator comp)|产生一个新流，其中按比较器顺序排序|

<br><br>查找与匹配

|方法|描述|
|:--:|:--:|
|allMatch|检查是否匹配所有元素anyMatch-检查是否至少匹配一 个元素|
|noneMatch|检查是否没有匹配所有元素findFirst-返回第- - 个元素|
|findAny|返回当前流中的任意元素count-返回流中元素的总个数max-返回流中最大值min-返回流中最小值|

<br><br>归约

|方法|描述|
|:--:|:--:|
|reduce(T iden, BinaryOperator b)|可以将流中元素反复结合起来， 得到一个值。  返回T|
|reduce (BinaryOperator b)   |可以将流中元素反复结合起来，得到一个值。近回Optiona1<T> |

<br>备注: map和reduce的连接通常称为map-reduce模式，因Google用它来进行网络搜索而出名。

<br><br>收集

|方法|描述|
|:--:|:--:|
|collect (Collector c)|将流转换为其他形式。 接收一个Collector楼口的实现，用于给Stream中元素做汇总的方法|

[Java 8 Stream](http://www.runoob.com/java/java8-streams.html) 
<br><br>3.接口新增：默认方法与静态方法
<br><br>4.方法引用,与Lambda表达式联合使用
<br><br>5.引入重复注解
<br><br>6.类型注解
<br><br>7.最新的Date/Time API (JSR 310)
<br><br>8.新增base64加解密API
<br><br>9.数组并行（parallel）操作
<br><br>10.JVM的PermGen空间被移除：取代它的是Metaspace（JEP 122）元空间
<br>使用Metaspace（JEP 122）代替持久代（PermGen space）。在JVM参数方面，使用-XX:MetaSpaceSize和-XX:MaxMetaspaceSize代替原来的-XX:PermSize和-XX:MaxPermSize。
<br><br>
 ![详情](https://github.com/gaoyuanyuan2/notes/blob/master/img/19.png) 
 <br><br>
<br><br>11.并发性
<br>Jdk8 数组+链表（加在末尾）+红黑树（均衡二叉树）（总元素大于64 单个大于8）添加效率低，其他效率都高
<br>Jdk8 ConcurrentHashMap：CAS算法（底层操作系统支持的算法）无锁添加内存结构改变。
<br>java.util.concurrent 程序包中新增了一些类和接口。
<br>java.util.concurrent.ConcurrentHashMap 类中新增了一些方法，支持基于新增流工具和 lambda 表达式的聚合操作。
<br>java.util.concurrent.atomic 程序包中新增了一些类来支持可扩展、可更新的变量。
<br>java.util.concurrent.ForkJoinPool 类中新增了一些方法来支持通用池。
<br>新增的 java.util.concurrent.locks.StampedLock 类提供了一个基于能力的锁，可通过三种模式来控制读/写访问。

<br>12.数据流定义
<br>想象一条河。河流从哪里开始？河流在哪里？我们对河流的理解本质上是流动的概念。这条河没有开始也没有结束。流数据非常适合于没有离散开头或结尾的数据。
<br>例如，交通灯的数据是连续的，没有“开始”或“完成”。数据流是连续而不是分批发送数据记录的过程。通常，数据流对于在生成数据时在连续流中以小尺寸（通常以千字节为单位）发送数据的数据源类型是有用的。这可能包括各种各样的数据源，例如来自连接设备的遥测，客户使用您的Web应用程序生成的日志文件，电子商务交易或来自社交网络或地理空间服务的信息。
传统上，数据是分批移动的。批处理通常同时处理大量数据，具有长时间的延迟。例如，该过程每24小时运行一次。虽然这可以是处理大量数据的有效方法，但它不适用于要流式传输的数据，因为数据在处理时可能是陈旧的。
数据流是时间序列和随时间检测模式的最佳选择。例如，跟踪Web会话的长度。大多数物联网数据非常适合数据流。交通传感器，健康传感器，交易日志和活动日志等都是数据流的理想选择。
此流数据通常用于实时聚合和关联，过滤或采样。通过数据流，您可以实时分析数据，并深入了解各种活动，例如计量，服务器活动，设备地理位置或网站点击。

<br>请考虑以下方案：
<br>金融机构跟踪市场变化并根据配置的约束（例如达到特定股票价值时的卖出）调整客户组合的设置。
<br>电网监控吞吐量并在达到某些阈值时生成警报。
<br>新闻源从各种平台流式传输点击流记录，并使用人口统计信息丰富数据，以便它可以提供与受众人口相关的文章。
<br>电子商务站点流式传输点击流记录以查找数据流中的异常行为，并在点击流显示异常行为时生成安全警报。

<br>数据流挑战
<br>数据流是一种功能强大的工具，但在使用流数据源时，有一些常见的挑战。以下列表显示了数据流时要规划的一些事项：
<br>规划可扩展性。
<br>规划数据持久性。
<br>在存储层和处理层中加入容错。

<br>数据流工具
<br>随着流数据的增长，出现了许多适合与之合作的解决方案。以下列表显示了一些用于处理流数据的常用工具：
<br>Amazon Kinesis Firehose。Amazon Kinesis是一种托管，可扩展，基于云的服务，允许实时处理大型数据流。
<br>Apache Kafka。Apache Kafka是一个分布式发布 - 订阅消息传递系统，它集成了应用程序和数据流。
<br>Apache Flink。Apache Flink是一种流数据流引擎，为数据流上的分布式计算提供了便利。
<br>Apache Storm。Apache Storm是一个分布式实时计算系统。Storm用于分布式机器学习，实时分析以及许多其他情况，尤其是具有高数据速度的情况。
<br>大规模管理数据并不难。了解完全免费的  开源HPCC Systems  平台如何使其更易于更

### 4、JAVA9
<br>1.  抽象类和接口的异同?
<br><br>1) 二者的定义:
<br>a. 声明的方式  
<br>b.内部的结构(jdk 7 ;jdk 8 ; jdk 9)
<br>2) 共同点;不能实例化;以多态的方式使用不同点:单继承;  多实现
```java
interface MyInterface{
    //jdk 7 :只能声明全局常量(public static final )和抽象方法(public abstract)void method1();
    
    // jdk 8 :声明静态方法和默认方法
    public static void method2(){
        System. out . println("method2");
    }
    default void method3( ){
        System.out.println("method3");
    }
    //jdk 9 :声明私有方法
}

```

<br><br>2.  String
<br>String: jdk 8及之前:底层使用char[]存储; jdk 9 :底层使用byte[] (encoding flag)
<br>StringBuffer:jdk 8及之前:底层使用char[]存储; jdk 9 :底层使用byte[]
<br>StringBuilder:jdk 8及之前:底层使用char[]存储; jdk 9 :底层使用byte[]
<br><br>String:不可变的字符序列;
<br>StringBuffer:可变的字符序列;线程安全的，效率低;
<br>StringBuilder:可变的字符序列;线程不安全的，效率高(jdk 5. 0)
#### 新特性1：jdk8和jdk9中jdk目录结构的变化
#### 新特性2：模块化的特性
#### 新特性3：jshell命令的使用
#### 新特性4：多版本兼容jar包的使用说明
#### 新特性5：接口中定义私有方法
#### 新特性6：钻石操作符的使用升级
#### 新特性7：异常处理try结构的使用升级
#### 新特性8：下划线命名标识符的限制
#### 新特性9：String底层存储结构的变化
#### 新特性10：创建只读集合
#### 新特性11：Optional提供的stream()
#### 新特性12：多分辨率图像API
#### 新特性13：全新的Http客户端API
#### 新特性14：Deprecated的相关API
#### 新特性15：智能java编译工具
#### 新特性16：统一的JVM日志系统
#### 新特性17：javadoc的HTML5支持
#### 新特性18：Javascript的Nashorn引擎升级
#### 新特性19：java的动态编译器
#### Reactive Streams
核心组件
Publisher
Subscriber
Subscription
Processor
Reactive StreamsReactive X

Reactive Streams前时代
时代局限性(Java9之前)
阻塞编程
无法并行计算资源低效使用-异步编程
CallbackFuture

Reactive Streams规范Reactive编程
一种异步编程的示范,这种示范与数据流式处理以及变化传播相关联,同时也经常被面向对象语言表示,作为一种观察者模式的扩展。
Reactive Stream规范(Java语言)
https://github.com/reactive-streams/reactive-streams-jvm

Reactive Streams规范
对比Iterator模式
数据方向
Reactive Streams : 推模式( Push )Iterator : 拉模式( Pull )编程模式
Reactive Streams :发布-订阅模式( Publish-Subscriber )Iterator :命令式编程模式( Imperative )

Reactive Streams规范
onSubscribe() :订阅事件
onNext() :数据达到事件
onComplete() :订阅完成事件
onError() :订阅异常
request() :请求
cancel() :取消
http://docs.oracle.com/javase/9/whatsnew/toc.htm

Flow API
Publisher<T>
Subscriber<T>
Processor<T,R>
Subscription

集合工厂方法( Factory Method of Collections )进程( Process )

堆栈API ( Stack-Walking API )变量处理( Variable Handles )

统一日志API ( Platform Logging API )自旋等待提示( Spin-Wait Hints )压缩字符串( Compact String )

GitHub资源: https://github.com/mercyblitz
