# Maven

## 命令

* mvn dependency:tree >d.txt  输出依赖树

* mvn clean package -U 强制拉一次

## scope

* compile编译例 如spring-core

* test测试

* provided编译例如servlet

* runtime运行时例如JDBC驱动实现

* system本地一些jar例如短信jar


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


