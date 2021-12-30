# Spring Boot





## 第一章 Spring Boot框架入门



### 1.1Spring Boot简介

Spring Boot 是Spring 家族中的一个全新的框架，它用来简化Spring 应用程序的创建和开发过程，也可以说Spring Boot 能简化我们之前采用SpringMVC + Spring + MyBatis 框架进行开发的过程。

在以往我们采用SpringMVC + Spring + MyBatis 框架进行开发的时候，搭建和整合三大框架，我们需要做很多工作，比如配置web.xml，配置Spring，配置MyBatis，并将它们整合在一起等，而Spring Boot 框架对此开发过程进行了革命性的颠覆，完全抛弃了繁琐的xml 配置过程，采用大量的默认配置简化我们的开发过程。所以采用Spring Boot 可以非常容易和快速地创建基于Spring 框架的应用程序，它让编码变简单了，配置变简单了，部署变简单了，监控变简单了。正因为 Spring Boot 它化繁为简，让开发变得极其简单和快速，所以在业界备受关注。

Spring Boot 在国内的关注趋势图：http://t.cn/ROQLquP



### 1.2Spring Boot 的特性

- 能快速的创建Spring的应用程序
- 能过直接使用java main 方法启动内嵌的Tomcat服务器运行 Spring Boot程序，不需要部署war包文件
- 提供约定的starter POM（起步依赖，起步pom文件，父工程的pom文件，里面已经存在很多依赖，由子pom文件去继承，声明式来获取所需的依赖） 来简化 Maven配置，让Maven配置变得更简单
- 自动化配置，根据项目的Maven依赖配置，Spring Boot 自动配置Spring、Spring MVC、等
- 提供了程序的健康检查等功能
- 基本可以完全不使用XML配置文件，采用注解方式



### 1.3Spring Boot四大核心



#### 1.3.1 自动配置



#### 1.3.2 起步依赖



#### 1.3.3 Actuator(国内不常用)



#### 1.3.4 命令行界面(国内不常用)





## 第二章 Spring Boot 入门案例



### 2.1第一个Spring Boot 项目



IDEA如果出现代理的错误，根据图片的标记操作

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot009.png)

https://start.aliyun.com/



#### 2.1.1 开发步骤

项目名称 Spring-Boot

（1）创建一个Module，选择为Spring Initializr 快速构建



![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot001.png)



（2）设置GAV坐标及pom配置信息

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot002.png)



（3）选择Spring Boot版本及依赖

snapshot：表示是开发版本，不是稳定版本

release：表示是稳定版本

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot003.png)



（4）设置目录名称、Content Root 路径及模块文件的目录

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot004.png)

<font color=red>点击Finish，如果是第一次创建，在右下角会提示正在下载相关的依赖</font>



（5）项目结构

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot005.png)

➢	.mvn|mvnw|mvnw.cmd：使用脚本操作执行 maven 相关命令，国内使用较少，可删除
➢	.gitignore：使用版本控制工具 git 的时候，设置一些忽略提交的内容
➢	static|templates：后面模板技术中存放文件的目录
➢	application.properties：SpringBoot 的配置文件，很多集成的配置都可以在该文件中进行配置，例如：Spring、springMVC、Mybatis、Redis 等。目前是空的
➢	Application.java：SpringBoot 程序执行的入口，执行该程序中的main 方法，SpringBoot就启动了

```xml
pom.xml解读
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<!--父工程GVA坐标-->
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.5.2</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<!--该工程的GVA坐标-->
	<groupId>com.yyb</groupId>
	<artifactId>spring_boot</artifactId>
	<version>0.0.1-SNAPSHOT</version>

	<name>spring_boot111</name>
	<description>Demo project for Spring Boot111</description>

	<!--设置编译的级别-->
	<properties>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
		<!--SpringBoot框架web项目的起步依赖-->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		<!--SpringBoot框架测试起步依赖-->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<!--SpringBoot框架编译打包的插件-->
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>

```



### 2.2 案例解读



#### 2.2.1 创建一个Spring MVC 的 IndexController



IndexContontroller 类所在包：com.yyb.springboot.web

```java
package com.yyb.springboot.web;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class IndexController {

    @RequestMapping("/index")
    @ResponseBody
    public Object index(){
        return "Hello SpringBoot Web Project";
    }
}

```

<font color=red>注意：新创建的类一定要位于 Application 同级目录或者下级目录，否则 SpringBoot 加载不到。 </font>



#### 2.2.2 在IDEA中右键，运行Application类中的main方法

通过在控制台的输出，可以看到启动 SpringBoot 框架，会启动一个内嵌的 tomcat，端口号为8080，上下文根为空 

```java
 Tomcat started on port(s): 8080 (http) with context path ''
```



#### 2.2.3 在浏览器输入http://localhost:8080/index访问



![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot006.png)



#### 2.2.4 分析

➢	Spring Boot 的父级依赖 spring-boot-starter-parent 配置之后，当前的项目就是 Spring Boot 项目
➢	spring-boot-starter-parent 是一个Springboot 的父级依赖，开发SpringBoot 程序都需要继承该父级项目，它用来提供相关的 Maven 默认依赖，使用它之后，常用的 jar包依赖可以省去 version 配置
➢	Spring Boot 提供了哪些默认 jar 包的依赖，可查看该父级依赖的pom 文件
➢	如果不想使用某个默认的依赖版本，可以通过 pom.xml 文件的属性配置覆盖各个依赖项，比如覆盖 Spring 版本

```xml
<properties> <spring-framework.version>5.0.0.RELEASE</ spring-framework.version > </properties> 
```

➢	<font color=red>@SpringBootApplication 注解是 Spring Boot 项目的核心注解，主要作用是开启Spring 自动配置，如果在 Application 类上去掉该注解，那么不会启动 SpringBoot程序</font>
➢	main 方法是一个标准的 Java 程序的main 方法，主要作用是作为项目启动运行的入口
➢	@Controller 及 @ResponseBody 依然是我们之前的Spring MVC，因为 Spring Boot的里面依然是使用我们的Spring MVC + Spring + MyBatis 等框架



### 2.3 Spring Boot 核心配置文件



Spring Boot 的核心配置文件用于配置 Spring Boot 程序，名字必须以application 开始，而且只能有一个该名称的文件

#### 2.3.1 核心配置格式

（1）.properties 文件（默认采用该文件）

通过修改application.properties 配置文件，在修改默认 tomcat 端口号及项目上下文件根

```properties
#设置内嵌Tomcat端口号
server.port=8090
#配置项目上下文根
server.servlet.context-path=/springboot
```

```java
Tomcat started on port(s): 8090 (http) with context path '/springboot'
```

页面显示结果

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot007.png)



（2）.yml文件

yml 是一种 yaml 格式的配置文件，主要采用一定的空格、换行等格式排版进行配置。 

yaml 是一种直观的能够被计算机识别的的数据序列化格式，容易被人类阅读，yaml 类似于 xml，但是语法比 xml 简洁很多，值与前面的冒号配置项必须要有一个空格， yml 后缀也可以使用 yaml 后缀 

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot008.png)

<font color=purple>注意：当两种格式配置文件同时存在，使用的是.properties 配置文件</font>



#### 2.3.2 多环境配置



在实际开发的过程中，我们的项目会经历很多的阶段（开发->测试->上线），每个阶段的配置也会不同，例如：端口、上下文根、数据库等，那么这个时候为了方便在不同的环境之间切换，SpringBoot 提供了多环境配置，具体步骤如下 

<font color=red>子环境核心配置文件的名称是以：application-xxx.properties</font>
<font color=red>主核心配置文件只能有一个：application.properties</font>

<font color=red>在核心配置文件中指定其中一个配置文件生效,通过spring.profiles.active=xxx名称</font>

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot010.png)

```properties
#application.properties
#激活配置文件
spring.profiles.active=dev

```

```yaml
#application.yml
#激活生产环境 
spring:
	profiles:
    	acitve: dev
```



#### 2.3.3 Spring Boot 自定义配置

在SpringBoot 的核心配置文件中，除了使用内置的配置项之外，我们还可以在自定义配置，然后采用如下注解去读取配置的属性值

（1）@Value 注解

- 在核心配置文件 applicatin.properties 中，添加两个自定义配置项 name 和website。在 IDEA 中可以看到这两个属性不能被SpringBoot 识别，背景是桔色的

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot011.png)

- 在 SpringBootController 中定义属性，并使用@Value 注解或者自定义配置值，并对其方法进行测试

  ```java
  package com.yyb.springboot.web;
  
  import org.springframework.beans.factory.annotation.Value;
  import org.springframework.stereotype.Controller;
  import org.springframework.web.bind.annotation.RequestMapping;
  import org.springframework.web.bind.annotation.ResponseBody;
  
  @Controller
  public class IndexController {
  
      @Value("${name}")
      private String name;//用@value注解获取application.properties的值并接收给变量
  
      @Value("${website}")
      private String website;
  
      @RequestMapping("/index")
      @ResponseBody
      public Object index(){
          return "name="+name+",website="+website;
      }
  }
  
  ```

- 重新运行Application，在浏览器中进行测试

  ![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot012.png)

