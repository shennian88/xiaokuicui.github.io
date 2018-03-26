---
layout: post
title: Spring Boot学习笔记(1)|入门
categories: Spring
description: Spring Boot学习笔记
keywords: Spring,Spring Boot
---

## Spring Boot简介

​	 Spring Boot简化了基于Spring应用的初始搭建及开发过程,其充分利用了JavaConfig 的配置模式以及“约定优于配置”的理念,能够极大的简化基于 Spring MVC 的 Web 应用和 REST 服务开发。用我的话来理解,就是Spring Boot其实不是什么新的框架，它默认配置了很多框架的使用方式，就像maven整合了所有的jar包，Spring Boot整合了所有的框架。可参考[spring-boot-dependencies.pom](https://github.com/spring-projects/spring-boot/blob/v2.0.0.RELEASE/spring-boot-project/spring-boot-dependencies/pom.xml)来获取整合的第三方框架及各框架版本。

## 快速上手

1.  通过``SPRING INITIALIZR``生成基本项目

    (1). 访问 http://start.spring.io/

    (2). 选择构建工具、spring boot版本及一些工程基本信息,点击"Switch to the full version."可选择Java版本,可参考下图所示:
      ![](https://raw.githubusercontent.com/xiaokuicui/xiaokuicui.github.io/master/assets/images/spring-boot/springboot-init.jpg)

    (3). 点击Generate Project下载项目压缩包。

2.  解压压缩包,并用IDEA以Maven项目导入

     ​	Spring Boot依赖关系使用组``org.springframework.boot``,Maven Pom文件继承``spring-boot-starter-parent``项目。如以下pom清单:

     ```
     <?xml version="1.0" encoding="UTF-8"?>
     <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
     	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
     	<modelVersion>4.0.0</modelVersion>

     	<groupId>com.example</groupId>
     	<artifactId>myproject</artifactId>
     	<version>0.0.1-SNAPSHOT</version>

     	<!-- 引入spring-boot-starter-parent父项目 -->
     	<parent>
     		<groupId>org.springframework.boot</groupId>
     		<artifactId>spring-boot-starter-parent</artifactId>
     		<version>2.0.0.RELEASE</version>
     	</parent>

     	<properties>
     		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
     		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
     		<!-- 覆盖父pom定义的变量 -->
     		<java.version>1.8</java.version>
     	</properties>

     	<!-- 添加spring-boot-starter-web依赖关系,标明正在开发web应用程序 -->
     	<dependencies>
     		<dependency>
     			<groupId>org.springframework.boot</groupId>
     			<artifactId>spring-boot-starter-web</artifactId>
     		</dependency>
     	</dependencies>

     	<!-- 可以将项目打包为可执行的Jar,方便随时随地的运行应用程序,Maven版本必须高于3.2-->
     	<build>
     		<plugins>
     			<plugin>
     				<groupId>org.springframework.boot</groupId>
     				<artifactId>spring-boot-maven-plugin</artifactId>
     			</plugin>
     		</plugins>
     	</build>

     </project>
     ```
## 项目结构介绍

![](https://raw.githubusercontent.com/xiaokuicui/xiaokuicui.github.io/master/assets/images/spring-boot/springboot-%E9%A1%B9%E7%9B%AE%E6%9C%BA%E6%9E%84.jpg)

如上图所示,Spring Boot的基础结构共三个文件:

- src/main/java 程序开发以及主程序入口
- src/main/resources 配置文件
- src/test/java 测试程序

spingboot建议的目录结果如下：

```
com
  +- example
    +- myproject
      +- Application.java
      |
      +- domain
      |  +- Customer.java
      |  +- CustomerRepository.java
      |
      +- service
      |  +- CustomerService.java
      |
      +- web
      |  +- CustomerController.java
      |
```

root package结构：`com.example.myproject`

* Application.java 建议放到根目录下面,主要用于做一些框架配置
* domain目录主要用于实体（Entity）与数据访问层（Repository）
* service 层主要是业务类代码
* web负责页面访问控制

## 编写HelloWorld服务

1. 添加支持web的依赖

   ```
   <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-web</artifactId>
   </dependency>
   ```

2. 编写HelloWorldController内容:

   ```java
   @RestController
   public class HelloWorldController {

       @RequestMapping(value = "/hello", method = RequestMethod.GET)
       public String helloWorld() {
           return "Hello World";
       }

   }
   ```

   标注``@RestController``注解的类不用再使用@Responsebody,也不用在写什么jackjson配置了！

3. 启动Application主类运行应用程序,访问http://localhost:8080/hello就可以看到效果了。

   ![](https://raw.githubusercontent.com/xiaokuicui/xiaokuicui.github.io/master/assets/images/spring-boot/springboot-Application.jpg)

   ``@SpringBootApplication``注解相当于使用``@Configuration @EnableAutoConfiguration @ComponentScan``与他们的默认属性。

## 单元测试



​    [示例代码](https://github.com/xiaokuicui/spring-boot-cloud-learning-examples)

## Spring Boot Starter介绍

|名称|描述|
| ---------------------------- | ------------------------------- |
| spring-boot-starter          | 核心入门,包括自动配置支持,日志记录和YAML  |
| spring-boot-starter-activemq | 使用Apache ActiveMQ启动JMS消息传递      |
| spring-boot-starter-amqp     | 使用Spring AMQP和Rabbit MQ    |
| spring-boot-starter-aop      | 使用Spring AOP和AspectJ进行面向方面编程 |
| spring-boot-starter-artemis  | 使用Apache Artemis启动JMS消息传递       |
| spring-boot-starter-batch    | 使用Spring Batch|
| spring-boot-starter-cache    | Spring Framework的缓存支持|
|spring-boot-starter-cloud-connectors|Starter使用Spring Cloud Connectors，可简化Cloud Foundry和Heroku等云平台中的服务连接|
|spring-boot-starter-data-cassandra|  使用Cassandra分布式数据库和Spring Data Cassandra|
|spring-boot-starter-data-cassandra-reactive|使用Cassandra分布式数据库和Spring Data Cassandra Reactive的初学者|
|spring-boot-starter-data-couchbase|使用Couchbase面向文档的数据库和Spring Data Couchbase的初学者|
|spring-boot-starter-data-couchbase-reactive|使用Couchbase面向文档的数据库和Spring Data Couchbase Reactive的初学者|
|spring-boot-starter-data-elasticsearch|使用Elasticsearch搜索和分析引擎和Spring Data Elasticsearch|
|spring-boot-starter-data-jpa|使用Spring数据JPA和Hibernate|
|spring-boot-starter-data-ldap|使用Spring Data LDAP|
|spring-boot-starter-data-mongodb|使用MongoDB面向文档的数据库和Spring Data MongoDB Reactive|
|spring-boot-starter-data-neo4j|使用Neo4j图形数据库和Spring Data Neo4j|
|spring-boot-starter-data-redis|使用Spring Data Redis和Lettuce客户端使用Redis键值数据存储|
|spring-boot-starter-data-redis-reactive|使用Redis键值数据存储以及Spring Data Redis反应器和Lettuce客户端|
|spring-boot-starter-data-rest|使用Spring Data REST通过REST公开Spring Data存储库|
|spring-boot-starter-data-solr|启动Spring Data Solr使用Apache Solr搜索平台|
|spring-boot-starter-freemarker|使用FreeMarker视图构建MVC Web应用程序|
|spring-boot-starter-groovy-templates|使用Groovy模板视图构建MVC Web应用程序|
|spring-boot-starter-hateoas|使用Spring MVC和Spring HATEOAS构建基于超媒体的RESTful Web应用程序|
|spring-boot-starter-integration|使用Spring Integration|
|spring-boot-starter-jdbc|将JDBC与Tomcat JDBC连接池配合使用|
|spring-boot-starter-jersey|使用JAX-RS和Jersey构建RESTful Web应用程序的入门者。替代方案spring-boot-starter-web|
|spring-boot-starter-jooq|使用jOOQ访问SQL数据库的入门者。替代spring-boot-starter-data-jpa或spring-boot-starter-jdbc|
|spring-boot-starter-json|用于阅读和编写json|
|spring-boot-starter-jta-atomikos|使用Atomikos启动JTA|
|spring-boot-starter-jta-bitronix|使用Bitronix启动JTA|
|spring-boot-starter-jta-narayana|启动Narayana JTA|
|spring-boot-starter-mail|使用Java Mail和Spring Framework的电子邮件发送|
|spring-boot-starter-mustache|使用Mustache视图构建Web应用程序|
|spring-boot-starter-quartz|使用quartz定时任务|
|spring-boot-starter-security|使用Spring Security|
|spring-boot-starter-test|用于测试包含JUnit，Hamcrest和Mockito等库的Spring Boot应用程序|
|spring-boot-starter-thymeleaf|使用Thymeleaf视图构建MVC Web应用程序|
|spring-boot-starter-validation|通过Hibernate Validator使用Java Bean验证|
|spring-boot-starter-web|使用Spring MVC构建Web，包括RESTful应用程序。使用Tomcat作为默认的嵌入容器|
|spring-boot-starter-web-services|使用Spring Web Services|
|spring-boot-starter-webflux|使用Spring Framework的Reactive Web支持构建WebFlux应用程序|
|spring-boot-starter-websocket|使用Spring Framework的WebSocket支持构建WebSocket应用程序|
|spring-boot-starter-actuator|可帮助您监控和管理您的应用程序|
|spring-boot-starter-jetty|将Jetty用作嵌入式servlet容器的入门者。替代方案spring-boot-starter-tomcat|
|spring-boot-starter-log4j2|使用Log4j2进行日志记录。替代方案spring-boot-starter-logging|
|spring-boot-starter-logging|使用Logback进行日志记录。默认日志启动器|
|spring-boot-starter-reactor-netty|使用Reactor Netty作为嵌入式反应式HTTP服务器|
|spring-boot-starter-tomcat|使用Tomcat作为嵌入式servlet容器的入门。默认使用的servlet容器启动器spring-boot-starter-web|
|spring-boot-starter-undertow|使用Undertow作为嵌入式servlet容器的入门者。替代方案spring-boot-starter-tomcat|

## 参考博客

   - [程序猿DD](http://blog.didispace.com/categories/Spring-Boot/)
   - [纯洁的微笑](http://www.ityouknow.com/spring-boot.html)
