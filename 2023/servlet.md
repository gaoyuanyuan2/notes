# Servlet 

## 传统 Servlet


## Servlet on Spring Boot


### Servlet 3.0 前时代

* 事件（since Servlet 2.3 ）
  * 生命周期类型
  * javax.servlet.ServletContextEvent
    * javax.servlet.http.HttpSessionEvent
    * java.servlet.ServletRequestEvent

  * 属性上下文类型
    * javax.servlet.ServletContextAttributeEvent
    * javax.servlet.http.HttpSessionBindingEvent
    * javax.servlet.ServletRequestAttributeEvent
    
### Servlet 3.0 后时代

* 组件申明注解
  * @javax.servlet.annotation.WebServlet
  * @javax.servlet.annotation.WebFilter
  * @javax.servlet.annotation.WebListener
  * @javax.servlet.annotation.ServletSecurity
  * @javax.servlet.annotation.HttpMethodConstraint
  * @javax.servlet.annotation.HttpConstraint

* 配置申明
  * @javax.servlet.annotation.WebInitParam

* 上下文
  * javax.servlet.AsyncContext

* 事件
  * javax.servlet.AsyncEvent

* 监听器
  * javax.servlet.AsyncListener

* Servlet 组件注册
  * javax.servlet.ServletContext#addServlet()
  * javax.servlet.ServletRegistration

* Filter 组件注册
  * javax.servlet.ServletContext#addFilter()
  * javax.servlet.FilterRegistration

* 监听器注册
  * javax.servlet.ServletContext#addListener()
  * javax.servlet.AsyncListener

* 自动装配
  * 初始器
    * javax.servlet.ServletContainerInitializer

  * 类型过滤
    * @javax.servlet.annotation.HandlesTypes

### Servlet 生命周期

* 初始化
当容器启动或者第一次执行时，Servlet#init(ServletConfig)方法被执行，初始化当前Servlet 。

* 处理请求
当HTTP 请求到达容器时，Servlet#service(ServletRequest,ServletResponse) 方法被执行，来处理请求。

* 销毁
当容器关闭时，容器将会调用Servlet#destroy 方法被执行，销毁当前Servlet。


### Filter 生命周期

* 初始化
当容器启动时，Filter#init(FilterConfig)方法被执行，初始化当前Filter。

* 处理请求
当HTTP 请求到达容器时，Filter#doFilter(ServletRequest,ServletResponse,FilterChain) 方法被执行，来拦截请求，在Servlet#service(ServletRequest,ServletResponse) 方法调用前执行。

* 销毁
当容器关闭时，容器将会调用Filter#destroy 方法被执行，销毁当前Filter。


### Servlet 组件扫描

* @org.springframework.boot.web.servlet.ServletComponentScan 
  * 指定包路径扫描
    * String[] value() default {}
    * String[] basePackages() default {}
  * 指定类扫描
    * Class<?>[] basePackageClasses() default {}

### 注解方式注册

### Servlet 组件

* 扩展 javax.servlet.Servlet
  * javax.servlet.http.HttpServlet
  * org.springframework.web.servlet.FrameworkServlet


* 标记 @javax.servlet.annotation.WebServlet


### Filter 组件

* 实现 javax.servlet.Filter
  * org.springframework.web.filter.OncePerRequestFilter


* 标记 @javax.servlet.annotation.WebFilter

### 监听器组件

* 实现Listener接口
  * javax.servlet.ServletContextListener
  * javax.servlet.http.HttpSessionListener
  * javax.servlet.http.HttpSessionActivationListener
  * javax.servlet.ServletRequestListener
  * javax.servlet.ServletContextAttributeListener
  * javax.servlet.http.HttpSessionAttributeListener
  * javax.servlet.http.HttpSessionBindingListener
  * javax.servlet.ServletRequestAttributeListener
  
* 标记 @javax.servlet.annotation.WebListener

### Spring Boot API方式注册

### Servlet 组件

* 扩展 javax.servlet.Servlet
  * javax.servlet.http.HttpServlet
  * org.springframework.web.servlet.FrameworkServlet

* 组装 Servlet
  * Spring Boot 1.4.0 开始支持
    * org.springframework.boot.web.servlet.ServletRegistrationBean
  * Spring Boot 1.4.0 之前
    * org.springframework.boot.context.embedded.ServletRegistrationBean
  
* 暴露 Spring Bean
  * @Bean



### Filter 组件

* 实现 javax.servlet.Filter
  * org.springframework.web.filter.OncePerRequestFilter

* 组装 Filter
  * Spring Boot 1.4.0 开始
    * org.springframework.boot.web.servlet.FilterRegistrationBean
  * Spring Boot  1.4.0 之前
    * org.springframework.boot.context.embedded.FilterRegistrationBean
    
* 暴露 Spring Bean
  * @Bean

### 监听器组件

* 实现 Listener

* 组装 Listener
  * Spring Boot 1.4.0 开始
    * org.springframework.boot.web.servlet.ServletListenerRegistrationBean
  * Spring Boot 1.4.0 之前
    * org.springframework.boot.context.embedded.ServletListenerRegistrationBean

* 暴露 Spring Bean
  * @Bean


## JSP on Spring Boot

### 激活

* 激活 传统Servlet Web部署
    * Spring Boot 1.4.0 开始
      * org.springframework.boot.web.support.SpringBootServletInitializer

* 组装 org.springframework.boot.builder.SpringApplicationBuilder

* 配置JSP视图
  * org.springframework.boot.autoconfigure.web.WebMvcProperties
    * spring.mvc.view.prefix
    * spring.mvc.view.suffix

