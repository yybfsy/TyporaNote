# Dubbo



## 前言



一、 什么是分布式框架 
分布式系统是若干独立系统的集合,但是用户使用起来像是在使用一套系统 

二、 为什么需要分布式系统? 
规模的逐步扩大和业务的复杂，单台计算机扛不住双十一那样的流量

三、 应用架构的发展演变 
（1） 单一架构
当网站流量很小的时候,我们将所有的应用(业务)放到一台服务器上,打包运行公司管理系统/超市收银系统 
优点:开发简单,部署简单 
缺点:扩展不容易(怎么处理日益增长的流量),谁都改一个,维护不容易,性能提升难 
2） 垂直应用架构
将大应用拆分成为小应用(一般按照业务拆分),根据不同的访问频率决定各自业务部署的服务器数量 
优点:扩展容易 
缺点:页面一改,可能造成整个项目重新部署,业务和界面没有分离开,随着业务种类增加,怎么解决业务之间的互相调用问题,订单服务器和用户服务器交互效率的问题
（3） 分布式架构(基于 RPC:远程过程调用)
将业务拆分后,用某种方式实现各个业务模块的远程调用和复用,这时一个好的 RPC 框架就决定了你的分布式架构的性能,怎么调用,何时调用,服务器挂了怎么办......我们需要一个框架来帮我们解决这个问题(当然大神可以自己写一个,但是应对大流量的成功者莫过于中国的阿里巴巴公司,顶住了淘宝双十一的流量,反观一些学校内部的选课系统,对于大流量时只有两个字--宕机)。 

dubbo 是一个高性能的 RPC 框架,解决了分布式中的调用问题 
优点:解决了分布式系统中互相调用的问题 
缺点:假设有 100 台服务器,50 台用户业务服务器,50 台订单业务服务器,但是在上线后发现，用户服务器使用率很小,但是订单服务器压力很大,最佳配比应该是 1:4,这时候就要求我们还有一个统一管理的调度中心。

 

## 第一章 初始Dubbo



### 1.1 Dubbo性能高的原因

​        高性能要从底层的原理说起，既然是一个 RPC 框架，主要干的就是远程过程(方法)调用，那么提升性能就要从最关键、最耗时的两个方面入手：序列化和网络通信。 
​       序列化：我们学习 Java 网络开发的时候知道,本地的对象要在网络上传输，必须要实现 Serializable 接口，也就是必须序列化。我们序列化的方案很多：xml、json、二进制流…其中效率最高的就是二进制流(因为计算机就是二进制的)。然而 Dubbo 采用的就是效率最高的二进制。 
​       网络通信：不同于 HTTP 需要进行 7 步走(三次握手和四次挥手)， Dubbo 采用 Socket 通信机制,一步到位,提升了通信效率,并且可以建立长连接,不用反复连接,直接传输数据。



### 1.2 别的 RPC 框架 

gRPC 
Thrift 
HSF 
... 



## 第二章 dubbo框架



### 2.1 dubbo 概述 
Apache Dubbo (incubating) |ˈdʌbəʊ| 是一款高性能、轻量级的开源Java RPC 框架，它提供了三大核心能力：面向接口的远程方法调用，智能容错和负载均衡，以及服务自动注册和发现。 

Dubbo 是一个分布式服务框架，致力于提供高性能和透明化的 RPC 远程服务调用方案、服务治理方案。 

官网：http://dubbo.apache.org/zh/

面向接口代理：调用接口的方法，在 A 服务器调用 B 服务器的方法，由 dubbo 实现对 B 的调用，无需关心实现的细节，就像 MyBatis 访问Dao 的接口，可以操作数据库一样。不用关心 Dao 接口方法的实现。这样开发是方便，舒服的。

 

### 2.2 基本结构

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/dubbo001.png)

init 初始化  0.开始  1.注册  2.订阅  

async 异步  3.通知  5.总数

sync 同步  4.调用  

 服务提供者（Provider）：暴露服务的服务提供方，服务提供者在启动时，向注册中心注册自己提供的服务。 

服务消费者（Consumer）: 调用远程服务的服务消费方，服务消费者在启动时，向注册中心订阅自己所需的服务，服务消费者，从提供者地址列表中，基于软负载均衡算法，选一台提供者进行调用，如果调用失败，再选另一台调用。

注册中心（Registry）：注册中心返回服务提供者地址列表给消费者，如果有变更，注册中心将基于长连接推送变更数据给消费者

监控中心（Monitor）：服务消费者和提供者，在内存中累计调用次数和调用时间，定时每分钟发送一次统计数据到监控中心 

