# Servlet容器

1、Servlet容器启动会扫描，当前应用里面每一个jar包的

	ServletContainerInitializer的实现
	
2、提供ServletContainerInitializer的实现类；

	必须绑定在，META-INF/services/javax.servlet.ServletContainerInitializer
	
	文件的内容就是ServletContainerInitializer实现类的全类名；

总结：容器在启动应用的时候，会扫描当前应用每一个jar包里面

META-INF/services/javax.servlet.ServletContainerInitializer

指定的实现类，启动并运行这个实现类的方法；传入感兴趣的类型；


ServletContainerInitializer；

@HandlesTypes；

## Servlet

![Servlet](/img/44.png) 

Servlet是一种基于Java技术的Web组件，用于生成动态内容，由容器管理。类似于其他Java技术组件，Servlet 是平台无关的Java类组成，
并且由JavaWeb服务器加载执行。
通常情况，由Servlet容器提供运行时环境。Servlet 容器，有时候也称作为Servlet引擎，作为Web服务器或应用服务器的一部分。
通过请求和响应对话，提供Web客户端与Servlets交互的能力。容器管理Servlets实例以及它们的生命周期。


从功能上，Servlet 介于CGI ( Common Gateway Interface)与服务扩展(如: Netscape Server API或Apache模块)之间。

在体系上，Servlet 技术( 或者规范)属于JavaEE技术(规范)的一部分。不过Servlet并非一开始就隶属于J2EE或者JavaEE。

Java Servlet是和平台无关的服务器端组件,它运行在Servlet容器中。Servlet容器负责Servlet和客户的通信以及调用Servlet的方法, 
Servlet和客户的通信采用“请求/响应"的模式。

##  GenericServlet(了解)
   
1、是一个Servlet. 是Servlet接口和ServletConfig接口的实现类但是一个抽象类。其中的service方法为抽象方法

2、如果新建的Servlet程序直接继承GenericServlet会使开发更简洁。

3、具体实现:

①.在GenericServlet 中声明了一个ServletConfig类型的成员变量,在init(ServletConfig)方法中对其进行了初始化。

②.利用servletConfig成员变量的方法实现了ServletConfig接口的方法。

③.还定义了一个init()方法,在init(ServletConfig)方法中对其进行调用,子类可以直接覆盖init,在其中实现对Servlet的初始化。

④.不建议直接覆盖init(ServletConfig) ，因为如果忘记编写super.init(config);而还是用了ServletConfig接口的方法，
则会出现空指针异常。

⑤.新建的init() 并非Servlet 的生命周期方法。而init(ServletConfig) 是生命周期相关的方法。

##  HttpServlet:
   
1、是一个Servlet,继承自GenericServlet。针对于HTTP协议所定制。

2、在service()方法中直接把ServletRequest和ServletResponse 转为HttpServletRequest和HttpServletResponse。并调用了重载的service
(HttpServletRequest, HttpServletResponse)。

在service(HttpServletRequest, HttpServletResponse)获取了请求方式: request.getMethod()。
根据请求方式有创建了doXxx()方法(xxx为具体的请求方式比如doGet, doPost)。


## Servlet组件

Servlet

Filter

Listener

## Filter

Authentication filters 

Logging and auditing filters

Image conversion filters

Data compression filters

Encryption filters

Tokenizing filters

Filters that trigger resource access events

XSL/T filters that transform XML content
 
MIME-type chain filters
 
Caching filters

## JSP

为了弥补Servlet的缺陷, SUN公司在Servlet的基础上推出了JSP( Java Server Pages )技术作为解决方案。
   
JSP是简化Servlet编写的一种技术,它将Java代码和HTML语句混合在同一个文件中编写,只对网页中的要动态产生的内容采用Java代码来编写，
而对固定不变的静态内容采用普通静态HTML页面的方式编写。


JSP 在SpringBoot 只能war包执行




