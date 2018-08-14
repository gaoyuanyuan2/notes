## JAVASE
### 1、类型
<br><br>1.10到其他进制的转化，除余法。
<br><br>2.0正 1负，正数的补码和原码相同，负数的补码是反码基础上加1.
<br><br>3.计算机操作的时候都是采用数据对应的二进制补码来计算的。
<br><br>4.数据向上转型、强制转化：大到小、8位一个字节
<br><br>
 ![类型](https://github.com/gaoyuanyuan2/notes/blob/master/img/17.png) 
<br><br>
<br>5.位异或运算 ^ ：相同则为0，不相同则为1
<br><br>6.位非运算符~：如果位为0，结果是1，如果位为1，结果是0
<br><br>7.补码原码
<br>        符号位 数值位
<br>补码:     1    0000010
<br>反码:     1    0000001
<br>原码:     1    1111110
<br><br>8.移位
<br> <<:左移左边最高位丢弃，右边补齐0
<br> >>:右移最高位是0，左边补齐0;最高为是1，左边补齐1
<br> >>>:无符号右移无论最高位是0还是1，左边补齐0
<br><br>9. switch 
<br> 表达式的取值，bvte short int char。JDK5以后可以是枚举. JDK7以后可以是String
<br><br>10.集合和泛型只能为引用类型
<br><br>11.泛型
<br>正确方式:
<br>
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
<br>总结:使用?通配符可以引用其他各种参数化的类型, ?通配符定义的变量主要用作引用,可以调用与参数化无关的方法，不能调用与参数化有关的万法。
<br>T限定通配符的上边界:
<br>正确: Vector<? extends Number> x = new Vector<Integer>();
<br>错误: Vector<? extends Number> x = new Vector<String>();
<br>?限定通配符的下边界:
<br>正确: Vector<super Integer> x = new Vector<Number>();
<br>错误; Vector<? super Integer> x = new Vector<Byte>();
<br>Java中的泛型类型(或者泛型)类似于C++中的模板。但是这种相似性仅限于表面，Java 语言中的泛型基本上完全是在编译器中实现，
用于编译器执行类型检查和类型推断，状后生成普通的非泛型的字节码，这种实现技术称为擦除(erasure) (编译器使用泛型类型信息保
证类型安全，然后在生成字节码之首将其清除)。这是因为扩展虚拟机指令集来支持泛型被认为是无法接受的。
### 2、对象
1.抽象的(abstract) 方法是否可同时是静态的(static) ,是否可同时是本地方法(native) ，是否可同时被synchronized修饰?
都不能。抽象方法需要子类重写，而静态的方法是无法被重写的，因此二者是矛盾的。
本地方法是由本地代码(如C代码)实现的方法，而抽象方法是没有实现的，也是矛盾的。
synchronized和方法的实现细节有关，抽象方法不涉及实现细节，因此也是相互矛盾的。
<br><br> 2. 如何实现对象克隆?
 <br> 1)实现Cloneable接口并重写Object类中的clone(方法;
  <br>2)实现Serializable接口, 通过对象的序列化和反序列化实现克隆，可以实现真正的深度克隆。
 <br><br> 3.工具类构造器私有化
 <br><br> 4.创建对象的代价是非常昂贵的
 <br><br> 5.重用对象会导致潜在错误和安全漏洞
 <br><br> 6.防内存泄漏：一旦数组元素变成非活动部分的部分，就手动清空这些数组元素；缓存遗忘，定时清理（LinkedHashMap 类的removeEldestEntry方法，更复杂的用java.lang.ref）;客户端在API中注册回调，没有显示的取消注册。
<br><br>7.终结方法：不建议使用。除非是安全网终止非关键本地资源，记住要调用super.finalize ，记录非法用法。与共有的非final类关联起来，考虑使用守卫者，确保执行（及时子类终结方法未调用super.finalize）
<br><br>8.protected void   finalize()当垃圾回收器确定不存在对该对象的更多引用时，由对象的垃圾回收器调用此方法。
<br><br>9.类加载的五个过程：加载、验证、准备、解析、初始化
<br><br>10.定义 DO/DTO/VO 等 POJO 类时，不要设定任何属性默认值，必须写 toString 方法
<br><br>11.使用索引访问用 String 的 split 方法得到的数组时，需做最后一个分隔符后有无内容的检查，否则会有抛 IndexOutOfBoundsException 的风险
<br><br>12.Object方法
<br>1)	equals 方法:值类需要覆盖equals方法(枚举类除外)
<br>反自性、传递性、一致性
<br>2)	高质量的equals：== （性能优化，如果是返回true），  instanceof 正确的类型 不是返回false，顺序
<br>3)	覆写equals必须覆写hashCode，相等的对象必须有相等的散列码。
<br>4)	始终要覆盖toString （自描述）
<br>5)	Clone 从不覆写改方法，也不调用，除非拷贝数组。
<br>6)	考虑实现comparable接口
<br>7)	构造器不能被继承，因此不能被重写，但可以被重载
<br>8)	抽象类中的成员可以是private、默认、protected、public的，而接口中的成员全都是public的。抽象类中可以定义成员变量，而接口中定义的成员变量实际上都是常量。
<br>9)	抽象方法需要子类重写，而静态的方法是无法被重写的
<br>10)	Clone equal tostring hashcode wait notify notifyall getClass
<br>11)	hashcode那就会使效率提高很多，桶
<br><br>13.通用程序设计
<br>1)	精确计算不使用float 和double 使用BigDecimal。9位内使用int，18位内使用long
<br>2)	如果其他类型更适合，尽量避免使用字符串。
<br>3)	重复n个字符串连接，需要n的平方级时间。使用StringBuilder 的append方法。
<br>4)	接口引用对象会使程序更加灵活。
<br>5)	接口优于反射机制。
<br>6)	再多底层优化无法弥补算法选择不当。

### 3、集合框架体
![集合](https://github.com/gaoyuanyuan2/notes/blob/master/img/5.png) 
<br><br>
![空值](https://github.com/gaoyuanyuan2/notes/blob/master/img/6.png) 
<br><br>
1.提供排序的比较器,业务比较器
<br>实现java. util. Comparator接口，
<br>重写public  int compare(T o1,  To2);作用:
<br>作用 解耦:独立于实体类 方便:便于应对各种排序规则

### 4、IO
![IO流](https://github.com/gaoyuanyuan2/notes/blob/master/img/7.png) 
1.foreach与正常for循环效率对比
循环数组结构的数据时，建议使用普通for循环；循环链表结构的数据时，一定不要使用普通for循环。

### 5、注解
 Annotation的作用:
 不是程序本身,可以对程序作出解释。(这一点，跟注释没什么区别)-可以被其他程序(比如:编译器等读取。(注解信息处理流程,是注解和注释的重大区别。如果没有注解信息处理流程,则注解毫无意义。
 <br><br>
 ![注解](https://github.com/gaoyuanyuan2/notes/blob/master/img/12.png) 
 <br><br>
 ![注解](https://github.com/gaoyuanyuan2/notes/blob/master/img/13.png) 
 <br><br>
 ![注解](https://github.com/gaoyuanyuan2/notes/blob/master/img/14.png) 
 <br><br>
 ![注解](https://github.com/gaoyuanyuan2/notes/blob/master/img/15.png) 
 <br><br>
 ![注解](https://github.com/gaoyuanyuan2/notes/blob/master/img/16.png) 
 <br><br>