容器（container）：可以理解为spring容器

调用关系说明: 

- 服务容器负责启动，加载，运行服务提供者。 
- 服务提供者在启动时，向注册中心注册自己提供的服务。 
- 服务消费者在启动时，向注册中心订阅自己所需的服务。 
- 注册中心返回服务提供者地址列表给消费者，如果有变更，注册 中心将基于长连接推送变更数据给消费者。 
- 服务消费者，从提供者地址列表中，基于软负载均衡算法，选一 台提供者进行调用，如果调用失败，再选另一台调用。 
- 服务消费者和提供者，在内存中累计调用次数和调用时间，定时 每分钟发送一次统计数据到监控中心。



### 2.3 dubbo 支持的协议 
支持多种协议：dubbo ,  hessian , rmi , http, webservice , thrift , memcached , redis。 
dubbo 官方推荐使用 dubbo 协议。dubbo 协议默认端口 20880 
使用 dubbo 协议，spring 配置文件加入： 
<dubbo:protocol name="dubbo" port="20880" /> 



### 2.4 电商平台需求 

某电商平台系统需求，用户浏览商品；选择商品下订单，订单系 统需要获取用户信息中的送货地址；向支付系统请求完成付款。

| 服务     | 功能                                 |
| -------- | ------------------------------------ |
| 网站系统 | 展示商品，修改用户信息               |
| 订单系统 | 生成订单                             |
| 用户系统 | 用户信息（地址，收件人，联系方式等） |



### 2.5 直连方式 dubbo 

点对点的直连项目:消费者直接访问服务提供者，没有注册中心。 消费者必须指定服务提供者的访问地址（url）。 消费者直接通过 url 地址访问固定的服务提供者。这个 url 地址是 不变的。



#### 2.5.1 实现方式

（1）创建一个名为01-link-provider的项目（服务提供者）

（2）maven加入dubbo，spring，springmvc的依赖

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.yyb.dubbo</groupId>
  <artifactId>01-link-provider</artifactId>
  <version>1.0-SNAPSHOT</version>
  <!--
     注释<packaging>war</packaging>
     并把该项目打包到本地仓库（让消费者端的项目添加该项目的依赖）
     mvn 002-link-provider install
     然后把<packaging>war</packaging>改回
 -->
  <!--<packaging>war</packaging>-->



  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>

  <dependencies>

    <!--Dubbo依赖-->
    <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>dubbo</artifactId>
      <version>2.6.0</version>
    </dependency>

    <!--Spring依赖-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>4.3.16.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>4.3.16.RELEASE</version>
    </dependency>

  </dependencies>

</project>

```

（3）在resources目下创建dubbo（spring）的核心配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:dubbo="http://code.alibabatech.com/schema/dubbo"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://code.alibabatech.com/schema/dubbo http://code.alibabatech.com/schema/dubbo/dubbo.xsd">

    <!--声明服务提供者名称，保证它的唯一性，它是dubbo内部使用的唯一标识-->
    <dubbo:application name="dubbo-link-provider"/>

    <!--指定dubbo的协议名称和端口号
        name 指定协议名称，官方推荐dubbo协议
        port 协议的端口号，默认为20880
    -->
    <dubbo:protocol name="dubbo" port="20880"/>

    <!--
       暴露服务:dubbo:service
       interface 暴露服务的接口全限定类名
       ref 引用接口在spring容器中的标识名称
       registry 使用直连方式，不使用注册，值：N/A
   -->
    <dubbo:service interface="com.yyb.dubbo.service.SomeService"
                   ref="someServiceImpl"
                   registry="N/A"
    />

    <!--加载接口实现类-->
    <bean id="someServiceImpl" class="com.yyb.dubbo.service.impl.SomeServiceImpl"/>

</beans>
```

（4）在web.xml初始化dubbo

```xml
    <!--dubbo初始化-->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:dubbo-link-provider.xml</param-value>
    </context-param>
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>

```

（5）创建service层,模拟持久层

```java
SomeService.java
package com.yyb.dubbo.service;

public interface SomeService {

    String hello(String msg);

}

SomeServiceImpl.java

package com.yyb.dubbo.service.impl;

import com.yyb.dubbo.service.SomeService;


public class SomeServiceImpl implements SomeService {

    @Override
    public String hello(String msg) {
        //调用数据持久层
        return "Hello " + msg;
    }
}

```

（6）使用maven命令install将该项目打包到本地仓库给消费端的项目引用依赖

