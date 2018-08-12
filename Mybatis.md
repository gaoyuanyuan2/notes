## Mybatis
### 1、 SqlSession
        SqlSession的实例不是线程安全的,因此是不能被共享的。
       <br> SqlSession每次使用完成后需要正确关闭,这个关闭操作是必须的
### 2、 自增主键
        mysq1支持自增主键，自增主键值的获取，mybatis 也是利用statement.getGenreatedKeys();
       <br> useGeneratedKeys="true";使用自增主键获取王键值策略
        keyProperty;指定对应的主键属性，也就是mybatis获取到主键值以后，将这个值封装给javaBean的哪个属性
        ```xml
        <insert id="addEmp" parameterType="com.bean.Employee" useGeneratedKeys="true" keyProperty="id' databaseId= "mysq1">
            insert into employee (last_ name , email , gender)values (#{lastName} ,# {email} , # {gender})
        </insert>
         ```
      

      