（2）@ConfigurationProperties

将整个文件映射成一个对象，用于自定义配置项比较多的情况

在 com.yyb.springboot.model 包下创建 School,City 类，并为该类加上 Component 和ConfigurationProperties 注解，并在 ConfigurationProperties 注解中添加属性 prefix，作用可以区分同名配置

```java
School.java
package com.yyb.springboot.model;

import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;

@Component//使用在类上用于实例化Bean
@ConfigurationProperties(prefix = "school")
public class School {

    private String name;
    private String website;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getWebsite() {
        return website;
    }

    public void setWebsite(String website) {
        this.website = website;
    }
}

City.java
package com.yyb.springboot.model;

import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;

@Component
@ConfigurationProperties(prefix = "city")
public class City {

    private String name;
    private String website;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getWebsite() {
        return website;
    }

    public void setWebsite(String website) {
        this.website = website;
    }
}

```

application.properties 配置文件

```properties
# 应用名称
spring.application.name=17_005_springboot

# 应用服务 WEB 访问端口
server.port=8080

school.name=hnrj
school.website=www.hnrj.com
city.name=hn
city.website=www.hn.com

```

application.yml 配置文件

```yaml
server:
	prot: 8080
school:
	name: hnrj
	website: www.hnrj.com
city:
	name: hn
	website: www.hn.com
```

在com.yyb.springboot.web目录下创建IndexController

```java
package com.yyb.springboot.web;

import com.yyb.springboot.model.City;
import com.yyb.springboot.model.School;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class IndexController {

    //在IndexController 中注入School,City 配置类
    @Autowired
    private School school;

    @Autowired
    private City city;

    @RequestMapping("/school")
    @ResponseBody
    public Object school(){
        return "school.name="+school.getName()+",school.website="+school.getWebsite();
    }

    @RequestMapping("/city")
    @ResponseBody
    public Object city(){
        return "city.name="+city.getName()+",city.website"+city.getWebsite();
    }
}

```

重新运行Application，在浏览器中进行测试

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot013.png)

（3）警告解决

- 在 ConfigInfo 类中使用了 ConfigurationProperties 注解后，IDEA 会出现一个警告，不影响程序的执行

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot014.png)

- 点击open documentnation 跳转到网页，在网页中提示需要加一个依赖，我们将这个依赖拷贝，粘贴到 pom.xml 文件中

  ![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot015.png)

```xml
<!--解决使用@ConfigurationProperties注解出现警告问题-->
<dependency> 
	<groupId>org.springframework.boot</groupId> 
	<artifactId>spring-boot-configuration-processor</artifactId> 
	<optional>true</optional> 
</dependency>
```

（4）中文乱码

如果在SpringBoot 核心配置文件中有中文信息，会出现乱码：

◼	一般在配置文件中，不建议出现中文（注释除外）
◼	如果有，可以先转化为 ASCII 码

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot016.png)

（5）提示

<font color=red>如果是从其它地方拷贝的配置文件，一定要将里面的空格删干净 </font>



### 2.4 Spring Boot 前端使用jsp



SpringBoot集成jsp思路：

- 创建一个webapp来存放jsp页面

- 添加SpringBoot工程内嵌Tomcat对jsp解析的一个依赖

- SpringBoot工程指定了jsp文件编译的路径META-INF/resources

  

#### 2.4.1 在 src/main 下创建一个 webapp 目录，然后在该目录下新建index.jsp 页面 

如果在webapp目录下右键，没有创建jsp的选项，可以在Project Structure中指定webapp为Web Resource Directory 



#### 2.4.2 在pom.xml 文件中配置以下依赖项

```xml
        <!--SpringBoot框架内嵌Tomcat对象jsp的解析依赖-->
        <dependency>
            <groupId>org.apache.tomcat.embed</groupId>
            <artifactId>tomcat-embed-jasper</artifactId>
        </dependency>
        如果要使用servlet必须添加该以下两个依赖-->
        <!-- servlet依赖的jar包-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
        </dependency>
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>javax.servlet.jsp-api</artifactId>
            <version>2.3.1</version>
        </dependency>
        <!--如果使用JSTL必须添加该依赖-->
        <!--jstl标签依赖的jar包start-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>jstl</artifactId>
        </dependency>
```



#### 2.4.3 在pom.xml 的build 标签中要配置以下信息

```xml
     <build>
        <!--
            SpringBoot框架集成jsp，指定jsp文件编译的路径META-INF/resources
        -->
        <resources>
            <resource>
                <!--指定源文件路径-->
                <directory>src/main/webapp</directory>
                <!--指定编译的路径-->
                <!--指定编译到META-INF/resources，该目录不能随便写-->
                <targetPath>META-INF/resources</targetPath>
                <includes>
                    <include>*.*</include>
                </includes>
            </resource>

            <resource>
                <directory>src/main/resources</directory>
                <!--指定要把哪些文件编译进去，**表示webapp目录及子目录，*.*表示所有文件-->
                <includes>
                    <include>**/*.*</include>
                </includes>
            </resource>
        </resources>
    </build>

```

#### 2.4.4 在 application.properties 文件配置 Spring MVC 的视图展示为jsp，这里相当于Spring MVC 的配置 

```properties
#视图解析器
#其中：/ 表示目录为 src/main/webapp
spring.mvc.view.prefix=/
spring.mvc.view.suffix=.jsp

```

```yaml
#视图解析器
#其中：/ 表示目录为 src/main/webapp
spring:
	mvc:
		view:
			prefix: /
			suffix: .jsp
```



#### 2.4.5 在com.yyb.springboot.web 包下创建IndexController 类，并编写代码 

```java
package com.yyb.springboot.web;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;


@Controller
public class IndexController {

    @RequestMapping("/index")
    @ResponseBody
    public String index(Model model){
        model.addAttribute("data","SpringBoot框架集成JSP页面");
        return "index";
    }
}

```

#### 2.5.5 在jsp 中获取Controller 传递过来的数据

```jsp
<body>
<h1>${data}</h1>
</body>
```

#### 2.5.6 重新运行Application，通过浏览器访问测试

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot017.png)





## 第三章 Spring Boot 框架 Web 开发



### 3.1 Spring Boot 集成 Mybatis



SpringBoot框架集成MyBatis思路：
1.添加依赖（MyBatis、连接数据库的驱动）
2.连接数据库的配置
3.通过MyBatis逆向工程生成：数据持久层和实体bean

#### 3.1.1 实现步骤

（1）准备数据库

```mysql
DROP TABLE IF EXISTS t_student;
  
CREATE TABLE t_student 
(
   id                   INT(10)                        NOT NULL AUTO_INCREMENT,
   NAME                 VARCHAR(20)                    NULL,
   age                  INT(10)                        NULL,
   CONSTRAINT PK_T_STUDENT PRIMARY KEY clustered (id)
);
INSERT INTO t_student(NAME,age) VALUES("zhangsan",25);
INSERT INTO t_student(NAME,age) VALUES("lisi",28);
INSERT INTO t_student(NAME,age) VALUES("wangwu",23);
INSERT INTO t_student(NAME,age) VALUES("Tom",21);
INSERT INTO t_student(NAME,age) VALUES("Jck",55);
INSERT INTO t_student(NAME,age) VALUES("Lucy",27);
INSERT INTO t_student(NAME,age) VALUES("zhaoliu",75);

```

（2）创建项目

（3）Mybatis逆向工程

- 在maven中添加Mybatis逆向工程的插件

  ```xml
   <build>
          <plugins>
              <!--mybatis 代码自动生成插件-->
              <plugin>
                  <groupId>org.mybatis.generator</groupId>
                  <artifactId>mybatis-generator-maven-plugin</artifactId>
                  <version>1.3.6</version>
                  <configuration>
                      <!--配置文件的位置-->
                      <configurationFile>GeneratorMapper.xml</configurationFile>
                      <verbose>true</verbose>
                      <overwrite>true</overwrite>
                  </configuration>
              </plugin>
            </plugins>
    </build>
  ```