```xml
<!--
     注释<packaging>war</packaging>
     并把该项目打包到本地仓库（让消费者端的项目添加该项目的依赖）
     mvn 002-link-provider install
     然后把<packaging>war</packaging>改回
 -->
```

（7）创建名为02-link-consumer的项目（服务消费者）

（8）maven加入dubbo，spring，springmvc，服务提供者（暴露接口）的依赖

```xml
  <dependencies>

  <!--Dubbo依赖-->
  <dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>dubbo</artifactId>
    <version>2.6.0</version>
  </dependency>

  <!--Spring依赖-->
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>4.3.16.RELEASE</version>
  </dependency>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>4.3.16.RELEASE</version>
  </dependency>

  <!--暴露接口依赖-->
  <dependency>
    <groupId>com.yyb.dubbo</groupId>
    <artifactId>01-link-provider</artifactId>
    <version>1.0-SNAPSHOT</version>
  </dependency>
  </dependencies>
```

（9）在resources在配置dubbo（Spring）和springmvc核心配置文件

```xml
springmvc.xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/cache"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/cache http://www.springframework.org/schema/cache/spring-cache.xsd">

    <!--组件扫描-->
    <context:component-scan base-package="com.yyb.dubbo.web"/>

    <!--注解驱动-->
    <mvc:annotation-driven/>

    <!--视图解析器-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
</beans>

dubbo-link-consumer.xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:dubbo="http://code.alibabatech.com/schema/dubbo"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://code.alibabatech.com/schema/dubbo http://code.alibabatech.com/schema/dubbo/dubbo.xsd">

    <!--声明服务消费者名称，保证它的唯一性，它是dubbo内部服务名称的唯一标识-->
    <dubbo:application name="002-link-consumer"/>

    <!--
        引用远程接口
        id 远程接口服务的代理对象名称
        interface 接口的全限定类名
        url 调用远程接口服务的url地址
        registry 直连方式，不使用注册中心，值：N/A
    -->
    <dubbo:reference id="someService"
                     interface="com.yyb.dubbo.service.SomeService"
                     url="dubbo://localhost:20880"
                     registry="N/A"/>

</beans>
```

（10）配置web.xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!--声明springmvc的中央调度器-->
    <servlet>
        <servlet-name>dispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:dubbo-link-consumer.xml,classpath:springmvc.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>dispatcherServlet</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```

（11）创建Controller层连接暴露接口

```java
package com.yyb.dubbo.web;

import com.yyb.dubbo.service.SomeService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;


@Controller
public class SomeController {

    @Autowired
    private SomeService someService;

    @RequestMapping("/hello")
    public String hello(Model model){
        //调用远程接口
        String hello = someService.hello("world");

        model.addAttribute("hello",hello);

        return "hello";
    }
}

```

（12）把两个项目都用IDEA部署到tomcat上（注意端口号不要一样），然后在浏览器上输入访问地址即可



直连方式的缺点 ：在实现暴露服务接口的同时也会知道服务提供者的底层实现细节。





### 2.6 Dubbo官方推荐使用的项目结构

dubbo官方推荐使用的项目结构如下：
1.服务提供者工程
	实现接口工程中的业务接口
	web工程
2.服务消费者工程
	消费服务提供者提供的业务接口
	web工程
3.接口工程
	业务接口和实体类
	java工程

#### 2.6.1 实现方式

（1）创建接口工程（java工程）

（2）创建本地对象的javabean和服务层的接口（只要是分布式开发本地对象都要做序列化操作）

```java
User.java

package com.yyb.dubbo.model;

import java.io.Serializable;

//只要是分布式开发本地对象都要做序列化操作
public class User implements Serializable {
    private Integer id;
    private String username;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }
}

SomeService.java

package com.yyb.dubbo.service;

import com.yyb.dubbo.model.User;

public interface SomeService {
    /**
     * Hello
     * @return
     */
    String hello();

    /**
     * 根据用户标识获取用户详情
     * @param id
     * @return
     */
    User queryUserById(Integer id);
}

```

（3）创建服务提供者工程（web工程）

（4）加入dubbo，spring，springmvc以及接口工程依赖

```xml
  <dependencies>

    <!--dubbo依赖-->
    <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>dubbo</artifactId>
      <version>2.6.0</version>
    </dependency>

    <!--Spring依赖-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>4.3.16.RELEASE</version>
    </dependency>

    <!--spingmvc依赖-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>4.3.16.RELEASE</version>
    </dependency>

    <!--接口工程-->
    <dependency>
      <groupId>com.yyb.dubbo</groupId>
      <artifactId>003-interface</artifactId>
      <version>1.0-SNAPSHOT</version>
    </dependency>

  </dependencies>
