## Java编程模型

* OOP

* AOP

1.Java静态接口

`java.util.logging.Filter`

`java.util.EventListener`

2、字节码提升

ASM(ObjectWeb)

CGLIB

Javassist(JBoss)

BCEL(Apache)

3、Java动态代理

`java.lang.reflect.Proxy`

`java.lang.reflect.InvocationHandler`


* 面向元信息编程（MDOP）

泛型

反射

注解

* 面向函数编程（FOP）

函数式接口

默认方法

方法应引用

* 面向模块编程（MOP）

## Java 编程思想

* 契约编程

* 设计模式

1.面向对象设计模式

构造模式

结构模式

行为模式

并发模式

2.面向元数据设计模式

泛型接口设计

注解驱动设计

3.面向切面设计模式

判断模式

拦截模式

4.面向函数设计模式

函数式接口设计（SCFP）

Fluent API 设计

Reactive/Stream API设计

* 模式驱动

接口驱动

函数驱动

配置驱动

模块驱动

注解驱动


## JSP有9个内置对象：

* request：封装客户端的请求，其中包含来自GET或POST请求的参数；
* response：封装服务器对客户端的响应；
* pageContext：通过该对象可以获取其他对象；
* session：封装用户会话的对象；
* application：封装服务器运行环境的对象；
* out：输出服务器响应的输出流对象；
* config：Web应用的配置对象；
* page：JSP页面本身（相当于Java程序中的this）；
* exception：封装页面抛出异常的对象。

## JSP中的四种作用域包括page、request、session和application，具体来说：
   
* page代表与一个页面相关的对象和属性。
* request代表与Web客户机发出的一个请求相关的对象和属性。
一个请求可能跨越多个页面，涉及多个Web组件；需要在页面显示的临时数据可以置于此作用域。
* session代表与某个用户与服务器建立的一次会话相关的对象和属性。
跟某个用户相关的数据应该放在用户自己的session中。
* application代表与整个Web应用程序相关的对象和属性，它实质上是跨越整个Web应用程序，
包括多个页面、请求和会话的一个全局作用域。

## Cookie

优点: 数据可以持久保存，不需要服务器资源，简单，基于文本的Key-Value

缺点: 大小受到限制，用户可以禁用Cookie功能，由于保存在本地，有一定的安全风险。

Cookie 数据保存在客户端(浏览器端)，Session 数据保存在服务器端。

Cookie 存储在客户端中，而Session存储在服务器上，相对来说 Session 安全性更高。
如果使用 Cookie 的一些敏感信息不要写入 Cookie 中，
最好能将 Cookie 信息加密然后使用到的时候再去服务器端解密。