- 在根目录下创建GeneratorMapper.xml文件

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE generatorConfiguration
          PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
          "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
  <generatorConfiguration>
  
      <!-- 指定连接数据库的 JDBC 驱动包所在位置，指定到你本机的完整路径 -->
      <classPathEntry location="D:\maven\maven_repository\mysql\mysql-connector-java\5.1.6\mysql-connector-java-5.1.6.jar"/>
  
      <!-- 配置 table 表信息内容体，targetRuntime 指定采用 MyBatis3 的版本 -->
      <context id="tables" targetRuntime="MyBatis3">
          <!-- 抑制生成注释，由于生成的注释都是英文的，可以不让它生成 -->
          <commentGenerator>
              <property name="suppressAllComments" value="true"/>
          </commentGenerator>
  
  
          <!-- 配置数据库连接信息 -->
          <jdbcConnection driverClass="com.mysql.jdbc.Driver"
                          connectionURL="jdbc:mysql://127.0.0.1:3306/springdb"
                          userId="root"
                          password="fsy200195">
          </jdbcConnection>
          <!-- 生成 model 类，targetPackage 指定 model 类的包名， targetProject 指定
          生成的 model 放在 eclipse 的哪个工程下面-->
          <javaModelGenerator targetPackage="com.yyb.springboot.model"
                              targetProject="src/main/java">
              <property name="enableSubPackages" value="false"/>
              <property name="trimStrings" value="false"/>
          </javaModelGenerator>
  
          <!-- 生成 MyBatis 的 Mapper.xml 文件，targetPackage 指定 mapper.xml 文件的
          包名， targetProject 指定生成的 mapper.xml 放在 eclipse 的哪个工程下面 -->
          <sqlMapGenerator targetPackage="com.yyb.springboot.mapper"
                           targetProject="src/main/java">
              <property name="enableSubPackages" value="false"/>
          </sqlMapGenerator>
  
          <!-- 生成 MyBatis 的 Mapper 接口类文件,targetPackage 指定 Mapper 接口类的包
          名， targetProject 指定生成的 Mapper 接口放在 eclipse 的哪个工程下面 -->
          <javaClientGenerator type="XMLMAPPER"
                               targetPackage="com.yyb.springboot.mapper" targetProject="src/main/java">
              <property name="enableSubPackages" value="false"/>
          </javaClientGenerator>
  
          <!-- 数据库表名及对应的 Java 模型类名 -->
          <table tableName="t_student" domainObjectName="Student"
                 enableCountByExample="false"
                 enableUpdateByExample="false"
                 enableDeleteByExample="false"
                 enableSelectByExample="false"
                 selectByExampleQueryId="false"/>
      </context>
  </generatorConfiguration>
  ```

- 点击maven -> 逆向模块目录 -> Plugins -> mybatis-generator -> 双击mybatis-generator:generate运行生成

（4）在pom.xml 中添加相关jar 依赖

```xml
        <!--MyBatis整合SpringBoot的起步依赖-->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>2.0.0</version>
        </dependency>

        <!--MySQL的驱动依赖-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>
```

（5）在 Springboot 的核心配置文件 application.properties 中配置数据源

```properties
# 应用名称
spring.application.name=18_001_springboot

# 应用服务 WEB 访问端口
server.port=8080

#连接数据库信息 mysql8的jar包
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/springdb?useUnicode=true&characterEncoding=UTF-8&useJDBCCompliantTimezoneShift=true&useLegacyDatetimeCode=false&serverTimezone=Asia/Shanghai
spring.datasource.username=root
spring.datasource.password=fsy200195
#url+数据库强制使用UTF-8编码+serverTimezone
#在使用jdbc的时候，发现我的MySQ是8.0.19版本，在配置jdbc的url时，必须在数据库名后面加上serverTimezone参数，也就是
#jdbc:mysql://localhost:3306/数据库名?serverTimezone=Asia/Shanghai
#注意：网上有设置serverTimezone=UTC的，这个是有问题的，和中国时间相差8小时

```

（6）开发代码

- 在web 包下创建 StudentController 并编写代码

  ```java
  package com.yyb.springboot.web;
  
  import com.yyb.springboot.model.Student;
  import com.yyb.springboot.service.StudentService;
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.stereotype.Controller;
  import org.springframework.web.bind.annotation.RequestMapping;
  import org.springframework.web.bind.annotation.ResponseBody;
  
  @Controller
  public class StudentController {
  
      @Autowired
      private StudentService studentService;
  
      @RequestMapping("/student/detail")
      @ResponseBody
      public Object studentDetail(Integer id){
          Student student = studentService.queryStudentById(id);
          return student;
      }
  }
  
  ```

- 在service 包下创建 service 接口并编写代码

  ```java
  package com.yyb.springboot.service;
  
  import com.yyb.springboot.model.Student;
  
  public interface StudentService {
  
      Student queryStudentById(Integer id);
  }
  
  ```

- 在service.impl 包下创建service 接口并编写代码

  ```java
  package com.yyb.springboot.service.impl;
  
  import com.yyb.springboot.mapper.StudentMapper;
  import com.yyb.springboot.model.Student;
  import com.yyb.springboot.service.StudentService;
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.stereotype.Service;
  
  @Service
  public class StudentServiceImpl implements StudentService {
  
      @Autowired
      private StudentMapper studentMapper;
  
      @Override
      public Student queryStudentById(Integer id) {
          return studentMapper.selectByPrimaryKey(id);
      }
  }
  
  ```

- 如果在web 中导入service 存在报错，可以尝试进行如下配置解决

  ![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot019.png)

- 在Mybatis 反向工程生成的 StudentMapper 接口上加一个Mapper 注解
  @Mapper 作用：mybatis 自动扫描数据持久层的映射文件及DAO 接口的关系

  ```java
  @Mapper
  /**
   * 添加了@Mapper注解之后这个接口在编译时会生成相应的实现类
   *
   * 需要注意的是：这个接口中不可以定义同名的方法，因为会生成相同的id
   * 也就是说这个接口是不支持重载的
   * 代替mybatis的指定mapper文件位置
   */
  public interface StudentMapper {.......}
  ```

  

- 注意：默认情况下，Mybatis 的xml 映射文件不会编译到 target 的class 目录下，所以我们需要在 pom.xml 文件中配置resource

  ```xml
  <!-- 资源插件：处理src/main/java/目录中的xml-->
          <resources>
              <resource>
                  <directory>src/main/java</directory>
                  <includes>
                      <include>**/*.xml</include>
                  </includes>
              </resource>
              <resource>
                  <directory>src/main/resources</directory>
                  <includes>
                      <include>**/*.*</include>
                  </includes>
              </resource>
          </resources>
  ```

  

（7）启动Application 应用，浏览器访问测试运行

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot020.png)



#### 3.1.2 DAO其他开发方式

（8）在 运 行 的 主 类 上 添 加 注 解 包 扫 描@MapperScan("com.abc.springboot.mapper")

注释掉StudentMapper 接口上的@Mapper 注解

```java
//@Mapper
public interface StudentMapper {......}
```

在运行主类Application 上加@MapperScan("com.xxx.springboot.mapper")

```java
@SpringBootApplication
@MapperScan(basePackages = "com.yyb.springboot.mapper")
//Mybatis提供的注解：扫描数据持久层的mapper映谢配置文件,DAO接口上就不用加@Mapper
// basePackages通常指定到数据持久层包即可
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```



（9）将接口和映射文件分开

因为 SpringBoot 不能自动编译接口映射的 xml 文件，还需要手动在 pom 文件中指定，所以有的公司直接将映射文件直接放到resources 目录下 

- 在resources 目录下新建目录mapper 存放映射文件，将 StudentMapper.xml 文件移到resources/mapper 目录下

  ![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot021.png)

- 在 application.properties 配置文件中指定映射文件的位置，这个配置只有接口和映射文件不在同一个包的情况下，才需要指定

  ```properties
  # 指定Mybatis映射文件的路径
  mybatis.mapper-locations=classpath:mapper/*.xml
  
  ```



### 3.2 Spring Boot 事物支持



Spring Boot 使用事务非常简单，底层依然采用的是Spring 本身提供的事务管理

➢	在入口类中使用注解 @EnableTransactionManagement 开启事务支持
➢	在访问数据库的 Service 方法上添加注解 @Transactional 即可

#### 3.2,1 实现步骤（基于上面案例继续实现）

（10）在StudentController 中添加更新学生的方法

```java
@RequestMapping("/update")
    @ResponseBody
    public Object update(Integer id,String name){
        Student student = new Student();
        student.setId(id);
        student.setName(name);
        int modifyCount = studentService.modifyStudentById(student);
        int i=10/0;
        return "修改结果"+modifyCount;
    }

```

（11）在StudentService 接口中添加更新学生方法

```java
int modifyStudentById(Student student);

@Override
    public Student queryStudentById(Integer id) {
        Student student = studentMapper.selectByPrimaryKey(id);
        return student;
    }

```

（12）在 StudentServiceImpl 接口实现类中对更新学生方法进行实现，并构建一个异常，同时在该方法上加@Transactional 注解 

```java
 @Transactional//是声明式事务管理 编程中使用的注解
    @Override
    public Student queryStudentById(Integer id) {
        Student student = studentMapper.selectByPrimaryKey(id);
        return student;
    }

```

（13）在Application类上加@EnableTransactionManagement开启事务支持

<font color=red>@EnableTransactionManagement 可选，但是业务方法上必须添加@Transactional 事务才生效</font>

```java
@SpringBootApplication
@MapperScan(basePackages = "com.yyb.springboot.mapper")
@EnableTransactionManagement    //开启事务，可选项
public class Application {......}
```

（14）启动Application，通过浏览器访问进行测试



### 3.3 Spring Boot 下的Spring MVC



IDEA插件 RestfulToolkit

教程  https://blog.csdn.net/qq_22741461/article/details/81625079

Http 接口请求工具Postman 介绍
因为通过浏览器输入地址，默认发送的只能是 get 请求，通过Postman 工具，可以模拟发送不同类型的请求，并查询结果，在安装的时候，有些机器可能会需要安装MicroSort .NET Framework 

教程 https://blog.csdn.net/weixin_44675537/article/details/112887037?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522162660343016780366541510%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=162660343016780366541510&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-112887037.first_rank_v2_pc_rank_v29&utm_term=Postman&spm=1018.2226.3001.4187

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot022.png)

Spring Boot 下的 Spring MVC 和之前的Spring MVC 使用是完全一样的，主要有以下注解

#### 3.3.1 @Controller

Spring MVC 的注解，处理http 请求

#### 3.3.2 @RestController

pring 4 后新增注解，是@Controller 注解功能的增强 
是 @Controller 与@ResponseBody 的组合注解 
如果一个Controller 类添加了@RestController，那么该Controller 类下的所有方法都相当于添加了@ResponseBody 注解。用于返回字符串或 json 数据

#### 3.3.3 @RequestMapping（常用）

支持Get 请求，也支持 Post 请求

#### 3.3.4 @GetMapping

RequestMapping 和Get 请求方法的组合   
只支持Get 请求 
Get 请求主要用于查询操作 

#### 3.3.5 @PostMapping

RequestMapping 和Post 请求方法的组合   
只支持Post 请求 
Post 请求主要用户新增数据 

#### 3.3.6 @PutMapping

RequestMapping 和Put 请求方法的组合 
只支持Put 请求 
Put 通常用于修改数据 

#### 3.3.7 @DeleteMapping

RequestMapping 和 Delete 请求方法的组合 
只支持Delete 请求 
通常用于删除数据 

```java
package com.yyb.springboot.web;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.*;

//@Controller
@RestController//如果该方法只响应json 就可以使用该注解。相当于类上加@Controller+方法上加@ResponseBody
public class IndexController {
    /**
     * 该方法即支付get请求，也支持post请求
     * @return
     */
    @RequestMapping("/index")
    //@ResponseBody
    public Object index(){
        return "index";
    }

    /**
     * 该方法只支持get请求
     * @return
     */
    @RequestMapping(value = "/index1",method = RequestMethod.GET)
    //@ResponseBody
    public Object index1(){
        return "index1 get method";
    }

    /**
     * 该方法只支持get请求
     * @return
     * 通常使用在查询操作
     */
    @GetMapping(value = "/index2")
    //@ResponseBody
    public Object index2(){
        return "index2 get method";
    }

    /**
     * 该方法只支持POST请求
     * @return
     */
    @RequestMapping(value = "/index3",method = RequestMethod.POST)
    public Object index3(){
        return "index3 post method";
    }

    /**
     * 该方法只支持post请求，通常用于新增操作
     * @return
     */
    @PostMapping("/index4")
    public Object index4(){
        return "index3 post method";
    }

    /**
     * 该方法只支持PUT请求
     * @return
     */
    @RequestMapping(value = "/index5",method = RequestMethod.PUT)
    public Object index5(){
        return "index5 put method";
    }

    /**
     * 该方法只支持put请求，通常用于修改操作
     * @return
     */
    @PutMapping("/index6")
    public Object index6(){
        return "index6 put method";
    }

    /**
     * 该方法只支持Delete请求
     * @return
     */
    @RequestMapping(value = "/index7",method = RequestMethod.DELETE)
    public Object index7(){
        return "index7 delete method";
    }

    /**
     * 该方法只支持Delete请求,通常用于删除操作
     * @return
     */
    @DeleteMapping(value = "/index8")
    public Object index8(){
        return "index8 only deleteMethod!!";
    }

}