```

（5）创建接口工程实现类

```java
SomeServiceImpl.java

package com.yyb.dubbo.service.impl;

import com.yyb.dubbo.model.User;
import com.yyb.dubbo.service.SomeService;

public class SomeServiceImpl  implements SomeService {
    @Override
    public String hello() {
        return "hello dubbo";
    }

    @Override
    public User queryUserById(Integer id) {
        User user = new User();
        user.setId(id);
        user.setUsername("lisi"+id);
        return user;
    }
}
```

（6）创建dubbo（spring）核心配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:dubbo="http://code.alibabatech.com/schema/dubbo"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://code.alibabatech.com/schema/dubbo http://code.alibabatech.com/schema/dubbo/dubbo.xsd">

    <!--声明服务提供者名称，保证它的唯一性-->
    <dubbo:application name="dubbo-link-provider"/>

    <!--指定协议和端口号，官方推荐使用dubbo协议，端口号默认为20880-->
    <dubbo:protocol name="dubbo" port="20880"/>

    <!--暴露服务接口dubbo：service-->
    <dubbo:service interface="com.yyb.dubbo.service.SomeService"
                   ref="someServiceImpl"
                   registry="N/A"/>

    <!--加载实现类接口-->
    <bean id="someServiceImpl" class="com.yyb.dubbo.service.impl.SomeServiceImpl"/>
</beans>
```

（7）配置web.xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!--通过监听器初始化dubbo-->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:dubbo-link-provider.xml</param-value>
    </context-param>
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
</web-app>
```

（8）创建服务消费者工程（web工程）

（9）加入dubbo，spring，springmvc以及工程接口依赖

```xml
  <dependencies>
    <!--dubbo依赖-->
    <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>dubbo</artifactId>
      <version>2.6.0</version>
    </dependency>

    <!--Spring依赖-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>4.3.16.RELEASE</version>
    </dependency>

    <!--spingmvc依赖-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>4.3.16.RELEASE</version>
    </dependency>

    <!--接口工程-->
    <dependency>
      <groupId>com.yyb.dubbo</groupId>
      <artifactId>003-interface</artifactId>
      <version>1.0-SNAPSHOT</version>
    </dependency>

  </dependencies>
```

（10）创建Controller层调用服务

```java
SomeController.java

package com.yyb.dubbo.web;

import com.yyb.dubbo.model.User;
import com.yyb.dubbo.service.SomeService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class SomeController {

    @Autowired
    private SomeService someService;

    @RequestMapping("/hello")
    public String hello(Model model){
        //调用远程接口服务
        String hello = someService.hello();
        model.addAttribute("hello",hello);

        return "hello";
    }

    @RequestMapping("/user/detail")
    public String userDetail(Model model,Integer id){
        //调用远程接口服务
        User user = someService.queryUserById(id);
        model.addAttribute("user",user);
        return "user";
    }

}

```

（11）创建Springmvc，dubbo（spring）核心配置文件

```xml
springmvc.xml

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!--扫描组件-->
    <context:component-scan base-package="com.yyb.dubbo.web"/>

    <!--注解驱动-->
    <mvc:annotation-driven/>

    <!--视图解析器-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/"/>
        <property name="suffix" value=".jsp"/>
    </bean>

</beans>

dubbo-link-consumer.xml

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:dubbo="http://code.alibabatech.com/schema/dubbo"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://code.alibabatech.com/schema/dubbo http://code.alibabatech.com/schema/dubbo/dubbo.xsd">

    <!--服务消费者名称,保证它的唯一性-->
    <dubbo:application name="005-link-consumer"/>

    <!--
        引用远程接口服务
    -->
    <dubbo:reference id="someService"
                     interface="com.yyb.dubbo.service.SomeService"
                     url="dubbo://localhost:20880"
                     registry="N/A"/>

</beans>
```

（12）配置web.xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!--声明springmvc的中央调度器-->
    <servlet>
        <servlet-name>dispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:dubbo-link-consumer.xml,classpath:springmvc.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>dispatcherServlet</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```

（13）创建hello.jsp,user.jsp模拟接收数据

```jsp
hello.jsp
<h1>${hello}</h1>

user.jsp
<h2>用户编号：${user.id}</h2>
<h2>用户姓名：${user.username}</h2>
```

（14）将服务提供者工程和服务消费者工程部署到tomcat上面（注意端口号的问题），地址栏输入地址并测试



## 第三章 注册中心-Zookeeper



