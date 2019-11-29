# Mybatis

MyBatis 是一款优秀的持久层框架，它支持定制化 SQL、存储过程以及高级映射。

MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。

MyBatis 可以使用简单的 XML 或注解来配置和映射原生类型、接口和 Java 的 POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。
## 1、 SqlSession

 SqlSession的实例不是线程安全的,因此是不能被共享的。
 
 SqlSession每次使用完成后需要正确关闭,这个关闭操作是必须的
 
## 2、 自增主键

MySql 支持自增主键，自增主键值的获取，mybatis 也是利用statement.getGenreatedKeys();
 
useGeneratedKeys="true";使用自增主键获取王键值策略

keyProperty;指定对应的主键属性，也就是mybatis获取到主键值以后，将这个值封装给javaBean的哪个属性 

```Html
<insert id="addEmp" parameterType="com.bean.Employee" useGeneratedKeys="true" keyProperty="id" databaseId= "mysq1">
    insert into employee (last_ name , email , gender)values (#{lastName} ,# {email} , # {gender})
</insert>
```

特殊的代理

```java 
protected T newInstance(MapperProxy<T> mapperProxy) {
    return (T) Proxy.newProxyInstance(mapperInterface.getClassLoader(), new Class[] { mapperInterface }, mapperProxy);
}
```      

代理类：获取sql 执行结果 映射值
      