```



### 3.4 Spring Boot 实现RESTful



#### 3.4.1 认识RESTFul

REST（英文：Representational State Transfer，简称REST） 
一种互联网软件架构设计的风格，但它并不是标准，它只是提出了一组客户端和服务器交互时的架构理念和设计原则，基于这种理念和原则设计的接口可以更简洁，更有层次，REST这个词，是Roy Thomas Fielding 在他2000 年的博士论文中提出的。

任何的技术都可以实现这种理念，如果一个架构符合 REST 原则，就称它为 RESTFul 架构

比如我们要访问一个 http 接口：http://localhost:8080/boot/order?id=1021&status=1 
采用RESTFul 风格则 http 地址为：http://localhost:8080/boot/order/1021/1 

#### 3.4.2 Spring Boot 开发RESTFul

Spring boot 开发 RESTFul 主要是几个注解实现

（1）@PathVariable

获取url中的数据 <font color=red>该注解是实现RESTFUl最主要的一个注解</font>

（2）@PostMapping

接收和处理Post方式的请求

（3）@DeleteMapping

接收delete方式的请求，可以使用GetMapping代替

（4）@PutMapping

接收Put方式的请求，可以用PostMapping代替

（5）@GetMapping

接收get 方式的请求

```java
@Controller
public class StudentController {

    /**
     * 正常访问一个 http 接口
     * @param id
     * @return
     */
    @RequestMapping("/student/detail")
    @ResponseBody
    public Object studentDetail(Integer id){
        return "ID->"+id;
    }
    //http://localhost:8080/student/detail?id=111
    //ID->111

    /**
     * 采用RESTFul 风格 Get请求方式 并只带id参数的 http 地址
     * @param id
     * @return
     */
    @GetMapping("/student/detail/{id}")
    @ResponseBody
    public Object studentDetail1(@PathVariable("id") Integer id){
        return "ID->"+id;
    }
    //http://localhost:8080/student/detail/111
    //ID->111

    /**
     * 采用RESTFul 风格 Get请求方式 并带id,name参数的 http 地址
     * @param id
     * @param name
     * @return
     */
    @GetMapping("/student/detail/{id}/{name}")
    @ResponseBody
    public Object studentDetail2(@PathVariable("id") Integer id,
                                 @PathVariable("name") String name){
        return "ID->"+id+",NAME->"+name;
    }
    //http://localhost:8080/student/detail/111/zhangsan
    //ID->111,Name->zhangsan
    
}

```

好处

➢	传递参数变简单了
➢	服务提供者对外只提供了一个接口服务，而不是传统的 CRUD四个接口



#### 3.4.3 请求冲突

➢	改路径
➢	改请求方式

创建RESTfulController 类 进行测试说明

```java
@RestController
public class RESTfulController {
 /**
 * id:订单标识
 * status：订单状态
 * 请求路径：
http://localhost:9090/015-springboot-restful-url-conflict/springBoot/orde
r/1/1001
 * @param id
 * @param status
 * @return
 */
 @GetMapping(value = "/springBoot/order/{id}/{status}")
 public Object queryOrder(@PathVariable("id") Integer id,
 @PathVariable("status") Integer status) {
 Map<String,Object> map = new HashMap<String,Object>();
 map.put("id",id);
 map.put("status",status);
 return map;
 }
 /**
 * id:订单标识
 * status：订单状态
 * 请求路径：
http://localhost:9090/015-springboot-restful-url-conflict/springBoot/1/or
der/1001
 * @param id
 * @param status
 * @return
 */
 @GetMapping(value = "/springBoot/{id}/order/{status}")
 public Object queryOrder1(@PathVariable("id") Integer id,
 @PathVariable("status") Integer status) {
 Map<String,Object> map = new HashMap<String,Object>();
 map.put("id",id);
 map.put("status",status);
 return map;
 }
 /**
 * id:订单标识
 * status：订单状态
 * 请求路径：
http://localhost:9090/015-springboot-restful-url-conflict/springBoot/1001
/order/1
 * @param id
 * @param status
 * @return
 */
 @GetMapping(value = "/springBoot/{status}/order/{id}")
 public Object queryOrder2(@PathVariable("id") Integer id,
 @PathVariable("status") Integer status) {
 Map<String,Object> map = new HashMap<String,Object>();
 map.put("id",id);
 map.put("status",status);
 return map;
 }
 /**
 * id:订单标识
 * status：订单状态
 * 请求路径：
http://localhost:9090/015-springboot-restful-url-conflict/springBoot/1001
/order/1
 * @param id
 * @param status
 * @return
 */
  @PostMapping(value = "/springBoot/{status}/order/{id}")
 public Object queryOrder3(@PathVariable("id") Integer id,
 @PathVariable("status") Integer status) {
 Map<String,Object> map = new HashMap<String,Object>();
 map.put("id",id);
 map.put("status",status);
 return map;
 }
 /**
 * query1 和 query2 两个请求路径会发生请求路径冲突问题
 * query3 与 query1 和 query2 发生请求冲突
 * 注意：虽然两个路径写法改变了，但是由于传递的两个参数都是 int 值，所以不知道该交给
哪个请求进行处理
 * 就会出现匹配模糊不清的异常，所以要想解决冲突，有两种方式：
 * 1.修改请求路径
 * 2.修改请求方式
 */
}
```



#### 3.4.4 RESTFul原则

➢	增post 请求、删 delete 请求、改put 请求、查 get 请求
➢	<font color=red>请求路径不要出现动词</font>

例如：查询订单接口
/boot/order/1021/1（推荐） 
/boot/queryOrder/1021/1（不推荐）

➢	<font color=red>分页、排序等操作，不需要使用斜杠传参数</font>
例如：订单列表接口
/boot/orders?page=1&sort=desc 
一般传的参数不是数据库表的字段，可以不采用斜杠

### 3.5 Spring Boot 集成Redis

<font color=red>待补充</font>



### 3.6 Spring Boot 集成Dubbo

阿 里 巴 巴 提 供 了 dubbo 集成 springBoot 开 源 项 目 ， 可 以 到 GitHub 上https://github.com/alibaba/dubbo-spring-boot-starter 查看入门教程 

SpringBoot集成dubbo思路：
1.接口工程
	a.存放实体bean和业务接口
	b.maven java工程
2.服务提供者
	a.SpringBoot web工程
	b.实现业务接口中的接口
	c.集成MyBatis、集成Redis
3.服务消费者
	a.SpringBoot web工程
	b.处理从浏览器客户端发送的请求
	c.消费服务提供者所提供的服务

#### 3.6.1 基本集成步骤

（1） 开发Dubbo 服务接口

项目名称：24-springboot-interface

按照 Dubbo 官方开发建议，创建一个接口项目，该项目只定义接口和 model 类

创建普通java Maven 项目，dubbo 服务接口工程 创建SomeService接口

```java
package com.yyb.springboot.dubbo.service;

