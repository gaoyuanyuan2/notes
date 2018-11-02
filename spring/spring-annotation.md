# Spring 注解详解
## @Scope:调整作用域
 * prototype：多实例的：ioc容器启动并不会去调用方法创建对象放在容器中。
 * 					每次获取的时候才会调用方法创建对象；
 * singleton：单实例的（默认值）：ioc容器启动会调用方法创建对象放到ioc容器中。
 * 			以后每次获取就是直接从容器（map.get()）中拿，
 * request：同一次请求创建一个实例
 * session：同一个session创建一个实例

 * 懒加载：
 * 		单实例bean：默认在容器启动的时候创建对象；
 * 		懒加载：容器启动不创建对象。第一次使用(获取)Bean创建对象，并初始化；
## @Conditional({Condition}) ： 按照一定的条件进行判断，满足条件给容器中注册bean
## @Controller @Service @Repository @Component
 * 1）、包扫描+组件标注注解（@Controller/@Service/@Repository/@Component）[自己写的类]
 * 2）、@Bean[导入的第三方包里面的组件]
 * 3）、@Import[快速给容器中导入一个组件]
 * 		1）、@Import(要导入到容器中的组件)；容器中就会自动注册这个组件，id默认是全类名
 * 		2）、ImportSelector:返回需要导入的组件的全类名数组；
 * 		3）、ImportBeanDefinitionRegistrar:手动注册bean到容器中
 * 4）、使用Spring提供的 FactoryBean（工厂Bean）;
 * 		1）、默认获取到的是工厂bean调用getObject创建的对象
 * 		2）、要获取工厂Bean本身，我们需要给id前面加一个&
 * 			&colorFactoryBean
 ## @ComponentScan  value:指定要扫描的包
 * @Filter(type=FilterType.CUSTOM,classes={MyTypeFilter.class})
 ```java
public class MyTypeFilter implements TypeFilter {
	/**
	 * metadataReader：读取到的当前正在扫描的类的信息
	 * metadataReaderFactory:可以获取到其他任何类信息的
	 */
	@Override
	public boolean match(MetadataReader metadataReader, MetadataReaderFactory metadataReaderFactory)
			throws IOException {
		//获取当前类注解的信息
		AnnotationMetadata annotationMetadata = metadataReader.getAnnotationMetadata();
		//获取当前正在扫描的类的类信息
		ClassMetadata classMetadata = metadataReader.getClassMetadata();
		//获取当前类资源（类的路径）
		Resource resource = metadataReader.getResource();
		String className = classMetadata.getClassName();
		System.out.println("--->"+className);
		if(className.contains("er")){
			return true;
		}
		return false;
	}
}
 ```
## 自动装配;
* 		Spring利用依赖注入（DI），完成对IOC容器中中各个组件的依赖关系赋值；
*
* 1）、@Autowired：自动注入：
* 		1）、默认优先按照类型去容器中找对应的组件:applicationContext.getBean(BookDao.class);找到就赋值
* 		2）、如果找到多个相同类型的组件，再将属性的名称作为组件的id去容器中查找
* 							applicationContext.getBean("bookDao")
* 		3）、@Qualifier("bookDao")：使用@Qualifier指定需要装配的组件的id，而不是使用属性名
* 		4）、自动装配默认一定要将属性赋值好，没有就会报错；
* 			可以使用@Autowired(required=false);
* 		5）、@Primary：让Spring进行自动装配的时候，默认使用首选的bean；
* 				也可以继续使用@Qualifier指定需要装配的bean的名字
```java
 		BookService{
 			@Autowired
			BookDao  bookDao;
		}
```
* 2）、Spring还支持使用@Resource(JSR250)和@Inject(JSR330)[java规范的注解]
* 		@Resource:
* 			可以和@Autowired一样实现自动装配功能；默认是按照组件名称进行装配的；
* 			没有能支持@Primary功能没有支持@Autowired（reqiured=false）;
* 		@Inject:
* 			需要导入javax.inject的包，和Autowired的功能一样。没有required=false的功能；
*  @Autowired:Spring定义的； @Resource、@Inject都是java规范
*
* AutowiredAnnotationBeanPostProcessor:解析完成自动装配功能；

* 3）、 @Autowired:构造器，参数，方法，属性；都是从容器中获取参数组件的值
* 		1）、[标注在方法位置]：@Bean+方法参数；参数从容器中获取;默认不写@Autowired效果是一样的；都能自动装配
* 		2）、[标在构造器上]：如果组件只有一个有参构造器，这个有参构造器的@Autowired可以省略，参数位置的组件还是可以自动从容器中获取
* 		3）、放在参数位置：

* 4）、自定义组件想要使用Spring容器底层的一些组件（ApplicationContext，BeanFactory，xxx）；
* 		自定义组件实现xxxAware；在创建对象的时候，会调用接口规定的方法注入相关组件；Aware；
* 		把Spring底层一些组件注入到自定义的Bean中；
* 		xxxAware：功能使用xxxProcessor；
* 			ApplicationContextAware==》ApplicationContextAwareProcessor；