### 3.1 注册中心概述 
对于服务提供方，它需要发布服务，而且由于应用系统的复杂性，服务的数量、类型也不断膨胀；对于服务消费方，它最关心如何获取到它所需要的服务，而面对复杂的应用系统，需要管理大量的服务调用。 
而且，对于服务提供方和服务消费方来说，他们还有可能兼具这两种角色，即需要提供服务，有需要消费服务。 通过将服务统一管理起来，可以有效地优化内部应用对服务发布/使用的流程和管理。服务注册中心可以通过特定协议来完成服务对外的统一。Dubbo 提供的注册中心有如下几种类型可供选： 

Multicast 注册中心：组播方式 
Redis 注册中心：使用 Redis 作为注册中心
Simple 注册中心：就是一个 dubbo 服务。作为注册中心。提供查找服务的功能。 
Zookeeper 注册中心：使用 Zookeeper 作为注册中心

推荐使用Zookeeper 注册中心

查看文档 https://dubbo.apache.org/zh/docs/



### 3.2 注册中心工作方式

![](https://gitee.com/yybovo/note-images/raw/master/Typora/dubbo002.png)



### 3.3  Zookeeper 注册中心

Zookeeper 是一个高性能的，分布式的，开放源码的分布式应用程序协调服务。简称 zk。

Zookeeper 是翻译过来是动物管理员。可以理解为 windows 中的资源管理器或者注册表。

他是一个树形结构。这种树形结构和标准文件系统相似。ZooKeeper 树中的每个节点被称为Znode。和文件系统的目录树一样，ZooKeeper 树中的每个节点可以拥有子节点。每个节点表示一个唯一服务资源。Zookeeper 运行需要 java 环境。

#### 3.3.1 下载安装文件 
官网下载地址: http://zookeeper.apache.org/ 进入官网地址

![](https://gitee.com/yybovo/note-images/raw/master/Typora/dubbo003.png)

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/dubbo004.png)

镜像站点进行下载: https://mirrors.tuna.tsinghua.edu.cn/apache/zookeeper/

#### 3.3.2 安装配置 Zookeeper 
A、 Windows 平台 Zookeeper 安装，配置 
下载的文件 zookeeper-3.5.4-beta.tar.gz. 解压后到目录就可以了，例如D:\Apache\Zookeeper\apache-zookeeper-3.5.6-bin修改 zookeeper-3.5.6/conf/ 目录下配置文件 

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/dubbo005.png)

复制 zoo-sample.cfg 改名为 zoo.cfg

```
# The number of milliseconds of each tick
tickTime=2000
# The number of ticks that the initial 
# synchronization phase can take
initLimit=10
# The number of ticks that can pass between 
# sending a request and getting an acknowledgement
syncLimit=5
# the directory where the snapshot is stored.
# do not use /tmp for storage, /tmp here is just 
# example sakes.
dataDir=/tmp/zookeeper
# the port at which the clients will connect
clientPort=2181
```

tickTime: 心跳的时间，单位毫秒. Zookeeper 服务器之间或客户端与服务器之间维持心跳的时间间隔，也就是每个 tickTime 时间就会发送一个心跳。表明存活状态。

dataDir:  数据目录，可以是任意目录。存储 zookeeper 的快照文件、pid 文件，默认为/tmp/zookeeper，建议在 zookeeper 安装目录下创建 data 目 录 ， 将 dataDir 配置改为 /usr/local/zookeeper-3.4.10/data
clientPort: 客户端连接 zookeeper 的端口，即 zookeeper 对外的服务端口，默认为 2181 

配置内容：

1.	dataDir : zookeeper 数据的存放目录
2.	admin.serverPort=8888
   原因：zookeeper 3.5.x 内部默认会启动一个应用服务器，默认占用8080 端口 

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/dubbo006.png)



B、 Linux 平台 Zookeeper 安装、配置 
Zookeeper 的运行需要 jdk。使用前 Linux 系统要安装好 jdk. 
①：上传 zookeeper-3.5.4-beta.tar.gz.并解压
解压文件 zookeeper-3.5.4-beta.tar.gz. 
执行命令：tar -zxvf apache-zookeeper-3.5.6-bin.tar.gz -C /root/zookeeper
②：配置文件
在 zookeeper 的 conf 目录下，将 zoo_sample.cfg 改名为 zoo.cfg，cp zoo_sample.cfg zoo.cfg 
zookeeper 启动时会读取该文件作为默认配置文件。 
进入 zookeeper 目录下的 conf 
拷贝样例文件 zoo-sample.cfg 为 zoo.cfg 
③：启动 Zookeeper
启动（切换到安装目录的 bin 目录下）：./zkServer.sh start
④：关闭 Zookeeper
关闭（切换到安装目录的 bin 目录下）：./zkServer.sh stop