public interface SomeService {
    String hello();
}

```

（2）开发Dubbo 服务提供者

项目名称：24-springboot-provider

创建SpringBoot 框架的WEB 项目

加入Dubbo 集成SpringBoot 的起步依赖,加入Dubbo 集成SpringBoot 的起步依赖,加入 zookeeper 的客户端依赖,加入Dubbo 接口依赖

```xml
<!--Springboot框架web项目的起步依赖-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <!--Dubbo整合springboot框架的起步依赖-->
        <dependency>
            <groupId>com.alibaba.spring.boot</groupId>
            <artifactId>dubbo-spring-boot-starter</artifactId>
            <version>2.0.0</version>
        </dependency>
        <!--zookeeper注册中心-->
        <dependency>
            <groupId>com.101tec</groupId>
            <artifactId>zkclient</artifactId>
            <version>0.11</version>
        </dependency>
        <!--接口工程-->
        <dependency>
            <groupId>com.yyb.springboot</groupId>
            <artifactId>24_springboot_interface</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
```

在Springboot 的核心配置文件

```properties
# 应用服务 WEB 访问端口
server.port=8081
#配置dubbo信息
#声明服务提供者名称
spring.application.name=24_springboot_provider
#服务提供者工程需要声明自己是服务提供者工程
spring.dubbo.server=true
#指定注册中心
spring.dubbo.registry=zookeeper://localhost:2181

```

编写Dubbo 的接口实现类<font color=red>//@Service  相当于dubbo:service interface="" ref="" version="" timeout=""</font>

```java
package com.yyb.springboot.dubbo.service.impl;

import com.alibaba.dubbo.config.annotation.Service;
import com.yyb.springboot.dubbo.service.SomeService;
import org.springframework.stereotype.Component;
//@Component  相当于@Service 放入spring容器中
@Component
//@Service  相当于dubbo:service interface="" ref="" version="" timeout=""
@Service(interfaceClass = SomeService.class,version = "1.0.0",timeout = 35000)
public class SomeServiceImpl implements SomeService{

    @Override
    public String hello(){
        return "Hello SpringBoot集成Dubbo";
    }
}

```

在SpringBoot 入口程序类上加开启Dubbo 配置支持注解  <font color=red>@EnableDubboConfiguration //开启dubbo配置</font>

```java
package com.yyb.springboot;

import com.alibaba.dubbo.spring.boot.annotation.EnableDubboConfiguration;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
@EnableDubboConfiguration //开启dubbo配置
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

（3）开发Dubbo 服务消费者

项目名称：24-springboot-consumer

创建SpringBoot 框架的WEB 项目

加入Dubbo 集成SpringBoot 的起步依赖,加入Dubbo 集成SpringBoot 的起步依赖,加入 zookeeper 的客户端依赖,加入Dubbo 接口依赖

```xml
<!--Springboot框架web项目的起步依赖-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <!--Dubbo整合springboot框架的起步依赖-->
        <dependency>
            <groupId>com.alibaba.spring.boot</groupId>
            <artifactId>dubbo-spring-boot-starter</artifactId>
            <version>2.0.0</version>
        </dependency>
        <!--zookeeper注册中心-->
        <dependency>
            <groupId>com.101tec</groupId>
            <artifactId>zkclient</artifactId>
            <version>0.11</version>
        </dependency>
        <!--接口工程-->
        <dependency>
            <groupId>com.yyb.springboot</groupId>
            <artifactId>24_springboot_interface</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
```

在Springboot 的核心配置文件

```properties
# 应用服务 WEB 访问端口
server.port=8080
#设置dubbo配置
#声明服务消费者名称
spring.application.name=24_springboot_consumer
#指定注册中心
spring.dubbo.registry=zookeeper://localhost:2181

```

编写一个Controller 类，调用远程的Dubbo 服务  <font color=red>//@Reference 相当于 dubbo:reference interface="" version="" check=false</font>

```java
package com.yyb.springboot.dubbo.web;

import com.alibaba.dubbo.config.annotation.Reference;
import com.yyb.springboot.dubbo.service.SomeService;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class SomeController {
    //@Reference 相当于 dubbo:reference interface="" version="" check=false
    @Reference(interfaceClass = SomeService.class,version = "1.0.0",check = false)
    private SomeService someService;

    @RequestMapping("/hello")
    @ResponseBody
    public Object hello(){
        //调用远程接口服务
        String hello = someService.hello();
        return hello;
    }
}

```

在SpringBoot 入口程序类上加开启Dubbo 配置支持注解  <font color=red>@EnableDubboConfiguration //开启dubbo配置</font>

````java
package com.yyb.springboot;

import com.alibaba.dubbo.spring.boot.annotation.EnableDubboConfiguration;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
@EnableDubboConfiguration //开启dubbo配置
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
````

开启zookeeper注册中心

运行服务提供者和服务消费者项目，在浏览器输入地址查看

核心三个注解<font color=red> @Service @Reference @EnableDubboConfiguration</font>





## 第四章 Spring Boot 非 Web 应用程序



在 Spring Boot 框架中，要创建一个非 Web 应用程序（纯 Java 程序），有两种方式 



### 4.1 方式一：直接在main 方法中，根据SpringApplication.run()方法获取返回的Spring 容器对象，再获取业务bean 进行调用 



#### 4.1.1 创建一个Spring Boot Module

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot023.png)

#### 4.1.2 创建一个演示 UserService 接口及实现类

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot024.png)

SomeService.java 接口

```java
public interface SomeService {
    String hello();
}

```

SomeServiceImpl.java实现类

```java
@Service
public class SomeServiceImpl implements SomeService {
    @Override
    public String hello() {

        return "Hello SpringBoot Java Project-1";
    }
}

```

#### 4.1.3 在Application 类的main 方法中，获取容器，调用业务bean

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        //run方法返回的ConfigurableApplicationContext就相当于之前的ClasspathXmlApplicationContext spring容器对象
        ConfigurableApplicationContext configurableApplicationContext = SpringApplication.run(Application.class, args);
        //获取spring容器对象
        SomeService someserviceimpl = (SomeService) configurableApplicationContext.getBean("someServiceImpl");
        //调用业务方法
        String hello = someserviceimpl.hello();
        System.out.println(hello);
    }

}
```

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot025.png)



### 4.2 方式二：Spring boot 的入口类实现CommandLineRunner 接口



#### 4.2.1 创建一个SomeService接口及实现类

同上4.1.2

#### 4.2.2 修改启动类

将原有 Application 类的@SpringBootApplication 注解注释掉，复制一个新的 Application 取名为Application2，实现CommandLineRunner 接口 

```java
package com.yyb.springboot;

import com.yyb.springboot.service.SomeService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application implements CommandLineRunner {

    //第二步：通过容器获取 bean，并注入给 userService
    @Autowired
    private SomeService someService;

    public static void main(String[] args) {
        //第一步：SpringBoot的启动程序，会初始化 spring容器
        SpringApplication.run(Application.class, args);
    }

    //覆盖接口中的 run方法
    @Override
    public void run(String... args) throws Exception {
        //第三步：容器启动后调用 run方法，在该方法中调用业务方法
        String sayhello = someService.hello();
        System.out.println(sayhello);
    }
}

```

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot026.png)



### 4.3 小Tip



#### 4.3.1 关闭SpringBoot Logo 图标及启动日志

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication springApplication = new SpringApplication(Application.class);

        ///关闭启动 logo的输出
        springApplication.setBannerMode(Banner.Mode.OFF);
        springApplication.run(args);
    }

}
```



#### 4.3.2 修改启动的 logo 图标

在src/main/resources 放入banner.txt 文件，该文件名字不能随意，文件中的内容就是要输出的 logo ； 可 以 利 用 网 站 生 成 图 标 ： https://www.bootschool.net/ascii 或者http://patorjk.com/software/taag/，将生成好的图标文字粘贴到banner.txt 文件中，然后将关闭logo 输出的语句注释，启动看效果 
修改后LOGO 

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot027.png)



## 第五章 Spring Boot 使用拦截器



### 5.1 回顾拦截器Spring MVC 使用拦截器的步骤

