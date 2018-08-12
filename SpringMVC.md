## SpringMVC
![运行流程](https://github.com/gaoyuanyuan2/notes/blob/master/img/2.png) 
### 1、过滤器、拦截器
 1.过滤器Filter依赖于Servlet容器,基于回调函数,过滤范围大
  <br><br>拦截器Interceptor依赖于框架容器,基于反射机制,只过滤请求（收费站）
   <br><br>2.自定义拦截器：implements HandlerInterceptor
  <br>拦截器的方法介绍
  <br>1)preHandle方法,在请求被处理之前进行调用
  <br>2)postHandle方法,在请求被处理之后进行调用
  <br>3)afterCompletion方法 ,在请求结束之后才进行调用
  <br><br>3.拦截器的使用场景
  <br>使用原则:处理所有请求的共同问题
  <br>1)解决乱码问题
  <br>2)解决权限验证问题