### 3.4 改造 dubbo—使用 Zookeeper

#### 3.4.1 实现方式

（1）创建接口工程（java工程）

（2）创建本地对象的javabean和服务层的接口（只要是分布式开发本地对象都要做序列化操作）

```java
User.java

package com.yyb.dubbo.model;

import java.io.Serializable;

//只要是分布式开发本地对象都要做序列化操作
public class User implements Serializable {
    private Integer id;
    private String username;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }
}

SomeService.java

package com.yyb.dubbo.service;

import com.yyb.dubbo.model.User;

public interface SomeService {
    /**
     * Hello
     * @return
     */
    String hello();

    /**
     * 根据用户标识获取用户详情
     * @param id
     * @return
     */
    User queryUserById(Integer id);
}

```

（3）创建服务提供者工程（web工程）

（4）加入dubbo，spring，springmvc,工程接口以及zookeeper注册中心依赖

```xml
    <!--dubbo依赖-->
    <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>dubbo</artifactId>
      <version>2.6.2</version>
    </dependency>

    <!--Spring依赖-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>4.3.16.RELEASE</version>
    </dependency>

    <!--spingmvc依赖-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>4.3.16.RELEASE</version>
    </dependency>

    <!--接口工程-->
    <dependency>
      <groupId>com.yyb.dubbo</groupId>
      <artifactId>003-interface</artifactId>
      <version>1.0-SNAPSHOT</version>
    </dependency>

    <!--zookeeper注册中心依赖-->
    <dependency>
      <groupId>org.apache.curator</groupId>
      <artifactId>curator-framework</artifactId>
      <version>4.1.0</version>
    </dependency>
```

（5）创建接口工程实现类

```java
SomeServiceImpl.java

package com.yyb.dubbo.service.impl;

import com.yyb.dubbo.model.User;
import com.yyb.dubbo.service.SomeService;

public class SomeServiceImpl  implements SomeService {
    @Override
    public String hello() {
        return "hello dubbo";
    }

    @Override
    public User queryUserById(Integer id) {
        User user = new User();
        user.setId(id);
        user.setUsername("lisi"+id);
        return user;
    }
}
```

（6）创建dubbo（spring）核心配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:dubbo="http://code.alibabatech.com/schema/dubbo"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://code.alibabatech.com/schema/dubbo http://code.alibabatech.com/schema/dubbo/dubbo.xsd">

    <!--声明服务提供者名称-->
    <dubbo:application name="006-zk-provider"/>

    <!--指定协议及端口号-->
    <dubbo:protocol name="dubbo" port="20880"/>

    <!--指定注册中心-->
    <dubbo:registry address="zookeeper://localhost:2181"/>

    <!--暴露服务-->
    <dubbo:service interface="com.yyb.dubbo.service.SomeService" ref="someServiceImpl" timeout="35000"/>
    <!--timeout 超时，如果访问时间超过35秒还没有访问完就会报错-->

    <!--加载接口实现类-->
    <bean id="someServiceImpl" class="com.yyb.dubbo.service.impl.SomeServiceImpl"/>

</beans>
```

（7）配置web.xml文件

```xml
<!--通过监听器初始化dubbo-->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:dubbo-zk-provider.xml</param-value>
    </context-param>
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
```

（8）创建服务消费者工程（web工程）

（9）加入dubbo，spring，springmvc,工程接口以及zookeeper注册中心依赖

```xml
 <!--dubbo依赖-->
    <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>dubbo</artifactId>
      <version>2.6.2</version>
    </dependency>

    <!--Spring依赖-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>4.3.16.RELEASE</version>
    </dependency>

    <!--spingmvc依赖-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>4.3.16.RELEASE</version>
    </dependency>

    <!--接口工程-->
    <dependency>
      <groupId>com.yyb.dubbo</groupId>
      <artifactId>003-interface</artifactId>
      <version>1.0-SNAPSHOT</version>
    </dependency>

    <!--zookeeper注册中心依赖-->
    <dependency>
      <groupId>org.apache.curator</groupId>
      <artifactId>curator-framework</artifactId>
      <version>4.1.0</version>
    </dependency>
```

（10）创建Controller层调用服务

```java
package com.yyb.dubbo.web;