➢	自定义拦截器类，实现HandlerInterceptor 接口
➢	注册拦截器类

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot028.png)



➢ 按照 SpringMVC 方式编写一个拦截器类，实现 HandlerInterceptor 接口

```java
public class UserInterceptor implements HandlerInterceptor {
 @Override
 public boolean preHandle(HttpServletRequest request,
HttpServletResponse response, Object handler) throws Exception {
 //编写登录拦截业务逻辑
 //返回 true 通过
 //返回 false 被拦截
 System.out.println("--------登录拦截器---------");
 return true;
 }
 @Override
 public void postHandle(HttpServletRequest request,
HttpServletResponse response, Object handler, ModelAndView modelAndView)
throws Exception {
 }
 @Override
 public void afterCompletion(HttpServletRequest request,
HttpServletResponse response, Object handler, Exception ex) throws
Exceptio
```



### 5.2 Spring Boot 使用拦截器步骤



#### 5.2.1 创建一个 Spring Boot框架Web项目 

#### 5.2.2 实现一个登录拦截器

```java
package com.yyb.springboot.interceptor;

import com.yyb.springboot.model.User;
import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class UserInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        //拦截的规则
        //从session中获取用户的信息
        User user =(User) request.getSession().getAttribute("user");

        //判断用户是否为空
        if (user == null){
            response.sendRedirect(request.getContextPath() + "/user/page/login");
            return false;
        }
        return true;
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {

    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {

    }
}

```

#### 5.2.3 创建登录的id和name的javabean

```java
package com.yyb.springboot.model;

public class User {
    private Integer id;
    private String name;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

```

#### 5.2.4 创建一个控制层

```java
package com.yyb.springboot.web;


import com.yyb.springboot.model.User;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import javax.servlet.http.HttpServletRequest;

@RestController
public class IndexController {


    /**
     * 无需用户登录
     * @return
     */
    @RequestMapping(value = "/index")
    public String index(){
        return "INDEX";
    }


    /**
     * 无需用户登录
     * @return
     */
    @RequestMapping(value = "/user/page/login")
    public String loginPage(){
        return "Login Page";
    }

    @RequestMapping(value = "/user/login")
    public String login(HttpServletRequest request){
        User user = new User();
        user.setId(1);
        user.setName("lisi");

        request.getSession().setAttribute("user",user);

        return "Logged";
    }

    /**
     * 需要用户是登录状态
     * @return
     */
    @RequestMapping(value = "/user/center")
    public String center(){
        return "User Center";
    }
}

```

#### 5.2.5 @Configuration 定义配置类-拦截器

在项目中创建一个 config 包，创建一个配置类 InterceptorConfig ，并实现WebMvcConfigurer 接口， 覆盖接口中的 addInterceptors 方法，并为该配置类添加@Configuration 注解，标注此类为一个配置类，让 Spring Boot 扫描到，这里的操作就相当于SpringMVC 的注册拦截器 ，@Configuration 就相当于一个 applicationContext-mvc.xml

```java
package com.yyb.springboot.config;


import com.yyb.springboot.interceptor.UserInterceptor;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration //只要加上@Configuration，就说明此类为一个配置类，相当于xml文件
public class SystemConfig implements WebMvcConfigurer {
    //重写接口添加拦截器的方法
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        //定义要拦截的路径
        String[] addPathPatterns = {
                "/user/**"
        };

        //排除不需要拦截的路径
        String [] excludePathPatterns = {
                "/user/page/login",
                "/user/login"
        };


        registry.addInterceptor(new UserInterceptor()) //添加要注册的拦截器对象
                .addPathPatterns(addPathPatterns)//添加需要拦截的路径
                .excludePathPatterns(excludePathPatterns);//添加不需要拦截器对象
    }
}

```

#### 5.2.6 测试

运行application文件的main方法后，在网页中输入.../index网页会显示INDEX（未登录），输入.../user/page/login网页显示Login Page（登录界面）。输入.../user/center由于没有登录拦截器会自动跳转到.../user/page/login页面（登录界面），输入.../user/login网页显示Logged表示已登录的状态，如果再输入.../user/center页面会显示User Center，因为在登录的状态下拦截器不会拦截。



## 第6章 Spring Boot 中使用Servlet（了解） 



### 6.1 方式一 通过注解扫描方式实现 

#### 6.1.1 通过注解的方式创建一个Servlet

- 创建Myservlet.class

  ```java
  package com.yyb.springboot.servlet;
  
  import javax.servlet.ServletException;
  import javax.servlet.annotation.WebServlet;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import java.io.IOException;
  
  @WebServlet("/myServlet")
  public class MyServlet extends HttpServlet {
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          response.getWriter().println("MyServlet-1");//不仅可以打印输出文本格式的（包括html标签），还可以将一个对象以默认的编码方式转换为二进制字节输出
          response.getWriter().flush();
          response.getWriter().close();
      }
  
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          doPost(request, response);
      }
  }
  
  ```

- 在 主 应 用 程 序 Application类上添加@ServletComponentScan("com.yyb.springboot.servlet")

  ```java
  package com.yyb.springboot;
  
  import org.springframework.boot.SpringApplication;
  import org.springframework.boot.autoconfigure.SpringBootApplication;
  import org.springframework.boot.web.servlet.ServletComponentScan;
  
  @SpringBootApplication
  @ServletComponentScan("com.yyb.springboot.servlet")
  public class Application {
  
      public static void main(String[] args) {
          SpringApplication.run(Application.class, args);
      }
  
  }
  
  ```



### 6.2 方式二 通过SpringBoot 的配置类实现（组件注册） 

#### 6.2.1 创建一个普通的Servlet

```java
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;


public class MyServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.getWriter().println("MyServlet-2");
        response.getWriter().flush();
        response.getWriter().close();
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }
}

```

#### 6.2.2 编写一个Spring Boot 的配置类，在该类中注册Servlet 

```java
package com.yyb.springboot.config;

import com.yyb.springboot.servlet.MyServlet;
import org.springframework.boot.web.servlet.ServletRegistrationBean;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration //声明此类为一个配置类，相当于一个xml配置文件
public class MyConfig {

    //@Bean注解是方法级别的一个注解
    //@Bean相当于 <beans><bean></bean></beans>
    @Bean
    public ServletRegistrationBean myServletRegistrationBean(){

        //创建一个servlet注册bean对象
        //将自定义 servlet注册到注册 Servlet类中，并指定访问路径
        ServletRegistrationBean servletRegistrationBean = new ServletRegistrationBean(new MyServlet(),"/myservlet2","/myservlet3");

        return servletRegistrationBean;
    }

}
```



## 第七章 Spring Boot 中使用Filter（了解）



### 7.1 方式一 通过注解方式实现



#### 7.1.1 创建项目

#### 7.1.2 通过注解方式创建一个Filer

```java
package com.yyb.springboot.filter;

import javax.servlet.*;
import javax.servlet.annotation.WebFilter;
import java.io.IOException;

@WebFilter("/myFilter")
public class Myfilter implements Filter {
    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        System.out.println("----------您已进入过滤器----------");
        chain.doFilter(request,response);
    }
}
```

#### 7.1.3 在 主 应 用 程 序 Application 类上添加@ServletComponentScan("basePackages = "com.yyb.springboot.filter")

```java
package com.yyb.springboot;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.web.servlet.ServletComponentScan;

@SpringBootApplication
@ServletComponentScan(basePackages = "com.yyb.springboot.filter")
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```



### 7.2 方式二 通过Spring Boot 的配置类实现



#### 7.2.1 创建项目

#### 7.2.2 创建一个普通的Filter

```java
package com.yyb.springboot.filter;

import javax.servlet.*;
import java.io.IOException;

public class MyFilter implements Filter {
    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        System.out.println("----------您已进入过滤器222----------");
        chain.doFilter(request,response);
    }
}

```

#### 7.2.3 编写一个Spring Boot 的配置类，在该类中注册Filter 

```java
package com.yyb.springboot.config;

import com.yyb.springboot.filter.MyFilter;
import org.springframework.boot.web.servlet.FilterRegistrationBean;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration //定义为配置类
public class MyConfig {

    @Bean
    public FilterRegistrationBean myFilterRegistrationBean(){

        FilterRegistrationBean filterRegistrationBean = new FilterRegistrationBean();
        filterRegistrationBean.setFilter(new MyFilter());//注册过滤器
        filterRegistrationBean.addUrlPatterns("/myFilter");//添加过滤路径

        return filterRegistrationBean;
    }
}

```



## 第八章 Spring Boot 项目配置字符编码



### 8.1 方式一 使用传统的Spring 提供的字符编码过滤器



#### 8.1.1  创建项目

#### 8.1.2 创建一个Servlet

```java
package com.yyb.springboot.servlet;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/myServlet")
public class MyServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //强制设置浏览器客服端的字符编码
        response.setContentType("text/html;charset=UTF-8");
        response.getWriter().println("HelloWorld！世界你好！");//不仅可以打印输出文本格式的（包括html标签），还可以将一个对象以默认的编码方式转换为二进制字节输出
        response.getWriter().flush();
        response.getWriter().close();
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }
}

```

