# SpringMvc笔记

官方文档：

​	[Web on Servlet Stack (spring.io)](https://docs.spring.io/spring-framework/docs/5.3.7/reference/html/web.html)【5.3.7】

- [狂神说SpringMVC笔记 - 时移之人 - 博客园 (cnblogs.com)](https://www.cnblogs.com/yaolicheng/p/13689710.html)
- [狂神说SpringMVC笔记 - 时移之人 - 博客园 (cnblogs.com)](https://www.cnblogs.com/yaolicheng/p/13689710.html)
- [[(25条消息) SpringMvc狂神说学习笔记_爱喝夏进甜牛奶的博客-CSDN博客_狂神springmvc笔记](https://blog.csdn.net/weixin_47955543/article/details/126331841)](https://blog.csdn.net/m0_52162006/article/details/120167131)

## 1.什么是MVC

**MVC：模型(dao、service)、视图(jsp)、控制器(servlet)**

**MVC的工作流程：**

![image-20230211044752506](SpringMVC-images/image-20230211044752506.png)

### 1.1 Model2时代

Model2把一个项目分成三部分，包括**视图、控制、模型。**

![image-20230211045051027](Springmvc-images/image-20230211045051027.png)

1. 用户发请求
2. Servlet接收请求数据，并调用对应的业务逻辑方法
3. 业务处理完毕，返回更新后的数据给servlet
4. servlet转向到JSP，由JSP来渲染页面
5. 响应给前端更新后的页面

**职责分析：**

**Controller：控制器**

1. 取得表单数据
2. 调用业务逻辑
3. 转向指定的页面

**Model：模型**

1. 业务逻辑
2. 保存数据的状态

**View：视图**

1. 显示页面

### 1.2回顾Servlet

1. 新建一个Maven工程当做父工程！pom依赖！

   ```xml
   <dependencies>
      <dependency>
          <groupId>junit</groupId>
          <artifactId>junit</artifactId>
          <version>4.12</version>
      </dependency>
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-webmvc</artifactId>
          <version>5.1.9.RELEASE</version>
      </dependency>
      <dependency>
          <groupId>javax.servlet</groupId>
          <artifactId>servlet-api</artifactId>
          <version>2.5</version>
      </dependency>
      <dependency>
          <groupId>javax.servlet.jsp</groupId>
          <artifactId>jsp-api</artifactId>
          <version>2.2</version>
      </dependency>
      <dependency>
          <groupId>javax.servlet</groupId>
          <artifactId>jstl</artifactId>
          <version>1.2</version>
      </dependency>
   </dependencies>
   ```

   

2. 建立一个Moudle(模块)：springmvc-01-servlet ， 添加Web app的支持

3. 导入servlet 和 jsp 的 jar 依赖

   ```xml
   <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>servlet-api</artifactId>
      <version>2.5</version>
   </dependency>
   <dependency>
      <groupId>javax.servlet.jsp</groupId>
      <artifactId>jsp-api</artifactId>
      <version>2.2</version>
   </dependency>
   ```

   

4. 编写一个Servlet类，用来处理用户的请求

   ```java
   public class HelloServlet extends HttpServlet {
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           //取得参数
           String method = req.getParameter("method");
           if (method.equals("add")){
               req.getSession().setAttribute("msg","执行了add方法");
           }else if (method.equals("del")){
               req.getSession().setAttribute("msg","执行了del方法");
           }
           //业务逻辑
           //视图跳转
           req.getRequestDispatcher("/WEB-INF/jsp/test.jsp").forward(req,resp);
       }
   
       @Override
       protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           doGet(req,resp);
       }
   }
   ```

   

5. 编写test.jsp，在WEB-INF目录下新建一个jsp的文件夹

   ```jsp
   <%@ page contentType="text/html;charset=UTF-8" language="java" %>
   <html>
   <head>
       <title>Title</title>
   </head>
   <body>
   ${msg}
   </body>
   </html>
   ```

   

6. 在web.xml中注册Servlet

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
            version="4.0">
       <!---  <welcome-file-list>-->
       <!--        <welcome-file></welcome-file>-->
       <!--    </welcome-file-list> -->
           <session-config>
               <session-timeout>15</session-timeout>
           </session-config>
   
   
       <servlet>
           <servlet-name>hello</servlet-name>
           <servlet-class>com.zhang.servlet.HelloServlet</servlet-class>
       </servlet>
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/method</url-pattern>
       </servlet-mapping>
   </web-app>
   ```

   

7. 配置Tomcat，并启动测试

   ```
   http://localhost:8080/zhang/method?method=del
   http://localhost:8080/zhang/method?method=add
   ```

​	常见的服务器端MVC框架有：Struts、Spring MVC、ASP.NET MVC、Zend Framework、JSF；

​	常见前端MVC框架：vue、angularjs、react、backbone；由MVC演化出了另外一些模式如：MVP、MVVM 等等....

## 2. 什么是SpringMvc

### 2.1、概述

Spring MVC是Spring Framework的一部分，是基于Java实现MVC的轻量级Web框架

**我们为什么要学习SpringMVC呢?**

 Spring MVC的特点：

1. 轻量级，简单易学
2. 高效 , 基于请求响应的MVC框架
3. 与Spring兼容性好，无缝结合
4. 约定优于配置
5. 功能强大：RESTful、数据验证、格式化、本地化、主题等
6. 简洁灵活

Spring的web框架围绕==**DispatcherServlet**== [ 调度Servlet ] 设计。

DispatcherServlet的作用是将请求分发到不同的处理器。从Spring 2.5开始，使用Java 5或者以上版本的用户可以采用基于注解形式进行开发，十分简洁；

正因为SpringMVC好 , 简单 , 便捷 , 易学 , 天生和Spring无缝集成(使用SpringIoC和Aop) , 使用约定优于配置 . 能够进行简单的junit测试 . 支持Restful风格 .异常处理 , 本地化 , 国际化 , 数据验证 , 类型转换 , 拦截器 等等......所以我们要学习 .

### 2.2、中心控制器

Spring的web框架围绕DispatcherServlet设计。DispatcherServlet的作用是将请求分发到不同的处理器。

Spring MVC框架像许多其他MVC框架一样, **以请求为驱动** , **围绕一个中心Servlet分派请求及提供其他功能**，**DispatcherServlet是一个实际的Servlet (它继承自HttpServlet 基类)**。

![image-20230211180415716](SpringMVC-images/image-20230211180415716.png)

SpringMVC的原理如下图所示：

​	当发起请求时被前置的控制器拦截到请求，根据请求参数生成代理请求，找到请求对应的实际控制器，控制器处理请求，创建数据模型，访问数据库，将模型响应给中心控制器，控制器使用模型与视图渲染视图结果，将结果返回给中心控制器，再将结果返回给请求者。

![image-20230211180451354](SpringMVC-images/image-20230211180451354.png)

### 2.3、SpringMVC执行原理

实线表示SpringMVC框架提供的技术，不需要开发者实现，虚线表示需要开发者实现。

![image-20230211182823185](SpringMVC-images/image-20230211182823185.png)

**简要分析执行流程**

1. DispatcherServlet表示前置控制器，是整个SpringMVC的控制中心。用户发出请求，DispatcherServlet接收请求并拦截请求。

   我们假设请求的url为 : http://localhost:8080/SpringMVC/hello

   **如上url拆分成三部分：**

   http://localhost:8080服务器域名

   **SpringMVC部署在服务器上的web站点**

   **hello表示控制器**

   通过分析，如上url表示为：请求位于服务器localhost:8080上的SpringMVC站点的hello控制器。

2. HandlerMapping为处理器映射。DispatcherServlet调用HandlerMapping,HandlerMapping根据请求url查找Handler。

3. HandlerExecution表示具体的Handler,其主要作用是根据url查找控制器，如上url被查找控制器为：hello。

4. HandlerExecution将解析后的信息传递给DispatcherServlet,如解析控制器映射等。

5. HandlerAdapter表示处理器适配器，其按照特定的规则去执行Handler。

6. Handler让具体的Controller执行。

7. Controller将具体的执行信息返回给HandlerAdapter,如ModelAndView。

8. HandlerAdapter将视图逻辑名或模型传递给DispatcherServlet。

9. DispatcherServlet调用视图解析器(ViewResolver)来解析HandlerAdapter传递的逻辑视图名。

10. 视图解析器将解析的逻辑视图名传给DispatcherServlet。

11. DispatcherServlet根据视图解析器解析的视图结果，调用具体的视图。

12. 最终视图呈现给用户。

## 3.第一个MVC程序

#### 配置版

1、新建一个Moudle ， springmvc-02-hello ， 添加web的支持！

2、确定导入了SpringMVC 的依赖！

3、配置web.xml  ， 注册DispatcherServlet

```xml
<!--1.注册DispatcherServlet-->
    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!--关联一个springmvc的配置文件:【servlet-name】-servlet.xml-->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc-servlet.xml</param-value>
        </init-param>
        <!--启动级别-1-->
        <load-on-startup>1</load-on-startup>
    </servlet>

    <!--/ 匹配所有的请求；（不包括.jsp）-->
    <!--/* 匹配所有的请求；（包括.jsp）-->
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
```

4. 编写SpringMVC 的 配置文件！名称：springmvc-servlet.xml  : [servletname]-servlet.xml

   ```xml
   <!--Handler  将自己的类交给SpringIOC容器，注册bean-->
       <bean id="/hello" class="com.zhang.controller.HelloController"/>
   
       <!--  添加 处理映射器  -->
   
       <bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>
   
       <!--  添加 处理器适配器  -->
   
       <bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"/>
   
   
       <!--视图解析器:DispatcherServlet给他的ModelAndView-->
       <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="InternalResourceViewResolver">
           <!--前缀-->
           <property name="prefix" value="/WEB-INF/jsp/"/>
           <!--后缀-->
           <property name="suffix" value=".jsp"/>
       </bean>
   ```

   

说明，这里的名称要求是按照官方来的

5. 编写我们要操作业务Controller ，要么实现Controller接口，要么增加注解；需要返回一个ModelAndView，装数据，封视图；

   ```java
   //注意：这里我们先导入Controller接口
   public class HelloController implements Controller {
   
       public ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response) throws Exception {
           //ModelAndView 模型和视图
           ModelAndView mv = new ModelAndView();
   
           //封装对象，放在ModelAndView中。Model
           mv.addObject("msg","HelloSpringMVC!");
           //封装要跳转的视图，放在ModelAndView中
           mv.setViewName("hello"); //: /WEB-INF/jsp/hello.jsp
           return mv;
       }
   
   }
   ```

   6. 写要跳转的jsp页面，显示ModelandView存放的数据，以及我们的正常页面；

      ```jsp
      <%@ page contentType="text/html;charset=UTF-8" language="java" %>
      <html>
      <head>
          <title>Title</title>
      </head>
      <body>
      ${msg}
      </body>
      </html>
      ```

      **可能遇到的问题：访问出现404，排查步骤：**

      1. 查看控制台输出，看一下是不是缺少了什么jar包。

      2. 如果jar包存在，显示无法输出，就在IDEA的项目发布中，添加lib依赖！

         ![image-20230211234003550](SpringMVC-images/image-20230211234003550.png)

      3. 重启Tomcat 即可解决！

#### 注解版

1. **新建一个Moudle，springmvc-03-hello-annotation 。添加web支持！**

2. 由于Maven可能存在资源过滤的问题，我们将配置完善

   ```xml
   <build>
      <resources>
          <resource>
              <directory>src/main/java</directory>
              <includes>
                  <include>**/*.properties</include>
                  <include>**/*.xml</include>
              </includes>
              <filtering>false</filtering>
          </resource>
          <resource>
              <directory>src/main/resources</directory>
              <includes>
                  <include>**/*.properties</include>
                  <include>**/*.xml</include>
              </includes>
              <filtering>false</filtering>
          </resource>
      </resources>
   </build>
   ```

   

3. 在pom.xml文件引入相关的依赖：主要有Spring框架核心库、Spring MVC、servlet , JSTL等。我们在父依赖中已经引入了！

4. **配置web.xml**

   ```xml
   <!--1.注册DispatcherServlet:是SpringMVC的核心：请求分发器，前端控制器-->
       <servlet>
           <servlet-name>SpringMVC</servlet-name>
           <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
           <!--关联一个springmvc的配置文件:【servlet-name】-servlet.xml-->
           <init-param>
               <param-name>contextConfigLocation</param-name>
               <param-value>classpath:springmvc-servlet.xml</param-value>
           </init-param>
           <!--启动级别-1-->
           <load-on-startup>1</load-on-startup>
       </servlet>
       <servlet-mapping>
           <servlet-name>SpringMVC</servlet-name>
           <url-pattern>/</url-pattern>
       </servlet-mapping>
   ```

   **/ 和 /\* 的区别：**< url-pattern > / </ url-pattern > 不会匹配到.jsp， 只针对我们编写的请求；即：.jsp 不会进入spring的 DispatcherServlet类 。< url-pattern > /* </ url-pattern > 会匹配 *.jsp，会出现返回 jsp视图 时再次进入spring的DispatcherServlet 类，导致找不到对应的controller所以报404错。

   1. - 注意web.xml版本问题，要最新版！
      - 注册DispatcherServlet
      - 关联SpringMVC的配置文件
      - 启动级别为1
      - 映射路径为 / 【不要用/*，会404】

1. **添加Spring MVC配置文件**

   在resource目录下添加springmvc-servlet.xml配置文件，配置的形式与Spring容器配置基本类似，为了支持基于注解的IOC，设置了自动扫描包的功能，具体配置信息如下：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xmlns:mvc="http://www.springframework.org/schema/mvc"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/context
          https://www.springframework.org/schema/context/spring-context.xsd
          http://www.springframework.org/schema/mvc
          https://www.springframework.org/schema/mvc/spring-mvc.xsd">
   
      <!-- 自动扫描包，让指定包下的注解生效,由IOC容器统一管理 -->
      <context:component-scan base-package="com.kuang.controller"/>
      <!-- 让Spring MVC不处理静态资源 -->
      <mvc:default-servlet-handler />
      <!--
      支持mvc注解驱动
          在spring中一般采用@RequestMapping注解来完成映射关系
          要想使@RequestMapping注解生效
          必须向上下文中注册DefaultAnnotationHandlerMapping
          和一个AnnotationMethodHandlerAdapter实例
          这两个实例分别在类级别和方法级别处理。
          而annotation-driven配置帮助我们自动完成上述两个实例的注入。
       -->
      <mvc:annotation-driven />
   
      <!-- 视图解析器 -->
      <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
            id="internalResourceViewResolver">
          <!-- 前缀 -->
          <property name="prefix" value="/WEB-INF/jsp/" />
          <!-- 后缀 -->
          <property name="suffix" value=".jsp" />
      </bean>
   
   </beans>
   ```

   1. 在视图解析器中我们把所有的视图都存放在**/WEB-INF/**目录下，这样可以保证视图安全，因为这个目录下的文件，客户端不能直接访问。

   2. - 让IOC的注解生效
      - 静态资源过滤 ：HTML . JS . CSS . 图片 ， 视频 .....
      - MVC的注解驱动
      - 配置视图解析器

2. **创建Controller**

   ```JAVA
   @RequestMapping("/hello")
   @Controller
   public class HelloController {
       //真实访问地址 : 项目名/hello/h1
       @RequestMapping("/h1")
       public String Hello(Model model){
           //封装数据
           //向模型中添加属性msg与值，可以在JSP页面中取出并渲染
           model.addAttribute("msg","Hello,SpringMVC AAA");
           //web-inf/jsp/hello.jsp
           return "hello"; //被视图解析器处理
       }
   }
   
   ```

   - @Controller是为了让Spring IOC容器初始化时自动扫描到；
   - @RequestMapping是为了映射请求路径，这里因为类与方法上都有映射所以访问时应该是/HelloController/hello；
   - 方法中声明Model类型的参数是为了把Action中的数据带到视图中；
   - 方法返回的结果是视图的名称hello，加上配置文件中的前后缀变成WEB-INF/jsp/**hello**.jsp。

3. **创建视图层**

   ```JSP
   <%@ page contentType="text/html;charset=UTF-8" language="java" %>
   <html>
   <head>
       <title>Title</title>
   </head>
   <body>
   ${msg}
   </body>
   </html>	
   ```

   

4. **配置Tomcat运行**

### 小结

1. 使用springMVC必须配置的三大件：

2. **处理器映射器、处理器适配器、视图解析器**

3. 通常，我们只需要**手动配置视图解析器**，而**处理器映射器**和**处理器适配器**只需要开启**注解驱动**即可，而省去了大段的xml配置

4. 

## 4.控制器Controller

- 控制器复杂提供访问应用程序的行为，通常通过接口定义或注解定义两种方法实现。
- 控制器负责解析用户的请求并将其转换为一个模型。
- 在Spring MVC中一个控制器类可以包含多个方法
- 在Spring MVC中，对于Controller的配置方式有很多种

### 实现Controller接口

Controller是一个接口，在org.springframework.web.servlet.mvc包下，接口中只有一个方法；

```java
//实现该接口的类获得控制器功能
public interface Controller {
   //处理请求且返回一个模型与视图对象
   ModelAndView handleRequest(HttpServletRequest var1, HttpServletResponse var2) throws Exception;
}
```

#### **测试**

1. 新建一个Moudle，springmvc-04-controller 。将刚才的03 拷贝一份, 我们进行操作！

2. - 重写一个HelloController,

     ```java
     public class HelloController implements Controller {
         @Override
         public ModelAndView handleRequest(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
             ModelAndView modelAndView = new ModelAndView();
             modelAndView.addObject("msg","Controllertest");
             modelAndView.setViewName("test");
             return modelAndView;
         }
     }
     ```

     

   - mvc的配置文件只留下 视图解析器！

     ```xml
     <?xml version="1.0" encoding="UTF-8"?>
     <beans xmlns="http://www.springframework.org/schema/beans"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xmlns:context="http://www.springframework.org/schema/context"
            xmlns:mvc="http://www.springframework.org/schema/mvc"
            xsi:schemaLocation="http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd
            https://www.springframework.org/schema/context/spring-context.xsd
            http://www.springframework.org/schema/mvc
            https://www.springframework.org/schema/mvc/spring-mvc.xsd">
         <bean name="/t1" class="com.zhang.controller.HelloController"/>
         <!-- 自动扫描包，让指定包下的注解生效,由IOC容器统一管理 -->
     <!--    <context:component-scan base-package="com.zhang.controller"/>-->
     <!--    &lt;!&ndash; 让Spring MVC不处理静态资源 .css,js,html,mp3,mp4 &ndash;&gt;-->
     <!--    <mvc:default-servlet-handler />-->
     <!--    &lt;!&ndash;-->
     <!--    支持mvc注解驱动-->
     <!--        在spring中一般采用@RequestMapping注解来完成映射关系-->
     <!--        要想使@RequestMapping注解生效-->
     <!--        必须向上下文中注册DefaultAnnotationHandlerMapping-->
     <!--        和一个AnnotationMethodHandlerAdapter实例-->
     <!--        这两个实例分别在类级别和方法级别处理。-->
     <!--        而annotation-driven配置帮助我们自动完成上述两个实例的注入。-->
     <!--     &ndash;&gt;-->
     <!--    <mvc:annotation-driven />-->
         <!-- 视图解析器     ViewResolver -->
         <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="InternalResourceViewResolver">
             <!--前缀-->
             <property name="prefix" value="/WEB-INF/jsp/"></property>
             <!--后缀-->
             <property name="suffix" value=".jsp"></property>
         </bean>
     </beans>
     ```

     

3. 编写完毕后，去Spring配置文件中注册请求的bean；name对应请求路径，class对应处理请求的类

   ```xml
    <bean name="/t1" class="com.zhang.controller.HelloController"/>
   ```

   

4. 编写前端test.jsp，注意在WEB-INF/jsp目录下编写，对应我们的视图解析器

   ```jsp
   <%@ page contentType="text/html;charset=UTF-8" language="java" %>
   <html>
   <head>
       <title>Title</title>
   </head>
   <body>
   ${msg}
   </body>
   </html>
   ```

   **说明：**

   - 实现接口Controller定义控制器是较老的办法
   - 缺点是：一个控制器中只有一个方法，如果要多个方法则需要定义多个Controller；定义的方式比较麻烦；

### 使用注解@Controller

- @Controller注解类型用于声明Spring类的实例是一个控制器（在讲IOC时还提到了另外3个注解）；

```java
Spring框架中注解
    @Component  组件
    @Service	service(作用于业务逻辑层)
    @Controller  controller(作用于表现层（spring-mvc的注解）)
    @Repository  dao(作用于持久层)
```

- Spring可以使用扫描机制来找到应用程序中所有基于注解的控制器类，为了保证Spring能找到你的控制器，需要在配置文件中声明组件扫描。

  ```xml
  <!-- 自动扫描指定的包，下面所有注解类交给IOC容器管理 -->
  <context:component-scan base-package="com.zhang.controller"/>
  ```

- 增加一个ControllerTest2类，使用注解实现

  ```java
  //@Controller注解的类会自动添加到Spring上下文中
  @Controller
  public class ControllerTest2 {
      //映射访问路径
      @RequestMapping("/t2")
      public String test2(Model model){
          //Spring MVC会自动实例化一个Model对象用于向视图中传值
          model.addAttribute("msg", "ControllerTest2");
          //返回视图位置
          return "test";
      }
  }
  ```

  

## 5.@RequestMapping

- @RequestMapping注解用于映射url到控制器类或一个特定的处理程序方法。可用于类或方法上。用于类上，表示类中的所有响应请求的方法都是以该地址作为父路径。

- 为了测试结论更加准确，我们可以加上一个项目名测试 myweb

- 只注解在方法上面

  ```java
  @Controller
  public class TestController {
     @RequestMapping("/h1")
     public String test(){
         return "test";
    }
  }
  访问路径：http://localhost:8080 / 项目名 / h1
  ```

- 同时注解类与方法

  ```java
  @Controller
  @RequestMapping("/admin")
  public class TestController {
     @RequestMapping("/h1")
     public String test(){
         return "test";
    }
  }
  访问路径：http://localhost:8080 / 项目名/ admin /h1  , 需要先指定类的路径再指定方法的路径；
  ```

## 6.RestFul 风格

从http://127.0.0.1/item/queryItem.action?id=1

====>

http://127.0.0.1/item/1

### **概念**

Restful就是一个**资源定位及资源操作的风格**。不是标准也不是协议，只是一种风格。基于这个风格设计的软件可以**更简洁，更有层次，更易于实现缓存等机制**。

### **功能**

资源：互联网所有的事物都可以被抽象为资源

资源操作：使用POST、DELETE、PUT、GET，使用不同方法对资源进行操作。

分别对应 添加、 删除、修改、查询。

**传统方式操作资源**  ：通过不同的参数来实现不同的效果！方法单一，post 和 get

​	http://127.0.0.1/item/queryItem.action?id=1 查询,GET

​	http://127.0.0.1/item/saveItem.action 新增,POST

​	http://127.0.0.1/item/updateItem.action 更新,POST

​	http://127.0.0.1/item/deleteItem.action?id=1 删除,GET或POST

**使用RESTful操作资源** ：可以通过不同的请求方式来实现不同的效果！如下：请求地址一样，但是功能可以不同！

​	http://127.0.0.1/item/1 查询,GET

​	http://127.0.0.1/item 新增,POST

​	http://127.0.0.1/item 更新,PUT

​	http://127.0.0.1/item/1 删除,DELET

### **学习测试**

1. 在新建一个类 RestFulController

2. 在Spring MVC中可以使用  @PathVariable 注解，让方法参数的值对应绑定到一个URI模板变量上。

   ```java
   @Controller
   public class RestFulController {
       //原来方式：http://localhost:8080/add?a=1&b=1
       //RestFul：http://localhost:8080/add/1/2
       @RequestMapping("/add/{a}/{b}")
       public String test1(@PathVariable int a,@PathVariable int b, Model model){
           int result = a+b;
           model.addAttribute("msg","结果为"+result);
           return "test";
       }
   }
   ```

   

3. 测试

4. 思考：使用路径变量的好处？
   - 使路径变得更加简洁；
   - 获得参数更加方便，框架会自动进行类型转换。
   - 通过路径变量的类型可以约束访问参数，如果类型不一样，则访问不到对应的请求方法，如这里访问是的路径是/commit/1/a，则路径与方法不匹配，而不会是参数转换失败。

5. 修改下对应的参数类型，再次测试

**使用method属性指定请求类型**

用于约束请求的类型，可以收窄请求范围。指定请求谓词的类型如GET, POST, HEAD, OPTIONS, PUT, PATCH, DELETE, TRACE等

测试

- 增加一个方法
- 用浏览器地址栏进行访问默认是Get请求，会报错405：
- 将POST修改为GET则正常了；

### **小结：**

Spring MVC 的 **@RequestMapping** 注解能够处理 HTTP 请求的方法, 比如 GET, PUT, POST, DELETE 以及 PATCH。

**所有的地址栏请求默认都会是 HTTP GET 类型的。**

方法级别的注解变体有如下几个：组合注解

```java
@GetMapping 
@PostMapping
@PutMapping
@DeleteMapping
@PatchMapping
```

@GetMapping 是一个组合注解，平时使用的会比较多！

它所扮演的是 **@RequestMapping(method =RequestMethod.GET)** 的一个快捷方式。

### 扩展：小黄鸭调试法

## 7.重定向和转发

### 结果跳转方式

#### ModelAndView

设置ModelAndView对象 , 根据view的名称 , 和视图解析器跳到指定的页面 .

```xml
<!-- 视图解析器 -->
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
     id="internalResourceViewResolver">
   <!-- 前缀 -->
   <property name="prefix" value="/WEB-INF/jsp/" />
   <!-- 后缀 -->
   <property name="suffix" value=".jsp" />
</bean>
```

对应的controller类

```java
public class ControllerTest1 implements Controller {

   public ModelAndView handleRequest(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
       //返回一个模型视图对象
       ModelAndView mv = new ModelAndView();
       mv.addObject("msg","ControllerTest1");
       mv.setViewName("test");
       return mv;
  }
}
```

#### ServletAPI(不需要视图解析器)

通过设置ServletAPI 

- 1、通过HttpServletResponse进行输出
- 2、通过HttpServletResponse实现重定向
- 3、通过HttpServletResponse实现转发

#### SpringMVC

注：redirect（重定向）和forward（转发）都不会触发视图解析器

##### 无需视图解析器

​	通过SpringMVC来实现转发和重定向

测试前，需要将视图解析器注释掉

```java
@Controller
public class ModelTest2 {
    @RequestMapping("/m2/t2")
    public String test1(Model model){
        model.addAttribute("msg","modeltest2");
        return "/WEB-INF/jsp/test.jsp";
        或
        return "forward:/WEB-INF/jsp/test.jsp";
    }
}
```

##### 有视图解析器

​	通过SpringMVC来实现转发和重定向

```java

    @RequestMapping("/rsm2/t2")
    public String test2(Model model){
        //重定向
        model.addAttribute("msg","有视图解析器");
        return "test";
        //return "redirect:hello.do"; //hello.do为另一个请求/
    }
```

## 8.数据处理

### 处理提交数据

**1、提交的域名称和处理方法的参数名一致**

提交数据 : http://localhost:8080/hello?name=kuangshen

处理方法 :

```java
@RequestMapping("/hello")
public String hello(String name){
   System.out.println(name);
   return "hello";
}
```



**2、提交的域名称和处理方法的参数名不一致**

提交数据 : http://localhost:8080/hello?username=kuangshen

处理方法 :

@RequestParam("username") : username提交的域的名称 .

```java
@RequestMapping("/hello")
public String hello(@RequestParam("username") String name){
   System.out.println(name);
   return "hello";
}
```

**3、提交的是一个对象**

要求提交的表单域和对象的属性名一致  , 参数使用对象即可

```xml
<dependencies>
       <dependency>
           <groupId>org.projectlombok</groupId>
           <artifactId>lombok</artifactId>
           <version>1.18.24</version>
       </dependency>
   </dependencies>
```



1、实体类

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private int id;
    private String name;
    private int age;
    //构造
    //get/set
    //tostring()
}
```



2、提交数据 : http://localhost:8080/mvc04/user?name=kuangshen&id=1&age=15

3、处理方法 :

```java
@Controller
@RequestMapping("/user")
public class UserController {
    @GetMapping("/t1")
    public String test1(String name, Model model){
        // 1. 接受前端参数
        System.out.println("接收前端参数为"+name);
        // 2. 返回结果传递给前端 model
        model.addAttribute("msg",name);
        // 3. 视图跳转
        return "test";
    }
    
    @GetMapping("/t2")
    public String test2(User user){
        System.out.println(user);
        return "test";
    }
}
```

**说明**：如果使用对象的话，前端传递的参数名和对象名必须一致，否则就是null。

### 数据显示到前端

**第一种 : 通过ModelAndView**

```java
public class ControllerTest1 implements Controller {

   public ModelAndView handleRequest(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
       //返回一个模型视图对象
       ModelAndView mv = new ModelAndView();
       mv.addObject("msg","ControllerTest1");
       mv.setViewName("test");
       return mv;
  }
}
```



**第二种 : 通过ModelMap**

ModelMap

```java
@RequestMapping("/hello")
public String hello(@RequestParam("username") String name, ModelMap model){
   //封装要显示到视图中的数据
   //相当于req.setAttribute("name",name);
   model.addAttribute("name",name);
   System.out.println(name);
   return "hello";
}
```



**第三种 : 通过Model**

```java
@RequestMapping("/ct2/hello")
public String hello(@RequestParam("username") String name, Model model){
   //封装要显示到视图中的数据
   //相当于req.setAttribute("name",name);
   model.addAttribute("msg",name);
   System.out.println(name);
   return "test";
}
```



### 对比

就对于新手而言简单来说使用区别就是：

```
Model 只有寥寥几个方法只适合用于储存数据，简化了新手对于Model对象的操作和理解；

ModelMap 继承了 LinkedMap ，除了实现了自身的一些方法，同样的继承 LinkedMap 的方法和特性；

ModelAndView 可以在储存数据的同时，可以进行设置返回的逻辑视图，进行控制展示层的跳转。
```

当然更多的以后开发考虑的更多的是性能和优化，就不能单单仅限于此的了解。

**请使用80%的时间打好扎实的基础，剩下18%的时间研究框架，2%的时间去学点英文，框架的官方文档永远是最好的教程。**

## 9.乱码问题

测试步骤：

1、我们可以在首页编写一个提交的表单

```jsp
<form action="/e/t1" method="post">
        <input type="text" name="name">
        <input type="submit">
    </form>
```



2、后台编写对应的处理类

```java
@Controller
public class EncodingController {
    @PostMapping("/e/t1")
    public String test1(String name,Model model){
        model.addAttribute("msg",name);
        return "test";
    }

```



3、输入中文测试，发现乱码

输入中文后

![image-20230212223225143](SpringMVC-images/image-20230212223225143.png)

### SpringMVC提供的过滤器

而SpringMVC给我们提供了一个过滤器 , 可以在web.xml中配置 .

修改了xml文件需要重启服务器！

```xml
<filter>
   <filter-name>encoding</filter-name>
   <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
   <init-param>
       <param-name>encoding</param-name>
       <param-value>utf-8</param-value>
   </init-param>
</filter>
<filter-mapping>
   <filter-name>encoding</filter-name>
   <url-pattern>/*</url-pattern>
</filter-mapping>
```

### 自己写的过滤器

1. CharacterEncoding

   ```java
   package com.zhang.utils;
   
   import javax.servlet.*;
   import java.io.IOException;
   
   public class CharacterEncoding implements Filter {
   
       @Override
       public void init(FilterConfig filterConfig) throws ServletException {
   
       }
   
       @Override
       public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
           request.setCharacterEncoding("utf-8");
           response.setCharacterEncoding("utf-8");
           chain.doFilter(request,response);
       }
   
       @Override
       public void destroy() {
   
       }
   }
   
   ```

   

2. web.xml

   ```xml
   <filter>
           <filter-name>characterencoding</filter-name>
           <filter-class>com.zhang.utils.CharacterEncoding</filter-class>
       </filter>
       <filter-mapping>
           <filter-name>characterencoding</filter-name>
               <!-- /* 过滤所有清求       -->
           <url-pattern>/*</url-pattern>
       </filter-mapping>
   ```

   但是我们发现 , 有些极端情况下.这个过滤器对get的支持不好 .

   处理方法 :

   1、修改tomcat配置文件（conf/server.xml） ：设置编码！

   ```
   <Connector URIEncoding="utf-8" port="8080" protocol="HTTP/1.1"
             connectionTimeout="20000"
             redirectPort="8443" />
   ```

​      2、自定义过滤器

```java
package com.kuang.filter;

import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletRequestWrapper;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.UnsupportedEncodingException;
import java.util.Map;

/**
* 解决get和post请求 全部乱码的过滤器
*/
public class GenericEncodingFilter implements Filter {

   @Override
   public void destroy() {
  }

   @Override
   public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
       //处理response的字符编码
       HttpServletResponse myResponse=(HttpServletResponse) response;
       myResponse.setContentType("text/html;charset=UTF-8");

       // 转型为与协议相关对象
       HttpServletRequest httpServletRequest = (HttpServletRequest) request;
       // 对request包装增强
       HttpServletRequest myrequest = new MyRequest(httpServletRequest);
       chain.doFilter(myrequest, response);
  }

   @Override
   public void init(FilterConfig filterConfig) throws ServletException {
  }

}

//自定义request对象，HttpServletRequest的包装类
class MyRequest extends HttpServletRequestWrapper {

   private HttpServletRequest request;
   //是否编码的标记
   private boolean hasEncode;
   //定义一个可以传入HttpServletRequest对象的构造函数，以便对其进行装饰
   public MyRequest(HttpServletRequest request) {
       super(request);// super必须写
       this.request = request;
  }

   // 对需要增强方法 进行覆盖
   @Override
   public Map getParameterMap() {
       // 先获得请求方式
       String method = request.getMethod();
       if (method.equalsIgnoreCase("post")) {
           // post请求
           try {
               // 处理post乱码
               request.setCharacterEncoding("utf-8");
               return request.getParameterMap();
          } catch (UnsupportedEncodingException e) {
               e.printStackTrace();
          }
      } else if (method.equalsIgnoreCase("get")) {
           // get请求
           Map<String, String[]> parameterMap = request.getParameterMap();
           if (!hasEncode) { // 确保get手动编码逻辑只运行一次
               for (String parameterName : parameterMap.keySet()) {
                   String[] values = parameterMap.get(parameterName);
                   if (values != null) {
                       for (int i = 0; i < values.length; i++) {
                           try {
                               // 处理get乱码
                               values[i] = new String(values[i]
                                      .getBytes("ISO-8859-1"), "utf-8");
                          } catch (UnsupportedEncodingException e) {
                               e.printStackTrace();
                          }
                      }
                  }
              }
               hasEncode = true;
          }
           return parameterMap;
      }
       return super.getParameterMap();
  }

   //取一个值
   @Override
   public String getParameter(String name) {
       Map<String, String[]> parameterMap = getParameterMap();
       String[] values = parameterMap.get(name);
       if (values == null) {
           return null;
      }
       return values[0]; // 取回参数的第一个值
  }

   //取所有值
   @Override
   public String[] getParameterValues(String name) {
       Map<String, String[]> parameterMap = getParameterMap();
       String[] values = parameterMap.get(name);
       return values;
  }
}
```

一般情况下，SpringMVC默认的乱码处理就已经能够很好的解决了！

**然后在web.xml中配置这个过滤器即可！**

## 10.JSON

### 什么是JSON

- JSON(JavaScript Object Notation, JS 对象标记) 是一种轻量级的数据交换格式，目前使用特别广泛。
- 采用完全独立于编程语言的**文本格式**来存储和表示数据。
- 简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言。
- 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。

在 JavaScript 语言中，一切都是对象。因此，任何JavaScript 支持的类型都可以通过 JSON 来表示，例如字符串、数字、对象、数组等。看看他的要求和语法格式：

- 对象表示为键值对，数据由逗号分隔
- 花括号保存对象
- 方括号保存数组

**JSON 键值对**是用来保存 JavaScript 对象的一种方式，和 JavaScript 对象的写法也大同小异，键/值对组合中的键名写在前面并用双引号 "" 包裹，使用冒号 : 分隔，然后紧接着值：

```json
{"name": "QinJiang"}
{"age": "3"}
{"sex": "男"}
```

JSON 是 JavaScript 对象的字符串表示法，它使用文本表示一个 JS 对象的信息，本质是一个字符串。

```json
var obj = {a: 'Hello', b: 'World'}; //这是一个对象，注意键名也是可以使用引号包裹的
var json = '{"a": "Hello", "b": "World"}'; //这是一个 JSON 字符串，本质是一个字符串
```

### **JSON 和 JavaScript 对象互转**

要实现从JSON字符串转换为JavaScript 对象，使用 JSON.parse() 方法：

```json
var obj = JSON.parse('{"a": "Hello", "b": "World"}');
//结果是 {a: 'Hello', b: 'World'}
```

### JavaScript 对象转换为JSON字符串

使用 JSON.stringify() 方法：

```javascript
var json = JSON.stringify({a: 'Hello', b: 'World'});
//结果是 '{"a": "Hello", "b": "World"}'
```

### **代码测试**

jsontest.html

```html
<script type="text/javascript">
        //编写一个JavaScript对象
        var user = {
            name: "阿花",
            age:18,
            sex:"女"
        };
        //将js对象转换成json字符串
        var str = JSON.stringify(user);
        console.log(str);
    </script>
```

### Controller返回JSON数据

#### Jackson使用

Jackson应该是目前比较好的json解析工具了

当然工具不止这一个，比如还有阿里巴巴的 **fastjson** 等等。

我们这里使用Jackson，使用它需要导入它的jar包；

```xml
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.14.2</version>
</dependency>


```

配置SpringMVC需要的配置

web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!--1.注册servlet-->
    <servlet>
        <servlet-name>SpringMVC</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!--通过初始化参数指定SpringMVC配置文件的位置，进行关联-->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc-servlet.xml</param-value>
        </init-param>
        <!-- 启动顺序，数字越小，启动越早 -->
        <load-on-startup>1</load-on-startup>
    </servlet>

    <!--所有请求都会被springmvc拦截 -->
    <servlet-mapping>
        <servlet-name>SpringMVC</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

    <filter>
        <filter-name>encoding</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>utf-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encoding</filter-name>
        <url-pattern>/</url-pattern>
    </filter-mapping>

</web-app>
```



springmvc-servlet.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       https://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/mvc
       https://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!-- 自动扫描指定的包，下面所有注解类交给IOC容器管理 -->
    <context:component-scan base-package="com.zhang.controller"/>

    <!-- 视图解析器 -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
          id="internalResourceViewResolver">
        <!-- 前缀 -->
        <property name="prefix" value="/WEB-INF/jsp/" />
        <!-- 后缀 -->
        <property name="suffix" value=".jsp" />
    </bean>

</beans>
```

User的实体类

```java
package com.zhang.pojo;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private String name;
    private int age;
    private String sex;
}

```

编写一个Controller

这里我们需要两个新东西，一个是**@ResponseBody**，一个是**ObjectMapper对象**，我们看下具体的用法

```java
//@Controller 会走视图解析器
//@RestController 只会返回字符串
@RestController
public class UserController {
    @RequestMapping(value = "/j1",produces = "application/json;charset=utf-8")
    //加了@ResponseBody，就不会走视图解析器，而是直接返回一个字符串
    @ResponseBody
    public String json1() throws JsonProcessingException {
        //创建一个jackson的对象映射器，用来解析数据
        ObjectMapper mapper = new ObjectMapper();
        //创建一个对象
        User user = new User("阿花", 18, "女");
        //将我们的对象解析成为json格式
        String str = mapper.writeValueAsString(user);
        //由于@ResponseBody注解，这里会将str转成json格式返回；十分方便
        return str;
    }
}
```

发现出现了乱码问题

```java
@RequestMapping(value = "/json1",produces = "application/json;charset=utf-8")
```

### 代码优化

#### **乱码统一解决**

springmvc的配置文件上添加一段消息StringHttpMessageConverter转换配置！

```xml
    <mvc:annotation-driven>
        <mvc:message-converters register-defaults="true">
            <bean class="org.springframework.http.converter.StringHttpMessageConverter">
                <constructor-arg value="UTF-8"/>
            </bean>
            <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter">
                <property name="objectMapper">
                    <bean class="org.springframework.http.converter.json.Jackson2ObjectMapperFactoryBean">
                        <property name="failOnEmptyBeans" value="false"/>
                    </bean>
                </property>
            </bean>
        </mvc:message-converters>
```

#### **返回json字符串统一解决**

在类上直接使用 **@RestController**，所有的方法都只会返回 json 字符串

```java
//@Controller 会走视图解析器
//@RestController 只会返回字符串
```

### 测试集合输出

编写工具类JsonUtils.java

```java
public class JsonUtils {
    public static String getJson(Object object) throws JsonProcessingException {
        return getJson(object,"yyyy-MM-dd HH:mm:ss");
    }
    
    public static String getJson(Object object,String dateFormat) throws JsonProcessingException {
        ObjectMapper mapper = new ObjectMapper();
        //使用ObjectMapper 来格式化;不使用时间戳
        mapper.configure(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS,false);
        //自定义日期格式
        SimpleDateFormat sdf = new SimpleDateFormat(dateFormat);
        mapper.setDateFormat(sdf);

        return  mapper.writeValueAsString(object);
    }
}
```



```java
    @RequestMapping(value = "/j2",produces = "application/json;charset=utf-8")
    //加了@ResponseBody，就不会走视图解析器，而是直接返回一个字符串
    @ResponseBody
    public String json2() throws JsonProcessingException {
        //创建一个jackson的对象映射器，用来解析数据
        ObjectMapper mapper = new ObjectMapper();
        //创建一个对象
        List<User> userList = new ArrayList<User>();
        User user1 = new User("阿花1", 181, "女1");
        User user2 = new User("阿花2", 182, "女2");
        User user3 = new User("阿花3", 183, "女3");
        User user4 = new User("阿花4", 184, "女4");
        userList.add(user1);
        userList.add(user2);
        userList.add(user3);
        userList.add(user4);
        //将我们的对象解析成为json格式
        String str = mapper.writeValueAsString(userList);
        //由于@ResponseBody注解，这里会将str转成json格式返回；十分方便
        return str;
    }
```

### 输出时间对象

```java
    @RequestMapping(value = "/j3",produces = "application/json;charset=utf-8")
    //加了@ResponseBody，就不会走视图解析器，而是直接返回一个字符串
    @ResponseBody
    public String json3() throws JsonProcessingException {
        //创建一个jackson的对象映射器，用来解析数据
        ObjectMapper mapper = new ObjectMapper();

        //创建一个对象
        Date date = new Date();

//        String str = mapper.writeValueAsString(simpleDateFormat.format(date));
        //ObjectMapper,时间解析后的默认格式是：Timestamp,时间戳
        //由于@ResponseBody注解，这里会将str转成json格式返回；十分方便
        return JsonUtils.getJson(date);
    }
```



### FastJson使用

fastjson.jar是阿里开发的一款专门用于Java开发的包，

- 可以方便的实现json对象与JavaBean对象的转换，
- 实现JavaBean对象与json字符串的转换，
- 实现json对象与json字符串的转换。

实现json的转换方法很多，最后的实现结果都是一样的。

fastjson 的 pom依赖！

```xml
<!-- https://mvnrepository.com/artifact/com.alibaba.fastjson2/fastjson2 -->
<dependency>
    <groupId>com.alibaba.fastjson2</groupId>
    <artifactId>fastjson2</artifactId>
    <version>2.0.23</version>
</dependency>

```

#### fastjson 三个主要的类：

**JSONObject  代表 json 对象** 

- JSONObject实现了Map接口, 猜想 JSONObject底层操作是由Map实现的。
- JSONObject对应json对象，通过各种形式的get()方法可以获取json对象中的数据，也可利用诸如size()，isEmpty()等方法获取"键：值"对的个数和判断是否为空。其本质是通过实现Map接口并调用接口中的方法完成的。

**JSONArray  代表 json 对象数组**

- 内部是有List接口中的方法来完成操作的。

**JSON代表 JSONObject和JSONArray的转化**

- JSON类源码分析与使用
- 仔细观察这些方法，主要是实现json对象，json对象数组，javabean对象，json字符串之间的相互转化。

#### **测试**

```java
@RequestMapping(value = "/j4",produces = "application/json;charset=utf-8")
    //加了@ResponseBody，就不会走视图解析器，而是直接返回一个字符串
    @ResponseBody
    public String json4() throws JsonProcessingException {
        //创建一个对象
        List<User> userList = new ArrayList<User>();
        User user1 = new User("阿花1", 181, "女1");
        User user2 = new User("阿花2", 182, "女2");
        User user3 = new User("阿花3", 183, "女3");
        User user4 = new User("阿花4", 184, "女4");
        userList.add(user1);
        userList.add(user2);
        userList.add(user3);
        userList.add(user4);
        String str = JSON.toJSONString(userList);
        System.out.println("*******Java对象 转 JSON字符串*******");
        String str1 = JSON.toJSONString(userList);
        System.out.println("JSON.toJSONString(list)==>"+str1);
        String str2 = JSON.toJSONString(user1);
        System.out.println("JSON.toJSONString(user1)==>"+str2);

        System.out.println("\n****** JSON字符串 转 Java对象*******");
        User jp_user1=JSON.parseObject(str2,User.class);
        System.out.println("JSON.parseObject(str2,User.class)==>"+jp_user1);

        System.out.println("\n****** Java对象 转 JSON对象 ******");
        JSONObject jsonObject1 = (JSONObject) JSON.toJSON(user2);
        System.out.println("(JSONObject) JSON.toJSON(user2)==>"+jsonObject1.getString("name"));

        System.out.println("\n****** JSON对象 转 Java对象 ******");
        User to_java_user = JSON.toJavaObject(jsonObject1, User.class);
        System.out.println("JSON.toJavaObject(jsonObject1, User.class)==>"+to_java_user);
        return str;
    }
```



## 11.整合SSM框架

### 11.1 ssm整合Mybatis层

### 11.2 ssm整合Spring层

### 11.3 ssm整合SpringMVC层

### 11.4环境要求

环境：

- IDEA
- MySQL 5.7.19
- Tomcat 9
- Maven 3.6

 要求：

- 需要熟练掌握MySQL数据库，Spring，JavaWeb及MyBatis知识，简单的前端知识；

数据库环境

创建一个存放书籍数据的数据库表



### 11.5 基本环境搭建

1、新建一Maven项目！ssmbuild ， 添加web的支持

2、导入相关的pom依赖！

3、Maven资源过滤设置

4、建立基本结构和配置框架！

- com.kuang.pojo
- com.kuang.dao
- com.kuang.service
- com.kuang.controller
- mybatis-config.xml

### 11.6 Mybatis层编写

1、数据库配置文件 **database.properties**

2、IDEA关联数据库

3、编写MyBatis的核心配置文件

4、编写数据库对应的实体类 com.kuang.pojo.Books

使用lombok插件！

5、编写Dao层的 Mapper接口！

6、编写接口对应的 Mapper.xml 文件。需要导入MyBatis的包；

7、编写Service层的接口和实现类

接口：

实现类：

**OK，到此，底层需求操作编写完毕！**

### 11.7 Spring层

1、配置**Spring整合MyBatis**，我们这里数据源使用c3p0连接池；

2、我们去编写Spring整合Mybatis的相关的配置文件；spring-dao.xml

3、**Spring整合service层**

Spring层搞定！再次理解一下，Spring就是一个大杂烩，一个容器！对吧！

### 11.8 SpringMVC层

1、**web.xml**

2、**spring-mvc.xml**

3、**Spring配置整合文件，applicationContext.xml**

**配置文件，暂时结束！Controller 和 视图层编写**

## 12.**Controller 和 视图层编写**

1、BookController 类编写 ， 方法一：查询全部书籍

2、编写首页 **index.jsp**

3、书籍列表页面 **allbook.jsp**

4、BookController 类编写 ， 方法二：添加书籍

5、添加书籍页面：**addBook.jsp**

6、BookController 类编写 ， 方法三：修改书籍

7、修改书籍页面  **updateBook.jsp**

8、BookController 类编写 ， 方法四：删除书籍

**配置Tomcat，进行运行！**

​	到目前为止，这个SSM项目整合已经完全的OK了，可以直接运行进行测试！这个练习十分的重要，大家需要保证，不看任何东西，自己也可以完整的实现出来！

### **项目结构图** 

## 13. 小结及展望

SSM框架的重要程度是不言而喻的，学到这里，大家已经可以进行基本网站的单独开发。但是这只是增删改查的基本操作。可以说学到这里，大家才算是真正的步入了后台开发的门。也就是能找一个后台相关工作的底线。

或许很多人，工作就做这些事情，但是对于个人的提高来说，还远远不够！

我们后面还要学习一些 SpringMVC 的知识！

- Ajax  和  Json
- 文件上传和下载
- 拦截器

## 14. Ajax研究【异步刷新】

### 简介

- **AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。**
- AJAX 是一种在**无需重新加载整个网页**的情况下，能够**更新部分网页的技术**。
- **Ajax 不是一种新的编程语言，而是一种用于创建更好更快以及交互性更强的Web应用程序的技术。**
- 在 2005 年，Google 通过其 Google Suggest 使 AJAX 变得流行起来。Google Suggest能够自动帮你完成搜索单词。
- Google Suggest 使用 AJAX 创造出动态性极强的 web 界面：当您在谷歌的搜索框输入关键字时，JavaScript 会把这些字符发送到服务器，然后服务器会返回一个搜索建议的列表。
- 就和国内百度的搜索框一样!

- 传统的网页(即不用ajax技术的网页)，想要更新内容或者提交一个表单，都需要重新加载整个网页。
- 使用ajax技术的网页，通过在后台服务器进行少量的数据交换，就可以实现异步局部更新。
- 使用Ajax，用户可以创建接近本地桌面应用的直接、高可用、更丰富、更动态的Web用户界面。

![image-20230214213210737](SpringMVC-images/image-20230214213210737.png)

### 伪造Ajax

我们可以使用前端的一个标签来伪造一个ajax的样子。iframe标签

1、新建一个module ：sspringmvc-06-ajax ， 导入web支持！

2、编写一个 ajax-frame.html 使用 iframe 测试，**感受下效果**

3、使用IDEA开浏览器测试一下！

### **利用AJAX可以做：**

- 注册时，输入用户名自动检测用户是否已经存在。
- 登陆时，提示用户名密码错误
- 删除数据行时，将行ID发送到后台，后台在数据库中删除，数据库删除成功后，在页面DOM中将数据行也删除。
- ....等等

### jQuery.ajax

Ajax的核心是XMLHttpRequest对象(XHR)。XHR为向服务器发送请求和解析服务器响应提供了接口。能够以异步方式从服务器获取新数据。

jQuery 提供多个与 AJAX 有关的方法。

通过 jQuery AJAX 方法，您能够使用 HTTP Get 和 HTTP Post 从远程服务器上请求文本、HTML、XML 或 JSON – 同时您能够把这些外部数据直接载入网页的被选元素中。

jQuery 不是生产者，而是大自然搬运工。

jQuery Ajax本质就是 XMLHttpRequest，对他进行了封装，方便调用！

### **测试**

**最原始的HttpServletResponse处理 , .最简单 , 最通用**

1、配置web.xml 和 springmvc的配置文件，复制上面案例的即可 【记得静态资源过滤和注解驱动配置上】

2、编写一个AjaxController

3、导入jquery ， 可以使用在线的CDN ， 也可以下载导入

4.、编写index.jsp测试

5、启动tomcat测试！打开浏览器的控制台，当我们鼠标离开输入框的时候，可以看到发出了一个ajax的请求！是后台返回给我们的结果！测试成功！

### **Springmvc实现**

实体类user

我们来获取一个集合对象，展示到前端页面

前端页面

### 注册提示效果

我们再测试一个小Demo，思考一下我们平时注册时候，输入框后面的实时提示怎么做到的；如何优化

我们写一个Controller

前端页面 login.jsp

【记得处理json乱码问题】

测试一下效果，动态请求响应，局部刷新，就是如此！

### 获取baidu接口Demo



## 15. 拦截器

SpringMVC的处理器拦截器类似于Servlet开发中的过滤器Filter

**过滤器与拦截器的区别：**拦截器是AOP思想的具体应用。

**过滤器**

- servlet规范中的一部分，任何java web工程都可以使用
- 在url-pattern中配置了/*之后，可以对所有要访问的资源进行拦截

**拦截器** 

- 拦截器是SpringMVC框架自己的，只有使用了SpringMVC框架的工程才能使用
- 拦截器只会拦截访问的控制器方法， 如果访问的是jsp/html/css/image/js是不会进行拦截的

### 自定义拦截器

想要自定义拦截器，必须实现 HandlerInterceptor 接口。

1、新建一个Moudule ， springmvc-07-Interceptor  ， 添加web支持

2、配置web.xml 和 springmvc-servlet.xml 文件

3、编写一个拦截器

```java
public class MyInterceptor implements HandlerInterceptor {
    // return true; 放行：执行下一个拦截器
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("------------处理前------------");
        return true;
    }
     //在请求处理方法执行之后执行
   public void postHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, ModelAndView modelAndView) throws Exception {
       System.out.println("------------处理后------------");
  }

   //在dispatcherServlet处理后执行,做清理工作.
   public void afterCompletion(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, Exception e) throws Exception {
       System.out.println("------------清理------------");
  }
}
```

4、在springmvc的配置文件中配置拦截器

```java
 <mvc:interceptors>
            <mvc:interceptor>
                  <!--/** 包括路径及其子路径-->
                  <!--/admin/* 拦截的是/admin/add等等这种 , /admin/add/user不会被拦截-->
                  <!--/admin/** 拦截的是/admin/下的所有-->
                  <mvc:mapping path="/**"/>
                  <!--bean配置的就是拦截器-->
                  <bean class="com.zhang.config.MyInterceptor"/>
            </mvc:interceptor>
 </mvc:interceptors>
```

编写一个Controller，接收请求

```java
@RestController
public class TestController {
    @GetMapping("/t1")
    public String test(){
        System.out.println("TestController===>执行");
        return "ok";
    }
}
```

### 验证用户是否登录 (认证用户)

**实现思路**

1、有一个登陆页面，需要写一个controller访问页面。

2、登陆页面有一提交表单的动作。需要在controller中处理。判断用户名密码是否正确。如果正确，向session中写入用户信息。*返回登陆成功。*

3、拦截用户请求，判断用户是否登陆。如果用户已经登陆。放行， 如果用户未登陆，跳转到登陆页面

**测试：**

1、编写一个登陆页面  login.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>login</h1>
<form action="${pageContext.request.contextPath}/user/login" method="post">
    username: <input type="text" name="username">
    password: <input type="password" name="password">
    <input type="submit" value="提交">
</form>
</body>
</html>
```

2、编写一个Controller处理请求

```java
@Controller
@RequestMapping("/user")
public class LoginController {
    @RequestMapping("/main")
    public String main(){
        return "main";
    }

    @RequestMapping("/goLogin")
    public String login(){
        return "login";
    }
    @RequestMapping("/login")
    public String login(HttpSession session, String username, String password, Model model){
        //把用户的信息存入session
        session.setAttribute("userLoginInfo",username);
        model.addAttribute("username",username);
        return "main";
    }

    @RequestMapping("/logout")
    public String logout(HttpSession session, String username, String password, Model model){
        //把用户的信息存入session
        session.removeAttribute("userLoginInfo");
        return "login";
    }


}
```

3、编写一个登陆成功的页面 success.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>首页</h1>
<span>${username}</span>
<p><a href="${pageContext.request.contextPath}/user/logout"> 注销 </a></p>
</body>
</html>

```

5、编写用户登录拦截器

```java
public class LoginInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        HttpSession session = request.getSession();
        //什么情况下登陆了
        //登陆页面放行
        if (request.getRequestURI().contains("goLogin")){
            return true;
        }

        //在登录
        if (request.getRequestURI().contains("login")){
            return true;
        }

        if (session.getAttribute("userLoginInfo")!= null) {
            return true;
        }
        //什么情况下没有登陆
        request.getRequestDispatcher("/WEB-INF/jsp/login.jsp").forward(request,response);
        return false;
    }
}
```



6、在Springmvc的配置文件中注册拦截器

```java
 <mvc:interceptor>
                  <!--/** 包括路径及其子路径-->
                  <!--/admin/* 拦截的是/admin/add等等这种 , /admin/add/user不会被拦截-->
                  <!--/admin/** 拦截的是/admin/下的所有-->
                  <mvc:mapping path="/**"/>
                  <!--bean配置的就是拦截器-->
                  <bean class="com.zhang.config.LoginInterceptor"/>
            </mvc:interceptor>
```



## 16. 文件上传和下载

### 准备工作

想使用Spring的文件上传功能，则需要在上下文中配置**MultipartResolver**。

前端表单要求：将表单的method设置为POST，并将enctype设置为multipart/form-data

浏览器才会把用户选择的文件以二进制数据发送给服务器；

**表单中的 enctype 属性做个详细的说明：**

- application/x-www=form-urlencoded：默认方式，只处理表单域中的 value 属性值，采用这种编码方式的表单会将表单域中的值处理成 URL 编码方式。
- multipart/form-data：这种编码方式会以二进制流的方式来处理表单数据，这种编码方式会把文件域指定文件的内容也封装到请求参数中，不会对字符编码。
- text/plain：除了把空格转换为 "+" 号外，其他字符都不做编码处理，这种方式适用直接通过表单发送邮件。

```html
<form action="" enctype="multipart/form-data" method="post">
   <input type="file" name="file"/>
   <input type="submit">
</form>
```

### 文件上传

1、导入文件上传的jar包，commons-fileupload ， Maven会自动帮我们导入他的依赖包 commons-io包；

```xml
<!--文件上传-->
<dependency>
   <groupId>commons-fileupload</groupId>
   <artifactId>commons-fileupload</artifactId>
   <version>1.3.3</version>
</dependency>
<!--servlet-api导入高版本的-->
<dependency>
   <groupId>javax.servlet</groupId>
   <artifactId>javax.servlet-api</artifactId>
   <version>4.0.1</version>
</dependency>
```

2、配置bean：multipartResolver

【**注意！！！这个bena的id必须为：multipartResolver ， 否则上传文件会报400的错误！在这里栽过坑,教训！**】

```xml
<!--文件上传配置-->
<bean id="multipartResolver"  class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
   <!-- 请求的编码格式，必须和jSP的pageEncoding属性一致，以便正确读取表单的内容，默认为ISO-8859-1 -->
   <property name="defaultEncoding" value="utf-8"/>
   <!-- 上传文件大小上限，单位为字节（10485760=10M） -->
   <property name="maxUploadSize" value="10485760"/>
   <property name="maxInMemorySize" value="40960"/>
</bean>
```

CommonsMultipartFile 的 常用方法：

- **String getOriginalFilename()：获取上传文件的原名**
- **InputStream getInputStream()：获取文件流**
- **void transferTo(File dest)：将上传文件保存到一个目录文件中**

测试

前端页面

```jsp
  <form action="${pageContext.request.contextPath}/upload" enctype="multipart/form-data" method="post">
    <input type="file" name="file"/>
    <input type="submit">
  </form>
```

**Controller**

一、

```java
    //@RequestParam("file") 将name=file控件得到的文件封装成CommonsMultipartFile 对象
    //批量上传CommonsMultipartFile则为数组即可
    @RequestMapping("/upload")
    public String fileUpload(@RequestParam("file") CommonsMultipartFile file , HttpServletRequest request) throws IOException, FileNotFoundException {

        //获取文件名 : file.getOriginalFilename();
        String uploadFileName = file.getOriginalFilename();

        //如果文件名为空，直接回到首页！
        if ("".equals(uploadFileName)){
            return "redirect:/index.jsp";
        }
        System.out.println("上传文件名 : "+uploadFileName);

        //上传路径保存设置
        String path = request.getServletContext().getRealPath("/upload");
        //如果路径不存在，创建一个
        File realPath = new File(path);
        if (!realPath.exists()){
            realPath.mkdir();
        }
        System.out.println("上传文件保存地址："+realPath);

        InputStream is = file.getInputStream(); //文件输入流
        OutputStream os = new FileOutputStream(new File(realPath,uploadFileName)); //文件输出流

        //读取写出
        int len=0;
        byte[] buffer = new byte[1024];
        while ((len=is.read(buffer))!=-1){
            os.write(buffer,0,len);
            os.flush();
        }
        os.close();
        is.close();
        return "redirect:/index.jsp";
    }
```

二、

```java
/*
     * 采用file.Transto 来保存上传的文件
     */
    @RequestMapping("/upload2")
    public String  fileUpload2(@RequestParam("file") CommonsMultipartFile file, HttpServletRequest request) throws IOException {

        //上传路径保存设置
        String path = request.getServletContext().getRealPath("/upload");
        File realPath = new File(path);
        if (!realPath.exists()){
            realPath.mkdir();
        }
        //上传文件地址
        System.out.println("上传文件保存地址："+realPath);

        //通过CommonsMultipartFile的方法直接写文件（注意这个时候）
        file.transferTo(new File(realPath +"/"+ file.getOriginalFilename()));

        return "redirect:/index.jsp";
    }
```

文件下载

**文件下载步骤：**

1、设置 response 响应头

2、读取文件 -- InputStream

3、写出文件 -- OutputStream

4、执行操作

5、关闭流 （先开后关）

```java
@RequestMapping(value="/download")
public String downloads(HttpServletResponse response ,HttpServletRequest request) throws Exception{
   //要下载的图片地址
   String  path = request.getServletContext().getRealPath("/upload");
   String  fileName = "基础语法.jpg";

   //1、设置response 响应头
   response.reset(); //设置页面不缓存,清空buffer
   response.setCharacterEncoding("UTF-8"); //字符编码
   response.setContentType("multipart/form-data"); //二进制传输数据
   //设置响应头
   response.setHeader("Content-Disposition",
           "attachment;fileName="+URLEncoder.encode(fileName, "UTF-8"));

   File file = new File(path,fileName);
   //2、 读取文件--输入流
   InputStream input=new FileInputStream(file);
   //3、 写出文件--输出流
   OutputStream out = response.getOutputStream();

   byte[] buff =new byte[1024];
   int index=0;
   //4、执行 写出操作
   while((index= input.read(buff))!= -1){
       out.write(buff, 0, index);
       out.flush();
  }
   out.close();
   input.close();
   return null;
}
```

前端

```jsp
<a href="/download">点击下载</a>
```