import com.yyb.dubbo.model.User;
import com.yyb.dubbo.service.SomeService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class SomeController {

    @Autowired
    private SomeService someService;

    @RequestMapping("/hello")
    public String hello(Model model){
        //调用远程接口服务
        String hello = someService.hello();
        model.addAttribute("hello",hello);

        return "hello";
    }

    @RequestMapping("/user/detail")
    public String userDetail(Model model,Integer id){
        //调用远程接口服务
        User user = someService.queryUserById(id);
        model.addAttribute("user",user);
        return "user";
    }

}

```

（11）创建Springmvc，dubbo（spring）核心配置文件

```xml
springmvc.xml

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!--扫描组件-->
    <context:component-scan base-package="com.yyb.dubbo.web"/>

    <!--注解驱动-->
    <mvc:annotation-driven/>

    <!--视图解析器-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/"/>
        <property name="suffix" value=".jsp"/>
    </bean>

</beans>

dubbo-zk-consumer.xml

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:dubbo="http://code.alibabatech.com/schema/dubbo"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://code.alibabatech.com/schema/dubbo http://code.alibabatech.com/schema/dubbo/dubbo.xsd">

    <!--声明服务消费者名称-->
    <dubbo:application name="007-zk-consumer"/>

    <!--指定注册中心-->
    <dubbo:registry address="zookeeper://localhost:2181"/>

    <!--引用远程接口服务-->
    <dubbo:reference id="someService" interface="com.yyb.dubbo.service.SomeService" check="false"/>

</beans>
```

（12）配置web.xml文件

```xml
    <!--声明springmvc的中央调度器-->
    <servlet>
        <servlet-name>dispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:dubbo-zk-consumer.xml,classpath:springmvc.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>dispatcherServlet</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
```

（13）创建接收模拟数据的hello.jsp,user.jsp

```jsp
hello.jsp
<h1>${hello}</h1>

user.jsp
<h2>用户编号：${user.id}</h2>
<h2>用户姓名：${user.username}</h2>
```

（14）启动zookeeper（bin/zkServer.cmd双击启动）

（15）将服务提供者工程和服务消费者工程部署到tomcat上面（注意端口号的问题），地址栏输入地址并测试

Zookeeper 是高可用的，健壮的。Zookeeper 宕机，正在运行中的dubbo 服务仍然可以正常访问。

健壮性

- 监控中心宕掉不影响使用，只是丢失部分采样数据

- 注册中心仍能通过缓存提供服务列表查询，但不能注册新服务

- 服务提供者无状态，任意一台宕掉后，不影响使用

- 服务提供者全部宕掉后，服务消费者应用将无法使用，并无限次重连等待服务提供者恢复 



## 第四章 dubbo 的配置



### 4.1 配置原则

在服务提供者配置访问参数。因为服务提供者更了解服务的各种参数。 



### 4.2 关闭检查 
dubbo 缺省会在启动时检查依赖的服务是否可用，不可用时会抛出异常，阻止 Spring 初始化完成，以便上线时，能及早发现问题，默认 check=true。通过 check="false"关闭检查，比如，测试时，有些服务不关心，或者出现了循环依赖，必须有一方先启动。 
例 1：关闭某个服务的启动时检查 
<dubbo:reference interface="com.foo.BarService" check="false" /> 

例 2：关闭注册中心启动时检查 
<dubbo:registry check="false" /> 
默认启动服务时检查注册中心存在并已运行。注册中心不启动会报错。 



### 4.3 重试次数 
消费者访问提供者，如果访问失败，则切换重试访问其它服务器，但重试会带来更长延迟。访问时间变长，用户的体验较差。多次重新访问服务器有可能访问成功。可通过 retries="2" 来设置重试次数(不含第一次)。 

重试次数配置如下：
<dubbo:service retries="2" />
或
<dubbo:reference retries="2" />



### 4.4 超时时间 
由于网络或服务端不可靠，会导致调用出现一种不确定的中间状态（超时）。为了避免超时导致客户端资源（线程）挂起耗尽，必须设置超时时间。
timeout：调用远程服务超时时间(毫秒)

#### 4.3.1 dubbo 消费端

指定接口超时配置
<dubbo:reference interface="com.foo.BarService" timeout="2000" />

#### 4.3.2 dubbo 服务端

指定接口超时配置
dubbo:server interface="com.foo.BarService" timeout="2000" />



### 4.5 版本号

每个接口都应定义版本号，为后续不兼容升级提供可能。当一个接口有不同的实现，项目早期使用的一个实现类， 之后创建接口的新的实现类。区分不同的接口实现使用 version。 

#### 4.5.1 实现方式

该项目在3.4.1 实现方式上继续实现，模拟项目中有在原有的服务上增加新的服务

（16）在服务提供者的项目中新增服务

```java
package com.yyb.dubbo.service.impl;