#### 8.1.3 创建配置类SystemConfig

```java
package com.yyb.springboot.config;

import org.springframework.boot.web.servlet.FilterRegistrationBean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.filter.CharacterEncodingFilter;

@Configuration //定义为配置类
public class MyConfig {

    public FilterRegistrationBean myFilterRegistrationBean(){
        //创建一个字符编码过滤器对象
        //CharacterEncoding是由 Spring提供的一个字符编码过滤器，之前是配置在web.xml文件中
        CharacterEncodingFilter characterEncodingFilter = new CharacterEncodingFilter();
        //强制使用指定字符编码
        characterEncodingFilter.setForceEncoding(true);
        //设置指定字符编码
        characterEncodingFilter.setEncoding("utf-8");
        //定义过滤器对象
        FilterRegistrationBean filterRegistrationBean = new FilterRegistrationBean();
        //设置字符编码过滤器
        filterRegistrationBean.setFilter(characterEncodingFilter);
        //设置字符编码过滤器路径
        filterRegistrationBean.addUrlPatterns("/**");
        return filterRegistrationBean;
    }
}

```

#### 8.1.4 关闭SpringBoot 的http 字符编码支持<font color=red>(spring boot版本是2.3.4以下的才用)</font>

```properties
#关闭 springboot的 http字符编码支持
#只有关闭该选项后，spring字符编码过滤器才生效
spring.http.encoding.enabled=false
```

#### 8.1.5 测试

无字符编码过滤器

```
HelloWorld??????
```

使用字符编码过滤器

```
HelloWorld！世界你好！ 
```

<font color=red>在servlet 中添加response.setContextType(“text/html;charset=utf-8”)指定浏览器编码方式</font>



### 8.2 方式二 在application.properties 中配置字符编码<font color=red>(spring boot版本是2.2.2以下的才用)</font>

#### 8.2.1 创建项目

#### 8.2.2 SpringBoot 核心配置文件添加字符编码设置

从 springboot 1.4.2 之后开始新增的一种字符编码设置

```properties
#设置请求响应的字符编码
spring.http.encoding.enabled=true
spring.http.encoding.force=true
spring.http.encoding.charset=UTF-8
```

#### 8.2.3 创建Servlet

```java
public class MyServlet extends HttpServlet {
 @Override
 protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws
ServletException, IOException {
 resp.getWriter().print("Hello World!世界您真好！");
 resp.setContentType("text/html;character=utf-8");
 resp.getWriter().flush();
 resp.getWriter().close();
 }
 @Override
 protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws
ServletException, IOException {
 doGet(req,resp);
 }
}
```

#### 8.2.4 创建配置类ServletConfig

```java
@Configuration
public class ServletConfig {
 @Bean
 public ServletRegistrationBean myServletRegistration() {
 ServletRegistrationBean servletRegistrationBean =
 new ServletRegistrationBean(new MyServlet(),"/myservlet");
 return servletRegistrationBean;
 }
}

```



## 第九章 Spring Boot 打包与部署



### 9.1 Spring Boot 程序 war 包部署

#### 9.1.1 方法一直接在Spring Boot项目创建是改成war包

（1）创建 Spring Boot Web 项目

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot029.png)

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot030.png)

（2）创建Controller层

```xml
package com.yyb.springboot.web;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class IndexConTroller {

    @RequestMapping("/index")
    @ResponseBody
    public Object index(){
        return "index";
    }
}

```



（3）添加忽略web.xml配置文件

```xml
           <!--表明忽略web.xml配置文件-->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>2.4</version>
                <configuration>
                    <failOnMissingWebXml>false</failOnMissingWebXml>
                </configuration>
            </plugin>
```

（4）在 pom.xml 的 build 标签下通过 finalName 指定打 war的名字

```xml
        <!--指定打 war包的名字-->
        <finalName>springboot</finalName>
```

（5）通过Maven package 命令打war 包到target 目录下

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot032.png)

（6）将war复制到Tomcat的apache-tomcat-9.0.13\webapps目录下，然后在bin下双击startup.bat

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot033.png)

（7）在网页输入http://localhost:8080/（项目名）/index 查看是否允许成功

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot034.png)



#### 9.1.2 方法二 Spring Boot项目是jar改成打包是war

（1）创建 Spring Boot Web 项目

（2） 添加SpringBoot 解析jsp 依赖<font color=red>（会报错，如果将war部署到Tomcat之后报错大概就是没加servlet两个依赖俺也不知道怎么解决）</font>

```xml
<!--SpringBoot 只解析 JSP 页面依赖-->
<dependency>
 <groupId>org.apache.tomcat.embed</groupId>
 <artifactId>tomcat-embed-jasper</artifactId>
</dependency>
        <!--如果要使用servlet必须添加该以下两个依赖-->
        <!-- servlet依赖的jar包-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
        </dependency>
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>javax.servlet.jsp-api</artifactId>
            <version>2.3.1</version>
        </dependency>
```

（3） 在pom.xml 文件中配置jsp 文件解析目录

```xml
     <build>
        <!--
            SpringBoot框架集成jsp，指定jsp文件编译的路径META-INF/resources
        -->
        <resources>
            <resource>
                <!--指定源文件路径-->
                <directory>src/main/webapp</directory>
                <!--指定编译的路径-->
                <!--指定编译到META-INF/resources，该目录不能随便写-->
                <targetPath>META-INF/resources</targetPath>
                <includes>
                    <include>*.*</include>
                </includes>
            </resource>

```

（4） 创建webapp 并指定为web 资源文件夹

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot031.png)

（5） 在application.properties 配置文件中配置jsp 的前后缀

```properties
#设置 jsp 的前/后缀
spring.mvc.view.prefix=/
spring.mvc.view.suffix=.jsp
```

（6） 创建IndexController 提供方法分别返回字符串及跳转页面

```java
package com.yyb.springboot.web;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class IndexConTroller {

    @RequestMapping(value = "/index")
    public String index(Model model) {
        model.addAttribute("data","SpringBoot");
        return "index";
    }

}

```

（7） 在src/main/webapp 目录下创建index.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
${data},打 war 包!
</body>
</html>

```

（8）程序入口类需扩展继承 SpringBootServletInitializer 类并覆盖configure 方法

```java
package com.yyb.springboot;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.builder.SpringApplicationBuilder;
import org.springframework.boot.web.servlet.support.SpringBootServletInitializer;

@SpringBootApplication
public class Application extends SpringBootServletInitializer {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
    @Override
    protected SpringApplicationBuilder
    configure(SpringApplicationBuilder builder) {
        //参数为当前 SpringBoot 启动类
        return builder.sources(Application.class);
    }
}

```

（9）在 pom.xml 中添加（修改）打包方式为war

```xml
<modelVersion>4.0.0</modelVersion>
    <groupId>com.yyb.springboot</groupId>
    <artifactId>20_002_springboot</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>war</packaging><!--修改打包方式-->
    <name>20_002_springboot</name>
    <description>Demo project for Spring Boot</description>
```

（10）在 pom.xml 中配置springboot 打包的插件(默认自动加)

```xml
           <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <version>2.3.7.RELEASE</version>
                <configuration>
                    <mainClass>com.yyb.springboot.Application</mainClass>
                </configuration>
                <executions>
                    <execution>
                        <id>repackage</id>
                        <goals>
                            <goal>repackage</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
```

（11）在pom.xml 中配置将配置文件编译到类路径

```xml
     <!--src/main/resources 下的所有配置文件编译到 classes 下面去-->
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.*</include>
                </includes>
            </resource>
        </resources>

```

（12）在 pom.xml 的 build 标签下通过 finalName 指定打 war的名字

```xml
        <!--指定打 war包的名字-->
        <finalName>springboot</finalName>
```

（13）添加忽略web.xml配置文件

```xml
           <!--表明忽略web.xml配置文件-->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>2.4</version>
                <configuration>
                    <failOnMissingWebXml>false</failOnMissingWebXml>
                </configuration>
            </plugin>
```

（14）通过Maven package 命令打war 包到target 目录下

（15）将war复制到Tomcat的apache-tomcat-9.0.13\webapps目录下，然后在bin下双击startup.bat

流程与方法一基本一致

遇到[严重 [ajp-nio-8009-exec-3\] org.apache.coyote.ajp.AjpMessage.processHeader Invalid message received with signature](https://www.cnblogs.com/jnhs/p/13403202.html)

解决方法： https://blog.csdn.net/weixin_42184538/article/details/108416029



### 9.2 Spring Boot 程序与Jar包与运行

为SpringBoot 默认打包方式就是 jar 包,所以我们直接执行 Maven 的package 命令就行了

#### 9.2.1 创建IndexController 

```java
package com.yyb.springboot.web;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class IndexConTroller {

    @RequestMapping("/index")
    @ResponseBody
    public Object index(){
        return "index";
    }
}

```

#### 9.2.2 在 pom.xml 的 build 标签下通过 finalName 指定打 war的名字

```xml
        <!--指定打 war包的名字-->
        <finalName>springboot</finalName>
