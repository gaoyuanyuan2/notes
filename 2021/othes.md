## 随笔记

* 二分任务,最后聚合
比如扩展RecursiveAction实现

* 找get set 方法，推荐使用`java.beans.BeanInfo`
软引用节约内存，提升性能

* BeanFactory BeanDefinitionRegistry => DefaultListableBeanFactory
getBean()引起Spring Bean容器过早的初始化

* Aware 被动，依赖注入，@Autowired 主动，依赖查找

* 工具类
Utility Classes通常采用抽象实现，《Effective Java》，目前是让其不要实例化。
Thymeleaf StringUtils是final,需要实例化。
context.put("strings",new StringUtil());
Velocity Tools需要实例化，但是context支持静态方法的调用。|

* 我想问一下，想拦截SQL执行前的SQL和SQL执行后的SQL保存到数据库,有什么思路?
AOP JdbcTemplate.
MyBatis Interceptor
JPA @PrePersist

* 我想获取HttpServletResponse中content的内容， 是不是只能通过HttpServletResponseWrapper这个接口呢，如果使用这个接口有什么需要注意的呢?
HttpServletResponseWrapper 使用Servlet技术Filter#doFilter.
content本文内容、二进制内容:
javax.servlet.ServletResponse#getWriter()
javax.servlet.ServletResponse#getOutputStream()
不能同时使用，否则IllegalStateException
Filter -> Filter -> Filter -> Servlet -> Filter -> Servlet
web.xml先URI匹配，如果相同按照定义顺序。
Spring Boot自动装配。

* 注意点二:状态判断是否commit,是否响应终止操作。
if(javax.servlet.ServletResponse#isCommitted()) {
// DO NOTHING
}
如果使用Spring Web,可以选择这个API ContentCachingResponseWrapper,这个
类出现在4.1.3以及更高，Spring Boot 1.1+.

*  spring里ObjectFactory和factoryBean有什么区别?在使用时该注意什么?
FactoryBean是一种BeanFactory SPI , 与ObjectFactory类似,获取单体或者原型对象不
过FactoryBean能够制定Bean的类型,而ObjectFactory则不行。ObjectFactory 更像是一个
在BeanFactory通过Bean名称关联的对象,在运行时确定getObject()方法返回的内容,也
就是所它不具备强类型。
ObjectFactory是一种延迟加载Bean策略或工厂。

* maven 写在前面先生效

* JSP 方法内联，空间换时间。