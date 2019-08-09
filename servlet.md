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

![Servlet](https://github.com/gaoyuanyuan2/notes/blob/master/img/44.png) 

Servlet是一种基于Java技术的Web组件，用于生成动态内容，由容器管理。类似于其他Java技术组件，Servlet 是平台无关的Java类组成，并且由JavaWeb服务器加载执行。
通常情况，由Servlet容器提供运行时环境。Servlet 容器，有时候也称作为Servlet引擎，作为Web服务器或应用服务器的一部分。
通过请求和响应对话，提供Web客户端与Servlets交互的能力。容器管理Servlets实例以及它们的生命周期。


从功能上，Servlet 介于CGI ( Common Gateway Interface)与服务扩展(如: Netscape Server API或Apache模块)之间。

在体系上，Servlet 技术( 或者规范)属于JavaEE技术(规范)的一部分。不过Servlet并非一开始就隶属于J2EE或者JavaEE。


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