```

#### 9.2.3 修改pom.xml 文件中打包插件的版本 
<font color=red>此案例不是用jsp达成jar但是如果用jsp则要修改默认 SpingBoot 提供的打包插件版本为 2.2.2.RELEASE，这个版本打的 jar 包 jsp 不能访问，我们这里修改为1.4.2.RELEASE（其它版本测试都有问题）</font>

```java
              <!-- SpringBoot提供打包编译插件 -->
              </plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <version>2.2.2.RELEASE</version>
              </plugin>
```

#### 9.2.4 通过 maven package打包

#### 9.2.5 通过java 命令执行jar 包，相当于启动内嵌tomcat

将target 下的jar 包拷贝到某一个目录，在该目录下执行 java -jar jar 包名称

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot035.png)

也可以创建一个bat文件放在和jar包同进同一级目录，bat文件写入java -jar jar名双击运行



### 9.3 Spring Boot 部署与运行的方式总结

➢	在IDEA 中直接运行 Spring Boot 程序的main 方法（开发阶段）
➢	用maven 将Spring Boot 安装为一个jar 包，使用 Java 命令运行

ava -jar  springboot-xxx.jar  
可以将该命令封装到一个 Linux 的一个shell 脚本中（上线部署）

- 写一个shell 脚本(run.sh)：

  #!/bin/sh 

  java -jar xxx.jar

- 赋权限 chmod 777 run.sh

- 启动shell 脚本： ./run.sh

  ![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot036.png)

<font color=red>使用Spring Boot 的maven 插件将Springboot 程序打成war 包，单独部署在tomcat 中运行（上线部署常用）</font>



## 第10章 SpringBoot 集成logback 日志



### 10.1 日志文件 
Spring Boot 官方推荐优先使用带有 -spring 的文件名作为你的日志配置（如使用 logback-spring.xml ，而不是 logback.xml），命名为 logback-spring.xml 的日志配置文件。 默认的命名规则，并且放在 src/main/resources 下如果你即想完全掌控日志配置，但又不想用logback.xml 作为Logback 配置的名字，application.yml 可以通过logging.config 属性指定自定义的名字： 

```
logging.config=classpath:logging-config.xml
```



#### 10.1.1 创建项目

#### 10.1.2 在src/main/resources 目录下创建名为logback-spring.xml文件，并添加以下代码

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- 日志级别从低到高分为 TRACE < DEBUG < INFO < WARN < ERROR < FATAL，如果
设置为 WARN，则低于 WARN 的信息都不会输出 -->
<!-- scan:当此属性设置为 true 时，配置文件如果发生改变，将会被重新加载，默认值为
true -->
<!-- scanPeriod:设置监测配置文件是否有修改的时间间隔，如果没有给出时间单位，默认
单位是毫秒。当 scan 为 true 时，此属性生效。默认的时间间隔为 1 分钟。 -->
<!-- debug:当此属性设置为 true 时，将打印出 logback 内部日志信息，实时查看 logback
运行状态。默认值为 false。通常不打印 -->
<configuration scan="true" scanPeriod="10 seconds">
    <!--输出到控制台-->
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <!--此日志 appender 是为开发使用，只配置最底级别，控制台输出的日志级别是大
        于或等于此级别的日志信息-->
        <filter class="ch.qos.logback.classic.filter.ThresholdFilter">
            <level>debug</level>
        </filter>
        <encoder>
            <Pattern>%date [%-5p] [%thread] %logger{60} [%file : %line] %msg%n
            </Pattern>
            <!-- 设置字符集 -->
            <charset>UTF-8</charset>
        </encoder>
    </appender>

    <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!--<File>/home/log/stdout.log</File>-->
        <File>D:/log/stdout.log</File>
        <encoder>
            <pattern>%date [%-5p] %thread %logger{60} [%file : %line] %msg%n</pattern>
        </encoder>
        <rollingPolicy
                class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!-- 添加.gz 历史日志会启用压缩 大大缩小日志文件所占空间 -->
            <!--<fileNamePattern>/home/log/stdout.log.%d{yyyy-MM-dd}.log</fileNam ePattern>-->
            <fileNamePattern>D:/log/stdout.log.%d{yyyy-MM-dd}.log</fileNamePattern>
            <maxHistory>30</maxHistory><!-- 保留 30 天日志 -->
        </rollingPolicy>
    </appender>

    <logger name="com.bjpowernode.springboot.mapper" level="DEBUG"/>

    <root level="INFO">
        <appender-ref ref="CONSOLE"/>
        <appender-ref ref="FILE"/>
    </root>
</configuration>
```

#### 10.1.3 项目俺正常部署即可





























## 附录

### Spring Boot 工程下使用Mybatis逆向工程



#### 拷贝Mybatis 逆向工程配置文件到项目的根目录下

获取目录：GeneratorMapper.xml



#### 根据项目及表的情况，修改GeneratorMapper.xml 配置

<font color=red>➢	如果使用高版本，驱动类变为：com.mysql.cj.jdbc.Driver</font>
<font color=red>➢	url 后面应该加属性nullCatalogMeansCurrent=true，否则生成有问题当前版本MySQL 数据库为5.7.18</font>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>

    <!-- 指定连接数据库的 JDBC 驱动包所在位置，指定到你本机的完整路径 -->
    <classPathEntry location="D:\maven\maven_repository\mysql\mysql-connector-java\5.1.6\mysql-connector-java-5.1.6.jar"/>

    <!-- 配置 table 表信息内容体，targetRuntime 指定采用 MyBatis3 的版本 -->
    <context id="tables" targetRuntime="MyBatis3">
        <!-- 抑制生成注释，由于生成的注释都是英文的，可以不让它生成 -->
        <commentGenerator>
            <property name="suppressAllComments" value="true"/>
        </commentGenerator>


        <!-- 配置数据库连接信息 -->
        <jdbcConnection driverClass="com.mysql.jdbc.Driver"
                        connectionURL="jdbc:mysql://127.0.0.1:3306/springdb"
                        userId="root"
                        password="fsy200195">
        </jdbcConnection>
        <!-- 生成 model 类，targetPackage 指定 model 类的包名， targetProject 指定
        生成的 model 放在 eclipse 的哪个工程下面-->
        <javaModelGenerator targetPackage="com.yyb.springboot.model"
                            targetProject="src/main/java">
            <property name="enableSubPackages" value="false"/>
            <property name="trimStrings" value="false"/>
        </javaModelGenerator>

        <!-- 生成 MyBatis 的 Mapper.xml 文件，targetPackage 指定 mapper.xml 文件的
        包名， targetProject 指定生成的 mapper.xml 放在 eclipse 的哪个工程下面 -->
        <sqlMapGenerator targetPackage="com.yyb.springboot.mapper"
                         targetProject="src/main/java">
            <property name="enableSubPackages" value="false"/>
        </sqlMapGenerator>

        <!-- 生成 MyBatis 的 Mapper 接口类文件,targetPackage 指定 Mapper 接口类的包
        名， targetProject 指定生成的 Mapper 接口放在 eclipse 的哪个工程下面 -->
        <javaClientGenerator type="XMLMAPPER"
                             targetPackage="com.yyb.springboot.mapper" targetProject="src/main/java">
            <property name="enableSubPackages" value="false"/>
        </javaClientGenerator>

        <!-- 数据库表名及对应的 Java 模型类名 -->
        <table tableName="t_student" domainObjectName="Student"
               enableCountByExample="false"
               enableUpdateByExample="false"
               enableDeleteByExample="false"
               enableSelectByExample="false"
               selectByExampleQueryId="false"/>
    </context>
</generatorConfiguration>
```



#### 在pom.xml 文件中添加mysql 逆向工程依赖

```xml
<!--mybatis 代码自动生成插件-->
            <plugin>
                <groupId>org.mybatis.generator</groupId>
                <artifactId>mybatis-generator-maven-plugin</artifactId>
                <version>1.3.6</version>
                <configuration>
                    <!--配置文件的位置-->
                    <configurationFile>GeneratorMapper.xml</configurationFile>
                    <verbose>true</verbose>
                    <overwrite>true</overwrite>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
```



#### 双击红色选中命令，生成相关文件

![image-20210717101753135](https://gitee.com/yybovo/note-images/raw/master/Typora/springboot018.png)

<font color=red>mybatis逆向工程生成bean文件的数据库的表名不区分大小写，数据库表名有下划线bean的表名会用驼峰命名法命名（stu_name ---> stuName）</font>>

```xml
mapper映射文件分析
<!--数据库自带名和属性名不一致的转换-->
  <resultMap id="BaseResultMap" type="com.yyb.springboot.model.Student">
    <id column="id" jdbcType="INTEGER" property="id" />
    <result column="NAME" jdbcType="VARCHAR" property="name" />
    <result column="age" jdbcType="INTEGER" property="age" />
  </resultMap>
  <!--抽取公共标签-->
  <sql id="Base_Column_List">
    id, NAME, age
  </sql>
  <select id="selectByPrimaryKey" parameterType="java.lang.Integer" resultMap="BaseResultMap">
    select 
    /*引用抽取的标签*/
    <include refid="Base_Column_List" />
    from t_student
    where id = #{id,jdbcType=INTEGER}
  </select>
```

