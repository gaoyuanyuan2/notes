# Maven （Java 写的）

*约定优于配置*

## 命令

* mvn dependency:tree >d.txt  输出依赖树

* mvn clean package -U 强制拉一次

* mvn -P test

## scope

* system本地一些jar例如短信jar

* test范围是指测试范围有效,在编译和打包时都不会使用这个依赖

* compile范围是指编译范围内有效,在编译和打包时都会将依赖存储进去

* provided依赖,在编译和测试过程中有效,最后生成的war包时不会加入 

例如:servlet-api,因为servlet-api  tomcat服务器已经存在了,如果再打包会冲突

* runtime在运行时候依赖,在编译时候不依赖 默认依赖范围是compile


## exclusion 解决冲突
```xml
<dependency>
  <groupId>sample.ProjectA</groupId>
  <artifactId>Project-A</artifactId>
  <version>1.0</version>
  <scope>compile</scope>
  <exclusions>
    <exclusion> 
      <groupId>javax.servlet</groupId>
      <artifactId>servlet-api</artifactId>
    </exclusion>
  </exclusions> 
</dependency>
```

## Maven阶段

![生命周期](/img/32.png) 

* validate：验证项目是否正确并且所有必要信息都可用

* compile 

* test: 使用合适的单元测试框架测试编译的源代码。这些测试不应要求打包或部署代码

* package: take the compiled code and package it in its distributable format, such as a JAR.

* integration-test:如有必要，将程序包处理并部署到可以运行集成测试的环境中

* verify: 运行任何检查以验证包是否有效并符合质量标准

* install: 将软件包安装到本地存储库中，以便在本地用作其他项目的依赖项

* deploy: 在集成或发布环境中完成，将最终包复制到远程存储库以与其他开发人员和项目共享。

* clean: cleans up artifacts created by prior builds

* site: 为该项目生成站点文档


1. A Build Lifecycle is Made Up of Phases  构建生命周期由阶段组成

2. A Build Phase is Made Up of Plugin Goals 构建阶段由插件目标组成

Release:该版本表示最终版，不能被强制覆盖。



* archetype 项目模板

* 优先级 ~/.m2/setting.xml  -> conf/setting.xml

* dependencyManagement 只出现在父pom，统一版本号，声明

* type 默认java

* score 默认 compile;test 测试期间用到；provided 编译 不会打包 eg：tomcat 有servlet 相关包；

* runtime 运行时，打包，接口编程，JDBC接口；system 本地包

* 传递依赖 

* 父pom （公司级别、部门级别）

* 依赖就近原则 ，加载先后原则（书写顺序）




eg:
```xml
<dependency>
    <groupId>org.apache.tomcat</groupId>
    <artifactId>tomcat-servlet-api</artifactId>
    <version>9.0.19</version>
    <scope>provided</scppe>
</dependency>

<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.15</version>
    <scope>runtime</scope>
</dependency>

<dependency>
    <groupId>com.gaoyuanyaun.yan</groupId>
    <artifactId>common-lib</artifactId>
    <version>1.0</version>
    <scope>system</scope>
    <systemPath>D:\common-lib.jar</systemPath>
</dependency>

```
## 常用镜像

```xml
<mirrors>
    <mirror>
      <id>alimaven</id>
      <name>aliyun maven</name>
      <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
      <mirrorOf>central</mirrorOf>        
    </mirror>
    <mirror>
      <id>ui</id>
      <mirrorOf>central</mirrorOf>
      <name>Human Readable Name for this Mirror.</name>
     <url>http://uk.maven.org/maven2/</url>
    </mirror>
    <mirror>
		<id>osc</id>
		<mirrorOf>central</mirrorOf>
		<url>http://maven.oschina.net/content/groups/public/</url>
	</mirror>
	 <mirror>
        <id>osc_thirdparty</id>
        <mirrorOf>thirdparty</mirrorOf>
        <url>http://maven.oschina.net/content/repositories/thirdparty/</url>
    </mirror>
</mirrors>

```

## maven统一修改项目版本号

使用插件完成版本号的修改，不需要一个个去修改

在父级pom文件中，加入versions插件配置，然后在linux或IntelliJ IDEA中执行修改版本号的命令

### versions插件配置

```xml
<build>
    <plugins>
        <plugin>
            <!-- https://mvnrepository.com/artifact/org.codehaus.mojo/versions-maven-plugin -->
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>versions-maven-plugin</artifactId>
            <version>2.7</version>
        </plugin>
    </plugins>
</build>
```
### 修改版本号命令

*mvn versions:set -DnewVersion=1.1-SANPSHOT*

## Plugin

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-dependency-plugin</artifactId>
    <version>2.10</version>
    <executions>
        <execution>
            <id>copy-dependencies</id> 
            <phase>package</phase>  //执行时机
            <goals>
                <goal>copy-dependencies</goal> //执行目标
            </goals>
            <configuration>
                <outputDirectory>${project.build.directory}/lib</outputDirectory>
            </configuration>
        </execution>
    </executions>
</plugin>
```

指定版本，就不用设置项目结构了

```xml
        <plugins>
            <plugin>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>2.5.1</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
        </plugins>
```


下载源码


mvn dependency:sources