import com.yyb.dubbo.model.User;
import com.yyb.dubbo.service.SomeService;

public class NewSomeServiceImpl implements SomeService {

    public String hello() {
        return "Hello Dubbo Project-222";
    }

    public User queryUserById(Integer id) {
        User user = new User();
        user.setId(id);
        user.setUsername("222-"+id);
        return user;
    }
}
```

（17）在dubbo（spring）配置文件中增加该服务

```xml
    <!--暴露服务-->
    <dubbo:service interface="com.yyb.dubbo.service.SomeService" ref="someServiceImpl" version="1.0"/>
    <!--version 版本号，与服务消费端相同的版本号实现对接-->
    <dubbo:service interface="com.yyb.dubbo.service.SomeService" ref="newSomeServiceImpl" version="2.0"/>

    <!--加载接口实现类-->
    <bean id="someServiceImpl" class="com.yyb.dubbo.service.impl.SomeServiceImpl"/>
    <bean id="newSomeServiceImpl" class="com.yyb.dubbo.service.impl.NewSomeServiceImpl"/>

```

（18）在服务消费者工程中对dubbo（spring）核心配置文件进行改动

```xml
    <!--引用远程接口服务-->
    <dubbo:reference id="someService" interface="com.yyb.dubbo.service.SomeService" version="1.0"/>
    <dubbo:reference id="newSomeService" interface="com.yyb.dubbo.service.SomeService" version="2.0"/>


```

（19）Controller层添加新服务

```java
package com.yyb.dubbo.web;

import com.yyb.dubbo.model.User;
import com.yyb.dubbo.service.SomeService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class SomeController {

    @Autowired
    private SomeService someService;

    @Autowired
    private SomeService newSomeService;

    @RequestMapping("/hello")
    public String hello(Model model){
        //调用远程接口服务
        String hello = someService.hello();
        model.addAttribute("hello",hello);

        String hello1 = newSomeService.hello();
        model.addAttribute("hello1",hello1);

        return "hello";
    }

    @RequestMapping("/user/detail")
    public String userDetail(Model model,Integer id){
        //调用远程接口服务
        User user = someService.queryUserById(id);
        model.addAttribute("user",user);

        User user1 = newSomeService.queryUserById(id);
        model.addAttribute("user1",user1);
        return "user";
    }

}
```

（20）jsp进行相应改动

```jsp
<h1>${hello}</h1>
<h1>${hello1}</h1>

<h2>用户编号：${user1.id}</h2>
<h2>用户姓名：${user1.username}</h2>
```

提供者有版本号，消费者必须有相应的版本号



## 第五章 监控中心 



### 5.1 什么是监控中心 

Dubbo 的使用，其实只需要有注册中心，消费者，提供者这三个就可以使用了，但是并不能看到有哪些消费者和提供者，为了更好的调试，发现问题，解决问题，因此引入 dubbo-admin。通过 dubbo-admin 可以对消费者和提供者进行管理。可以在 dubbo 应用部署做动态的调整，服务的管理。 
dubbo-admin 
图形化的服务管理页面；安装时需要指定注册中心地址，即可从注册中心中获取到所有的提供者/消费者进行配置管理 
dubbo-monitor-simple 
简单的监控中心； 

### 5.2 发布配置中心 

#### 5.2.1 下载监控中心 

https://github.com/apache/incubator-dubbo-ops 
这里下载的是源代码，需要手工编译才能使用。 

#### 5.2.2 运行管理后台 dubbo-admin 
到 dubbo-admin-0.0.1-SNAPSHOT.jar 所在的目录。执行下面命令 java -jar dubbo-admin-0.0.1-SNAPSHOT.jar 

#### 5.2.3 修改配置 dubbo-properties 文件 

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/dubbo007.png)

application.properties 文件，内容如下：

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/dubbo008.png)

#### 5.2.4 运行 dubbo-admin 应用

1）	先启动注册中心
2）	执行提供者项目
3）	java -jar dubbo-admin-0.0.1-SNAPSHOT.jar 启动 dubbo 管理后台
4）	在浏览器地址栏输入 http://localhost:7001 访问监控中心-控制台。

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/dubbo009.png)

#### 5.3 监控中心的数据来源 
dubbo.registry.address=zookeeper://127.0.0.1:2181 
监控中心的数据来自注册中心（Zookeeper） 

#### 5.4 应用监控中心 
通过浏览器，访问监控中心主页。点击菜单访问功能选项。

