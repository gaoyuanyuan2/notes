## SpringMVC
![运行流程](https://github.com/gaoyuanyuan2/notes/blob/master/img/2.png) 
### 1、过滤器、拦截器
 <br>1. 过滤器Filter依赖于Servlet容器,基于回调函数,过滤范围大
  <br><br>拦截器Interceptor依赖于框架容器,基于反射机制,只过滤请求（收费站）
   <br><br>2.自定义拦截器：implements HandlerInterceptor
  <br>拦截器的方法介绍
  <br>1)preHandle方法,在请求被处理之前进行调用
  <br>2)postHandle方法,在请求被处理之后进行调用
  <br>3)afterCompletion方法 ,在请求结束之后才进行调用
<br><br>2. Interceptor
<br><br>1)主要作用：拦截用户请求，进行处理，比如判断用户登录情况，权限验证，主要针对Action请求进行处理。是通过HandlerInterceptor 实现的。
```Xml
<mvc:interceptors>
    <bean class="cn.appsys.testInterceptor"></bean>//拦截所有请求
    <mvc:interceptor>
        <mvc:mapping path="/manager/backend/**"/>
        <bean class="cn.appsys.interceptor.SysInterceptor"/>//拦截上面请求
    </mvc:interceptor>  
</mvc:interceptors>
```
<br><br>2)一般拦截器可通过实现HandlerInterceptor接口或者继承HandlerInterceptorAdapter实现。代码如下：
```Java
public class TestInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse,
     Object o) throws Exception {
        System.out.println("preHandle");
        return true;
    }

    @Override
    public void postHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse,
     Object o, ModelAndView modelAndView) throws Exception {
        System.out.println("postHandle");
    }

    @Override
    public void afterCompletion(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, 
    Object o, Exception e) throws Exception {
        System.out.println("afterCompletion");
    }
}
```
<br><br>3)注：只能对Controller请求进行拦截，对一些静态资源无法拦截。  
<br><br>3.Filter
<br><br>1)主要作用：统一设置字符集等。
 依赖于servlet容器，过滤器实例只在初始化的时候调用一次。
<br><br>2)过滤器在web.xml配置如下：
 ```Xml
<filter>
     <filter-name>testFilter</filter-name>
     <filter-class>cn.appsys.TestFilter</filter-class>
 </filter>
 <filter-mapping>
     <filter-name>testFilter</filter-name>
     <url-pattern>/*</url-pattern>
 </filter-mapping>    
```
<br><br>3) 一般过滤器可通过实现Filter接口实现。代码如下：
```Java
 public class TestFilter implements Filter {
 
     @Override
     public void destroy() {
         System.out.println("filter destroy");
     }
 
     @Override
     public void doFilter(ServletRequest arg0, ServletResponse arg1, FilterChain arg2)
             throws IOException, ServletException {
         System.out.println("filter doFilter before");
         arg2.doFilter(arg0, arg1);
         System.out.println("filter doFilter after");
 
     }
 
     @Override
     public void init(FilterConfig arg0) throws ServletException {
         System.out.println("filter init");
     }
 
 }
```
<br><br>4. 拦截器和过滤器执行顺序：
<br>1)Filter.init();
<br>2)Filter.doFilter(); before doFilter
<br>3)HandlerInterceptor.preHandle();
<br>4)Controller方法执行
<br>5)HandlerInterceptor.postHandle();
<br>6)DispatcherServlet视图渲染
<br>7)HandlerInterceptor.afterCompletion();
<br>8)Filter.doFilter(); after doFilter
<br>9)Filter.destroy();
         
<br><br>5.  Filter和Interceptor的区别
<br>1)Filter是基于函数回调（doFilter()方法）的，而Interceptor则是基于Java反射的（AOP思想）。
<br>2) Filter依赖于Servlet容器，而Interceptor不依赖于Servlet容器。
<br>3)Filter对几乎所有的请求起作用，而Interceptor只能对action请求起作用。
<br>4)Interceptor可以访问Action的上下文，值栈里的对象，而Filter不能。
<br>5)在action的生命周期里，Interceptor可以被多次调用，而Filter只能在容器初始化时调用一次。

<br><br>6.  SpringMVC

<br>1、web容器在启动的时候，会扫描每个jar包下的META-INF/services/javax.servlet.ServletContainerInitializer

<br>2、加载这个文件指定的类SpringServletContainerInitializer

<br>3、spring的应用一启动会加载感兴趣的WebApplicationInitializer接口的下的所有组件；

<br>4、并且为WebApplicationInitializer组件创建对象（组件不是接口，不是抽象类）

<br>	1）、AbstractContextLoaderInitializer：创建根容器；createRootApplicationContext()；
	
<br>	2）、AbstractDispatcherServletInitializer：
	
			创建一个web的ioc容器；createServletApplicationContext();
			
			创建了DispatcherServlet；createDispatcherServlet()；
			
			将创建的DispatcherServlet添加到ServletContext中；
			
				getServletMappings();
				
<br>	3）、AbstractAnnotationConfigDispatcherServletInitializer：注解方式配置的DispatcherServlet初始化器
	
			创建根容器：createRootApplicationContext()
			
					getRootConfigClasses();传入一个配置类
					
			创建web的ioc容器： createServletApplicationContext();
			
					获取配置类；getServletConfigClasses();
	
总结：

	以注解方式来启动SpringMVC；继承AbstractAnnotationConfigDispatcherServletInitializer；
	
实现抽象方法指定DispatcherServlet的配置信息；

定制SpringMVC；

1）、@EnableWebMvc:开启SpringMVC定制配置功能；

	<mvc:annotation-driven/>；

2）、配置组件（视图解析器、视图映射、静态资源映射、拦截器。。。）

	extends WebMvcConfigurerAdapter



