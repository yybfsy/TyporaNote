# IDEA小问题合集



## Maven



#### 用maven-archetype-webapp模板创建项目web.xml版本低解决方法

```xml
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
  <display-name>Archetype Created Web Application</display-name>
</web-app>

```

- 首先找到maven本地仓库的maven-archetype-webapp模板路径（本地仓库\org\apache\maven\archetypes\maven-archetype-webapp\1.4\maven-archetype-webapp-1.4.jar），找到maven-archetype-webapp-1.4.jar包

- 用WinRAR解压jar包（到maven-archetype-webapp-1.4.jar\archetype-resources\src\main\webapp\WEB-INF路径下找到web.xml）

- 查看web.xml修改成web.xml4.0的版本（复制一份4.0版本的webx.ml文件，替换原来的文件即可）

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
           version="4.0">
  
  </web-app>
  ```




<h4>IDEA自动生成序列化版本号配置</h4>

- IDEA提供了可以自动生成序列化版本号的快捷方式，首先，需要在Setting中进行配置

  ![xwt001](https://gitee.com/yybovo/note-images/raw/master/Typora/IDEAxwt001.png)

- 然后，在自定义类的时候，将光标点到类名上，按alt+enter就会出现提示，自动添加序列化版本号

  ![img](https://gitee.com/yybovo/note-images/raw/master/Typora/IDEAxwt002.png)

