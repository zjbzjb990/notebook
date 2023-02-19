# IDEA使用小技巧

#### 1、IDEA启动小技巧

![image-20220712203731702](image/image-20220712203731702.png)



# 1、基本概念

#### 1.1、前言

web开发：

- web，网页的意思，www.baidu.com·
- 静态web
   - html，css
   - 提供给所有人看的数据始终不会发生变化！
- 动态web
   - 如淘宝，几乎所有的网站都是动态的。
   - 提供给所有人看的数据始终会发生变化，每个人在不同的时间，不同的地点看到的信息各不相同。
   - 技术栈：Servlet/JSP，ASP，PHP

#### 1.2、web应用程序

可以提供浏览器访问的程序；

- a.html、b.html...........多个web 资源，这些web资源可以被外界访问，对外界提供服务。
- 你们能访问到的任何一个页面或资源，都存在于这个世界的，某一个角落的计算机上。
- URL
- 这个统一的web资源会被放在同一个文件夹下，web应用程序>Tomcat：服务器。
- 一个web应用由多部分组成（静态web，动态web）
   - html，css，js
   - jsp，servlet
   - java程序
   - jar包
   - 配置文件（Properties）

web程序编写完毕后，若想提供给外界访问，需要一个服务器来统一管理。



#### 1.3、静态web

- *.htm， *.html这些都是网站的后缀，如果服务器上一直存在这些东西，我们就可以直接进行读取，需要网络；
- ![image-20220619114907205](image/image-20220619114907205.png)

- 静态web存在的缺点
   - Web页面无法动态更新，所有用户看到的都是同一个页面
      - 轮播图，点击特效：伪动态
      -  JavaScript[实际开发中，它用的最多] 
      - VBScript
   - 它无法和数据库交互（数据无法持久化，用户无法交互）



#### 1.4、动态web

页面会动态展示，“web页面的展示效果因人而异”

![image-20220619115452657](image/image-20220619115452657.png)

缺点：

- 加入服务器的动态web资源出现了错误，我们需要重新编写我们的后台程序，重新发布；
   - 停机维护

优点：

- web页面可以动态更新，所有用户看到的都不是同一页面
- 可以与数据库交互（数据持久化：注册，商品信息，用户信息..……）

![image-20220619115629197](image/image-20220619115629197.png)



# 2、Web服务器

#### 2.1、技术讲解

**ASP**：

- 微软：国内最早流行的就是ASP。
- 在HTML中嵌入了VB的脚本，ASP+COM。
- 在ASP开发中，基本一个页面都有几千行的业务代码，页面极其混乱。
- 维护成本高
- C#
- IIS

**PHP**：

- PHP开发速度很快，功能强大，跨平台，代码很简单（百分之70的中小项目可以使用）
- 无法承载大访问量的情况（局限性）

**jsp/Servlet：**

B/S：浏览器和服务器

C/S：客户端和服务器

- sun公司主推的B/S架构。
- 基于Java语言的（所有的大公司，或者一些开源的组件，都是用Java写的）。
- 语法像ASP，ASP->JSP，加强市场强度。



#### 2.2、web服务器

服务器是一种被动的操作，用来处理用户的一些请求和给用户的一些响应信息；

**IIS**

微软的；ASP，Windows中自带的

**Tomcat**

![image-20220620002504510](image/image-20220620002504510.png)

面向百度编程： Tomcat是Apache 软件基金会（Apache Software Foundation)的jakarta项目中的一个核心项目，最 新的Servlet 和JSP 规范总是能在Tomcat中得到体现，因为Tomcat 技术先进、性能稳定，而且免费， 因而深受lava爱好者的喜爱并得到了部分软件开发商的认可，成为目前比较流行的Web应用服务器。

Tomcat 服务器是一个免费的开放源代码的Web应用服务器，属于轻量级应用服务器，在中小型系统和 并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP程序的首选。对于一个Java初学web的人 来说，它是最佳的选择 Tomcat 实际上运行JSP页面和Serlet。Tornct最新版易9.0

 **工作3-5年之后，可以尝试手写Tomcat服务器；**

 下载tomcat：

	 1. 安装or解压 
	 2. 了解配置文件及目录结构 
	            	 3. 这个东西的作用



# 3、Tomcat

3.1、安装 Tomcat

官网：http://tomcat.apache.org/

![image-20220620003136721](image/image-20220620003136721.png)



#### 3.2、Tomcat启动和配置

文件夹作用：

![image-20220622221813103](image/image-20220622221813103.png)

![image-20220622223131473](image/image-20220622223131473.png)



访问测试：http://localhost:8080/

可能遇到的问题：

1. **Java环境变量没有配置 ，java版本和tomcat版本不匹配**

   ![image-20220623001013486](image/image-20220623001013486.png)

2. **闪退问题：需要配置兼容性** 

3. **乱码问题：配置文件中设置** 

Tomcat安装配置及CATALINA_HOME environment variable is not defined correctly问题的解决?

解决方法路径：https://blog.csdn.net/u013393958/article/details/78272242?spm=1001.2101.3001.6650.15&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-15-78272242-blog-111397924.pc_relevant_multi_platform_whitelistv1&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-15-78272242-blog-111397924.pc_relevant_multi_platform_whitelistv1&utm_relevant_index=21

配置Tomcat的环境变量也比较简单，在系统变量中新建，在变量名中输入CATALINA_HOME，在变量值中输入Tomcat的路径，按照此方法再新建，在变量名中输入CATALINA_Base，在变量值中输入Tomcat的路径，再新建，在变量名中输入TOMCAT_HOME，在变量值中输入Tomcat的路径依次确定即可。
![img](image/20171018134949486)

原因：

在这个文件中，首先判断`CATALINA_HOME`[环境变量](https://so.csdn.net/so/search?q=环境变量&spm=1001.2101.3001.7020)是否为空，如果为空，就将当前目录设为`CATALINA_HOME`的值。接着判断当前目录下是否存在`bin\catalina.bat`，如果文件不存在，将当前目录的父目录设为`CATALINA_HOME`的值。

根据笔者机器上Tomcat安装目录的层次结构，最后CATALINA_HOME的值被设为Tomcat的安装目录。如果环境变量CATALINA_HOME已经存在，则通过这个环境变量调用bin目录下的“`catalina.bat start`”命令。

通过这段分析，我们了解到两个信息：

- 一是Tomcat启动时，需要查找`CATALINA_HOME`这个环境变量，如果在Tomcat的bin目录下调用startup.bat，Tomcat会自动并正确设置CATALINA_HOME；
   ![在这里插入图片描述](image/20201219170622131.png)
- 二是执行`startup.bat`命令，实际上执行的是“`catalina.bat start`”命令。



**4、乱码问题**

可以修改 conf/logging.properties 中的 java.util.logging.ConsoleHandler.encoding = GBK **解决乱码 问题**



#### 3.3、配置

![image-20220622232523337](image/image-20220622232523337.png)

可以配置启动的端口号

- tomcat的默认端口号：8080
- mysql：3306
- http:80
- https:443

修改tomcat的默认端口号

![image-20220623003433205](image/image-20220623003433205.png)

```xml
<Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
```

可以配置主机的名称

- 默认的主机名为：localhost->127.0.0.1 
- 默认网站应用存放的位置为：webapps

![image-20220623003612284](image/image-20220623003612284.png)

```xml
<Host name="www.qinjiang.com" appBase="webapps"
unpackWARs="true" autoDeploy="true">
```

配置完tomcat的配置文件后，还需要配置本地的C:\Windows\System32\drivers\etc\hosts文件

`高难度面试题：`

请你谈谈网站时如何进行访问的！

1、输入一个域名；回车

2、检查本机的C:\Windows\System32\drivers\etc\hosts配置文件下有没有这个域名映射；

有：直接返回对应的ip地址，这个地址中有我们需要访问的web程序，可以直接访问

没有：去DNS服务器找，找到的话就返回，找不到就返回找不到

![image-20220623004228771](image/image-20220623004228771.png)

4、可以配置一下环境变量（可选性）



3.4、发布一个web网站

不会就先模仿

- 将自己写的网站，放到服务器（Tomcat）中指定的web应用的文件夹夹（webapps)下，就可以访问了

网站应该有的结构

```basic
--webapps ：Tomcat服务器的web目录
	-ROOT
	-kuangstudy ：网站的目录名
		- WEB-INF
			-classes : java程序
			-lib：web应用所依赖的jar包
			-web.xml ：网站配置文件
		- index.html 默认的首页
		- static
			-css
				-style.css
			-js
			-img
		-.....

```



# 4、Http

#### 4.1、什么是HTTP

（超文本传输协议）是一个简单的请求-响应协议，它通常运行在TCP之上。

- 文本：html，字符串......
- 超文本：图片、音乐、视频、定位、地图....
- 端口：80

Https：安全的



#### 4.2、两个时代

- http1.0
   - HTTP/1.0：客户端可以与web服务器连接后，只能获得一个web资源，断开连接。
- http2.0
   - HTTP/1.1：客户端可以与web服务器连接后，可以获得多个web资源。



#### 4.3、Http请求

- 客户端--发请求（Request）--服务器

例如：百度

```html
Request URL:https://www.baidu.com/   请求地址
Request Method:GET   get方法/post方法
Status Code:200 OK   状态码：200
Remote（远程）   Address:14.215.177.39:443


Accept:text/html
Accept-Encoding:gzip, deflate, br
Accept-Language:zh-CN,zh;q=0.9   语言
Cache-Control:max-age=0
Connection:keep-alive
```

> 请求行

- 请求行中的请求方式：GET
- 请求方式：Get、Post、HEAD、DELETE、PUT、TRACT......
   - get：请求能够携带的参数比较少，大小有限制，会在浏览器的URL地址栏显示数据内容，不安全，但高效
   - post：请求能够携带的参数没有限制，大小没有限制，不会再浏览器的URL地址栏显示数据内容，安全，但是不高效（现在网速快了，和get请求差别不大了）



> 消息头
>

```html
Accept：  告诉浏览器，它所支持的数据类型
Accept-Encoding：  支持哪种编码格式 GBK UTF-8 GB2312 ISO8859-1
Accept-Language：  告诉浏览器，它的语言环境
Cache-Control：  缓存控制
Connection：  告诉浏览器，请求完成是断开还是保持连接
HOST：  主机..../.
```



#### 4.4、响应

- 服务器--响应......客户端

百度：

```html
Cache-Control:private   缓存控制
Connection:Keep-Alive   连接
Content-Encoding:gzip   编码
Content-Type:text/html  类型
```

> 响应体

```html
Accept：  告诉浏览器，它所支持的数据类型
Accept-Encoding：  支持哪种编码格式 GBK UTF-8 GB2312 ISO8859-1
Accept-Language：  告诉浏览器，它的语言环境
Cache-Control：  缓存控制
Connection：  告诉浏览器，请求完成是断开还是保持连接
HOST：  主机..../.
Refresh：  告诉客户端，多久刷新一次；
Location：  让网页重新定位；
```



> 响应状态码

200：请求响应成功  200

3xx：请求重定向      重定向：你重新到我给你新位置去；

4xx：找不到资源      404.资源不存在

5xx：服务器代码错误   500  502：网关错误



`常见面试题：`

当你的浏览器中地址栏输入并回车的一瞬间到页面能够展示回来，经历了什么？



# 5、Maven

**我们为什么要学习这个技术？**

1、在Javaweb开发中，需要使用大量的jar包，我们手动去导入；

2、如何能够让一个东西自动帮我们导入和配置这个jar包。

由此，Maven诞生了



#### 5.1、Maven项目架构管理工具

我们目前用来就是方便导入jar包的！

Maven的核心思想：**约定大于配置**

- 有约束，不要去违反。

Maven会规定好你该如何去编写我们Java代码，必须要按照这个规范来；



#### 5.2、下载安装Maven

官网：https://maven.apache.org/

![image-20220624230104029](image/image-20220624230104029.png)

下载完成后，解压即可；

小狂神友情建议：电脑上的所有环境都放在一个文件夹下，方便管理；



#### 5.3、配置环境变量

在我们环境变量中配置如下配置：

- M2_HOME maven目录下的bin目录 
- MAVEN_HOME maven的目录 
- 在系统的path中配置%MAVEN_HOME%\bin



测试Maven是否安装成功，保证必须配置完毕！  **mvn -version**

![image-20220624230353283](image/image-20220624230353283.png)



#### 5.4、阿里云镜像

- 镜像：mirrors
- 作用：加速我们的下载
- 国内建议使用阿里云的镜像

```xml
<mirror>
    <id>nexus-aliyun</id>
    <mirrorOf>*,!jeecg,!jeecg-snapshots</mirrorOf>
    <name>Nexus aliyun</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public</url>
</mirror>
```



#### 5.5、本地仓库

D:Enmvironment\apache-maven-3.6.2conf\ettings.xml （狂神老师配置源和仓库的文件位置）

在本地的仓库，远程仓库； 建立一个本地仓库：localRepository

```xml
<localRepository>D:\Environment\apache-maven-3.6.2\maven-repo</localRepository>
```



#### 5.6、在IDEA中使用Maven

1、启动IDEA

2、创建一个Maven项目

![image-20220624232341353](image/image-20220624232341353.png)



![image-20220624232400904](image/image-20220624232400904.png)



![image-20220624232405912](image/image-20220624232405912.png)

![image-20220624232436345](image/image-20220624232436345.png)

![image-20220624232444924](image/image-20220624232444924.png)



3、等待项目初始化完毕

等右下角跑完，再点击enable auth-import

![image-20220624232626198](image/image-20220624232626198.png)

![image-20220624232635994](image/image-20220624232635994.png)

4、观察maven仓库中多了什么东西？

5、IDEA中的Maven设置

![image-20220624232806183](image/image-20220624232806183.png)

这里设置是项目的设置,所以会出现这种情况,在file中选择other

settrings,setting,for,new,projects可以解决

![image-20220624232859712](image/image-20220624232859712.png)

6、到这里，Maven在IDEA中的配置和使用就OK了！



#### 5.7、创建一个普通的Maven项目

![image-20220624233002505](image/image-20220624233002505.png)



![image-20220624233011130](image/image-20220624233011130.png)

![image-20220624233025722](image/image-20220624233025722.png)



#### 5.8、标记文件夹功能

![image-20220624233246254](image/image-20220624233246254.png)

![image-20220624233250729](image/image-20220624233250729.png)

![image-20220624233732350](image/image-20220624233732350.png)

![image-20220624233740300](image/image-20220624233740300.png)

![image-20220624233752550](image/image-20220624233752550.png)

**友情提示不要用高版本的maven,用3.6.1**



#### 5.9、在IDEA中配置Tomcat

![image-20220624233837933](image/image-20220624233837933.png)

![image-20220624233913804](image/image-20220624233913804.png)

![image-20220624233919190](image/image-20220624233919190.png)

![image-20220624233941971](image/image-20220624233941971.png)

上图是artifacts

**解决警告问题**

为什么会有这个问题：我们访问一个网站，需要指定一个文件夹名字；

![image-20220624234052985](image/image-20220624234052985.png)

![image-20220624234130192](image/image-20220624234130192.png)

![image-20220624234145615](image/image-20220624234145615.png)

![image-20220624234246922](image/image-20220624234246922.png)



#### 5.10、pom文件

pom.xml是Maven的核心配置文件

![image-20220624234355768](image/image-20220624234355768.png)

![image-20220624235001056](image/image-20220624235001056.png)

![image-20220624235053369](image/image-20220624235053369.png)

![image-20220624235226570](image/image-20220624235226570.png)

最新版本和idea不兼容，3.62~3.63都不兼容

![image-20220624235252852](image/image-20220624235252852.png)

要用的

**Maven的高级之处在于，他会帮你导入这个jar包所依赖的其他jar**

![image-20220624235307636](image/image-20220624235307636.png)

maven由于他的约定大于配置，我们之后可以遇到我们写的配置文件，无法被导出或者生效的问题，解决方案：

![image-20220625001035702](image/image-20220625001035702.png)

#### 5.11、没有

#### 5.12、IDEA操作

![image-20220625001524900](image/image-20220625001524900.png)

![image-20220625001530977](image/image-20220625001530977.png)



#### 5.13解决遇到的问题

1、**Maven 3.6.2**

![image-20220625165716051](image/image-20220625165716051.png)

降级为3.6.1

2、**Tomcat闪退**

![image-20220625165843556](image/image-20220625165843556.png)

可以先cmd，再startup.bat，就可以查看闪退的原因了

3、**IDEA中每次都要重复配置Maven**

![image-20220625170155618](image/image-20220625170155618.png)

![image-20220625170159917](image/image-20220625170159917.png)

4、**Maven项目中Tomcat无法配置**

5、**Maven默认web项目中的web.xml版本问题**

![image-20220625170557576](image/image-20220625170557576.png)

#### 6、替换为webapp4.0版本和tomcat一致

![image-20220625175118536](image/image-20220625175118536.png)

#### 7、Maven仓库的使用

![image-20220625175416002](image/image-20220625175416002.png)

![image-20220625175427969](image/image-20220625175427969.png)

![image-20220625175434101](image/image-20220625175434101.png)

![image-20220625175440371](image/image-20220625175440371.png)

![image-20220625175454832](image/image-20220625175454832.png)

![image-20220625175458661](image/image-20220625175458661.png)

作用域一般可以删掉

正常情况应该导入完上面的包就OK了



# 6、Servlet

#### 6.1、Servlet简介

- Servlet就是sun公司开发动态web的一门技术
- Sun在这些API中提供了一个接口叫做：Servlet，如果你想开发一个Servlet程序，只需要完成两个小步骤：
   - 编写一个类，实现Servlet接口
   - 把开发好Java类部署到web服务器中。

**把实现了Servlet接口的Java程序叫做Servlet**



#### 6.2、HelloServlet

Servlet接口Sun公司有两个默认的实现类：HttpServlet，GenericServled

1、构建一个普通的Maven项目，删除sc目录，以后我们的学习就在这个项目里面建立Moudel； 这个空的工程就题Maven主工程；

2、关于Maven工程的理解：

父项目中会有

```xml
<modules>
	<module>servlet-01</module>
</modules>
```

子项目会有

```xml
<parent>
    <artifactId>javaweb-02-servlet</artifactId>
    <groupId>com.kuang</groupId>
    <version>1.0-SNAPSHOT</version>
</parent>
```

父项目中的java子项目可以直接使用  相当于：

```java
son extends father
```

3、Maven环境优化

- 修改web.xml为最新的（现在是web4.0）
- 将maven的结构搭建完整

4、编写一个Servlet程序

- 编写一个普通类
- 实现Servlet接口，这里我们直接继承HttpServlet

```java
public class HelloServlet extends HttpServlet {
    //由于get或者post只是请求实现的不同的方式，可以相互调用，业务逻辑都一样；
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse
        resp) throws ServletException, IOException {
        //ServletOutputStream outputStream = resp.getOutputStream();
        PrintWriter writer = resp.getWriter(); //响应流
        writer.print("Hello,Serlvet");
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse
        resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

5、编写Serlvet映射

`为什么要编写映射`：

我们写的是Java程序，但是要通过浏览器访问，而浏览器需要连接web服务器，所以我们需要在web服务器中注册我们写的Servlet，还需给他一个浏览器能够访问的路径；

```xml
<!--注册Servlet-->
<servlet>
    <servlet-name>hello</servlet-name>
    <servlet-class>com.kuang.servlet.HelloServlet</servlet-class>
</servlet>
    <!--Servlet的请求路径-->
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
```

6、配置Tomcat

注意：配置项目发布的路径就可以了

![image-20220626234648177](image/image-20220626234648177.png)

![image-20220626234701742](image/image-20220626234701742.png)

7、 启动测试，OK！

![image-20220626234721552](image/image-20220626234721552.png)



#### 6.3、Servlet原理

Servlet是由Web服务器调用，web服务器在收到浏览器请求之后，会：

![image-20220628231555070](image/image-20220628231555070.png)



#### 6.4、Mapping问题

1、一个Servlet可以指定一个映射路径

```xml
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
```

2、一个Servlet可以指定多个映射路径

```xml
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello2</url-pattern>
</servlet-mapping>
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello3</url-pattern>
</servlet-mapping>
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello4</url-pattern>
</servlet-mapping>
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello5</url-pattern>
</servlet-mapping>
```

3、一个Servlet可以指定通用映射路径

```xml
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello/*</url-pattern>
</servlet-mapping>
```

4、默认请求路径

```xml
<!--默认请求路径-->
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/*</url-pattern>
</servlet-mapping>
```

5、指定一些后缀或者前缀等等....
**注意： .*前面不能加项目映射的路径 **

```xml
<!--可以自定义后缀实现请求映射
注意点，*前面不能加项目映射的路径
hello/sajdlkajda.qinjiang
-->
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>*.qinjiang</url-pattern>
</servlet-mapping>
```

6、优先级问题：

指定了固有的映射路径优先级最高，如果找不到就会走默认的处理请

```xml
<!--404-->
<servlet>
    <servlet-name>error</servlet-name>
    <servlet-class>com.kuang.servlet.ErrorServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>error</servlet-name>
    <url-pattern>/*</url-pattern>
</servlet-mapping>
```



#### 6.5、ServletContext

web容器在启动的时候，它会为每个web程序都创建一个对应的ServletContext对象，它代表了当前的web应用；

> 共享数据

在这个Servlet中保存的数据，可以在另外一个Servlet中拿到；

```java
package com.kuang.servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @description:
 * @author: GuoCL
 * @date: 2022/6/30
 */
public class HelloServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //this.getInitParameter() 初始化参数
        //this.getServletConfig() Servlet配置
        //this.getServletContext() Servlet上下文
        ServletContext context = this.getServletContext();

        //数据
        String username = "秦疆";
        //将一个数据保存在了ServletContext中，名字为：username 。值 username
        context.setAttribute("username", username);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

```java
package com.kuang.servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @description:
 * @author: GuoCL
 * @date: 2022/6/30
 */
public class GetServlet extends HelloServlet{
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext();
        String userName = (String) context.getAttribute("username");

        resp.setContentType("text/html");
        resp.setCharacterEncoding("UTF-8");
        resp.getWriter().print("名字"+userName);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.kuang.servlet.HelloServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
    
    <servlet>
        <servlet-name>getc</servlet-name>
        <servlet-class>com.kuang.servlet.GetServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>getc</servlet-name>
        <url-pattern>/getc</url-pattern>
    </servlet-mapping>
    
</web-app>
```

结果：先访问hello放数据

再getc取数据

![image-20220630235712237](image/image-20220630235712237.png)

> 获取初始化参数
>

```java
package com.kuang.servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @description:
 * @author: GuoCL
 * @date: 2022/7/1
 */
public class ServletDemo03 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws
            ServletException, IOException {
        ServletContext context = this.getServletContext();
        String url = context.getInitParameter("url");
        resp.getWriter().print(url);

    }



}

```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!--  配置一些web应用初始化参数  -->
    <context-param>
        <param-name>url</param-name>
        <param-value>jdbc:mysql://localhost:3306/mybatis</param-value>
    </context-param>

    <servlet>
        <servlet-name>demo03</servlet-name>
        <servlet-class>com.kuang.servlet.ServletDemo03</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>demo03</servlet-name>
        <url-pattern>/demo03</url-pattern>
    </servlet-mapping>
    
</web-app>
```

> 请求转发

```java
package com.kuang.servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @description:
 * @author: GuoCL
 * @date: 2022/7/1
 */
public class ServletDemo04 extends HelloServlet{

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws
            ServletException, IOException {
        ServletContext context = this.getServletContext();
        System.out.println("进入了ServletDemo04");
        //RequestDispatcher requestDispatcher = context.getRequestDispatcher("/gp"); //转发的请求路径
        //requestDispatcher.forward(req,resp); //调用forward实现请求转发；
        context.getRequestDispatcher("/demo03").forward(req,resp);
    }

}

```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!--  配置一些web应用初始化参数  -->
    <context-param>
        <param-name>url</param-name>
        <param-value>jdbc:mysql://localhost:3306/mybatis</param-value>
    </context-param>

    <servlet>
        <servlet-name>demo03</servlet-name>
        <servlet-class>com.kuang.servlet.ServletDemo03</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>demo03</servlet-name>
        <url-pattern>/demo03</url-pattern>
    </servlet-mapping>

    <servlet>
        <servlet-name>demo04</servlet-name>
        <servlet-class>com.kuang.servlet.ServletDemo04</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>demo04</servlet-name>
        <url-pattern>/demo04</url-pattern>
    </servlet-mapping>
    
</web-app>
```

![image-20220701002041487](image/image-20220701002041487.png)

请求转发：A不能直接访问C，只能通过B来访问C  ----- url不会改变

重定向：A可以访问B和C，当A访问B时，B告诉A得访问C，A就会跳转到C   ----    url会改变



> idea中web、favorites、structure作用
>

![image-20220701002808158](image/image-20220701002808158.png)

最佳答案：https://blog.csdn.net/lz710117239/article/details/104175842

Structure：

![image-20220701002938756](image/image-20220701002938756.png)



![](image/image-20220701003838760.png)



> 读取资源文件
>

Properties

- 在java目录下新建properties
- 在resources目录下新建properties

发现：都被打包到了同一个路径下：classes，我们俗称这个路径为classpath；

思路：需要一个文件流

```properties
username=root12312
password=zxczxczxc
```

读取resources下的properties

读取com.kuang.servlet下的properties

```java
public class ServletDemo05 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
throws ServletException, IOException {
    InputStream is = this.getServletContext().getResourceAsStream("/WEBINF/classes/com/kuang/servlet/aa.properties");
    Properties prop = new Properties();
    prop.load(is);
    String user = prop.getProperty("username");
    String pwd = prop.getProperty("password");
    resp.getWriter().print(user+":"+pwd);
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp)
throws ServletException, IOException {
    doGet(req, resp);
    }
}

```

访问测试即可

#### 6.6、HttpServletResponse

web服务器收接到客户端的http请求，针对这个请求，分别创建一个代表请求的HttpServletRequest对象，代表相应的一个HttpServletResponse；

- 如果要获取客户端请求过来的参数：找HttpServletRequest
- 如果要给客户端相应一些信息：找HttpServletResponse

> 简单分类
>

负责向浏览器发送数据的方法

```java
servletOutputstream getOutputstream() throws IOException;
Printwriter getwriter() throws IOException;
```

负责向浏览器发送响应头的方法 

```java
void setCharacterEncoding(String var1)；
void setContentLength(int var1)；
void setContentLengthLong(long var1);
void setContentType(String var1)；
void setDateHeader(String varl,long var2)
void addDateHeader(String var1,long var2)
void setHeader(String var1,String var2);
void addHeader(String var1,String var2)；
void setIntHeader(String var1,int var2);
void addIntHeader(String varl,int var2);
```

响应的状态码

![image-20220705221605766](image/image-20220705221605766.png)



> 下载文件

1、向浏览器输出消息（一直讲，就不说了）

2、下载文件

​	1.要获取下载文件的路径

​	2.下载的文件名是啥？

​	3.设置想办法让浏览器能够支持下载我们需要的东西

​	4.获取下载文件的输入流

​	5.创建缓冲区

​	6.获取OutputStream对象

​	7.将FileOutputStream流写入到bufer缓冲区

​	8.使用OutputStream将缓冲区中的数据输出到客户端

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp)
throws ServletException, IOException {
    // 1. 要获取下载文件的路径
    String realPath = "F:\\班级管理\\西开【19525】\\2、代码\\JavaWeb\\javaweb02-servlet\\response\\target\\classes\\秦疆.png";
    System.out.println("下载文件的路径："+realPath);
    // 2. 下载的文件名是啥？
    String fileName = realPath.substring(realPath.lastIndexOf("\\") + 1);
    // 3. 设置想办法让浏览器能够支持(Content-Disposition)下载我们需要的东西,中文文
    件名URLEncoder.encode编码，否则有可能乱码
    resp.setHeader("ContentDisposition","attachment;filename="+URLEncoder.encode(fileName,"UTF-8"));
    // 4. 获取下载文件的输入流
    FileInputStream in = new FileInputStream(realPath);
    // 5. 创建缓冲区
    int len = 0;
    byte[] buffer = new byte[1024];
    // 6. 获取OutputStream对象
    ServletOutputStream out = resp.getOutputStream();
    // 7. 将FileOutputStream流写入到buffer缓冲区,使用OutputStream将缓冲区中的数据
    输出到客户端！
    while ((len=in.read(buffer))>0){
    	out.write(buffer,0,len);
    }
    in.close();
    out.close();
}
```



> 验证码功能

验证怎么来的？

- 前端实现
- 后端实现，需要用到Java的图片类，生成一个图片

```java
package com.kuang.servlet;
import javax.imageio.ImageIO;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.io.IOException;
import java.util.Random;

public class ImageServlet extends HttpServlet {
    
        @Override
        protected void doGet(HttpServletRequest req, HttpServletResponse resp)
     throws ServletException, IOException {
            //如何让浏览器3秒自动刷新一次;
            resp.setHeader("refresh","3");
            //在内存中创建一个图片
            BufferedImage image = new
            BufferedImage(80,20,BufferedImage.TYPE_INT_RGB);
            //得到图片
            Graphics2D g = (Graphics2D) image.getGraphics(); //笔
            //设置图片的背景颜色
            g.setColor(Color.white);
            g.fillRect(0,0,80,20);
            //给图片写数据
            g.setColor(Color.BLUE);
            g.setFont(new Font(null,Font.BOLD,20));
            g.drawString(makeNum(),0,20);
            //告诉浏览器，这个请求用图片的方式打开
            resp.setContentType("image/jpeg");
            //网站存在缓存，不让浏览器缓存
            resp.setDateHeader("expires",-1);
            resp.setHeader("Cache-Control","no-cache");
            resp.setHeader("Pragma","no-cache");
            //把图片写给浏览器
            ImageIO.write(image,"jpg", resp.getOutputStream());
    	}
    
        //生成随机数
        private String makeNum(){
            Random random = new Random();
            String num = random.nextInt(9999999) + "";
            StringBuffer sb = new StringBuffer();
            for (int i = 0; i < 7-num.length() ; i++) {
                sb.append("0");
            }
            num = sb.toString() + num;
            return num;
        }

        @Override
        protected void doPost(HttpServletRequest req, HttpServletResponse resp)
    throws ServletException, IOException {
        	doGet(req, resp);
        }
}

```

```xml
<servlet>
    <servlet-name>ImageServlet</servlet-name>
    <servlet-class>com.kuang.servlet.ImageServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>Imageservlet</servlet-name>
    <url-pattern>/img</url-pattern>
</servlet-mapping>
```



> 实现重定向

![image-20220705221637064](image/image-20220705221637064.png)

（B）一个web资源收到客户端（A）请求后，（B）它会通知（A）客户端去访问另一个（C）web资源，这个过程叫重定向

常见场景：

- 用户登录

```java
void sendRedirect(String var1) throws IOException;
```

测试：

```java
@override
protected void doGet(HttpservletRequest req, HttpservletResponse resp) throws
ServletException, IOException {
    resp. sendRedirect("/r/img");//重定向
    /*
    resp. setHeader("Location","/r/img");
    resp. setstatus (302);
    */
}

```

面试题：请你聊聊重定向和转发的区别？

相同点：

- 页面都会实现跳转

不同点：

- 请求转发的时候，url不会产生变化。 307
- 重定向的时候，url地址栏会发生变化。 302

![image-20220705221646922](image/image-20220705221646922.png)

**测试：写一个表单提交后进行重定向**

index.jsp

```html
<html>
    <body>
        <h2>Hel1o World!</h2>
        
        《%--这里超交的路径,需要寻找到项目的路径--%>
        <%--${pageContext.request.contextPath}代表当前的项目--%>
        <form action="${pageContext.request.contextPath}/login" method="get">
            用户名: <input type="text" name="username"> <br>
            密码: <input type="password" name="password"> <br>
            <input type="submit">
        </form>
    </body>
</html>

```

RequestTest.java

```java
public class RequestTest extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
    throws ServletException, IOException {
        //处理方求
        String username = req.getParameter( s: "username");
        String password = req.getParameter( s: "password");
        System.out.println(username+":"+password);
        resp.sendRedirect(s: "/r/success.jsp");
    }
}
```

重定向页面success.jsp

```jsp
<%@ page contentType="text/html; charset=UTF-8" language="java" %>
<html>
    <head>
    	<title>Title</title>
    </head>
    <body>
    	<h1>success</h1>
    </body>
</html>
```

web.xml配置

```xml
<servlet>
    <servlet-name>requset</servlet-name>
    <servlet-class>com. kuang. servlet. RequestTest</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>requset</servlet-name>
    <url-pattern>/login</url-pattern>
</servlet-mapping>
```

导入依赖的jar包

```xml
<dependencies>
    <!-- https://mvnrepository. com/artifact/javax. servLet/javax. servletopi -->
    <dependency>
        <groupld>javax.servlet</grouptd>
        <artifactId>javax. servlet-api</artifactId>
        <version>4.0.1</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/javax. servLet.jsp/javax.
    servLet.jsp-opi -->
    <dependency>
        <groupId>javax.servlet.jsp</groupld>
        <artifactId>javax. servlet.jsp-api</artifactId>
        <version>2.3.3</version>
    </dependency>
</dependencies>
```

 

#### 6.7、HttpServletRequest

HttpServletRequest代表客户端的请求，用户通过Http协议访问服务器，Http请求中的所有信息会被封装到HttpServletRequest，通过这个HttpServletRequest的方法，获得客户端的所有请求。

![image-20220705221724731](image/image-20220705221724731.png)

**获取参数，请求转发**

![image-20220705221733511](image/image-20220705221733511.png)



自己创建类，且需要继承HttpServlet类

```java
@Override
protected void doGet(HttpservletRequest req. HttpservletResponse resp)
throws ServletException, IOException {
    req. setcharacterEncoding("utf-8");
    resp.setcharacterEncoding("utf-8");
    String username = req.getParameter("username");
    String password = req.getParameter("password");
    String[] hobbys = req.getParameterValues("hobbys");
    System.out.println("==========");
    //后台接收中文乱码问题
    System. out.println(username);
    System. out.println(password);
    System. out.println(Arrays.tostring(hobbys));
    System. out.println("============");
    system. out.println(req.getContextPath());
    //通过请求转发
    //这里的/代表当前的web应用
    req.getRequestDispatcher("/success.jsp").forward(req,resp);
}
```

![image-20220705221744557](image/image-20220705221744557.png)



# 7、Cookie、Session

#### 7.1、会话

**会话**：用户打开一个浏览器，点击了很多超链接，访问多个web资源，关闭浏览器，这个过程可以称之为会话；

**有状态会话：**一个同学来过教室，下次再来教室，我们会知道这个同学，曾经来过，称之为有状态会话；

**你能怎么证明你是西开的学生？**

1、发票：  西开给你开发票

2、学校登记：西开标记你来过了

**一个网站，怎么证明你来过？**

客户端    服务器

1、第一次访问服务端给客户端一个信件，客户端下次访问服务端带上信件就可以了；cookie

2、服务器登记你来过了，下次你来的时候，服务器来匹配客户端；session



#### 7.2、保存会话的两种技术

> cookie

- 客户端技术（响应，请求）

> session
>

- 服务器技术，利用这个技术，可以保存用户的会话信息。我们可以把信息或者数据放在session中！



常见：网站登录后，你下次就不用再登录了，第二次访问直接就上去了。



#### 7.3、Cookie

![image-20220705221801849](image/image-20220705221801849.png)



1、从请求中拿到cookie信息

2、服务器响应给客户端cookie

```java
Cookie[] cookies = req.getCookies(); //获得Cookie
cookie.getName(); //获得cookie中的key
cookie.getValue(); //获得cookie中的vlaue
new Cookie("lastLoginTime", System.currentTimeMillis()+""); //新建一个cookie
cookie.setMaxAge(24*60*60); //设置cookie的有效期
resp.addCookie(cookie); //响应给客户端一个cookie
```

**cookie：一般会保存在本地的 用户目录下appdata**



一个网站cookie是否存在上限！

- 一个cookie只能保存一个信息；
- 一个web站点可以给浏览器发送多个cookie，最多存放20个cookie；
- cookie大小有限制4kb；
- 300个cookie 浏览器上限



> 删除cookie

- 不设置有效日期，关闭浏览器，自动失效；
- 设置有效时间为0；



> 编码解码

```java
URLEncoder.encode("秦疆","utf-8")
URLDecoder.decode(cookie.getValue(),"UTF-8")
```



#### 7.4、Session（重点）

![image-20220712204239374](image/image-20220712204239374.png)

什么是Session：

- 服务器会给每一个**用户（浏览器）**创建一个Session对象；
- 一个Session独占一个浏览器，只要浏览器没有关闭，这个Session就存在；
- 用户登录之后，整个网站它都可以访问！ --》保存用户的信息；保存购物车信息。......



> Session和Cookie的区别

- Cookie是把用户的数据写给用户的浏览器，浏览器保存（可以保存多个）
- Session把用户的数据写到用户独占Session中，服务器端保存 （保存重要的信息，减少服务器资 源的浪费）
- Session对象由服务器创建；



> 使用场景

- 保存一个登录用户的信息；
- 购物车信息；
- 在整个网站中经常会使用的数据，我们把它保存在Session中



> 使用Session

```java
package com.kuang.servlet;
import com.kuang.pojo.Person;
import javax.servlet.ServletException;
import javax.servlet.http.*;
import java.io.IOException;
public class SessionDemo01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
throws ServletException, IOException {
    //解决乱码问题
    req.setCharacterEncoding("UTF-8");
    resp.setCharacterEncoding("UTF-8");
    resp.setContentType("text/html;charset=utf-8");
    //得到Session
    HttpSession session = req.getSession();
    //给Session中存东西
    session.setAttribute("name",new Person("秦疆",1));
    //获取Session的ID
    String sessionId = session.getId();
    //判断Session是不是新创建
    if (session.isNew()){
    	resp.getWriter().write("session创建成功,ID:"+sessionId);
    }else {
        resp.getWriter().write("session以及在服务器中存在
        了,ID:"+sessionId);
    }
        //Session创建的时候做了什么事情；
        // Cookie cookie = new Cookie("JSESSIONID",sessionId);
        // resp.addCookie(cookie);
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp)
throws ServletException, IOException {
    	doGet(req, resp);
    }
}
```

```java
//得到Session
HttpSession session = req.getSession();
Person person = (Person) session.getAttribute("name");
System.out.println(person.toString());
HttpSession session = req.getSession();
session.removeAttribute("name");
//手动注销Session
session.invalidate();
```



> 会话自动过期：web.xml配置

```xml
<!--设置Session默认的失效时间-->
<session-config>
	<!--15分钟后Session自动失效，以分钟为单位-->
	<session-timeout>15</session-timeout>
</session-config>
```

![image-20220712204405497](image/image-20220712204405497.png)



# 8、JSP



#### 8.1、什么是JSP

Java Server Pages：Java服务端页面，也和Servlet一样，用于动态Web技术！

最大特点：

- 写JSP就像在写HTML
- 区别：
   - HTML只给用户提供静态的数据；
   - JSP页面中可以嵌入JAVA代码，为用户提供动态数据；



#### 8.2、JSP原理

思路：JSP到底怎么执行的！

- 代码层面没有任何问题

- 服务器内部工作

   - tomcat中有一个work目录；
   - IDEA中使用tomcat的会在IDEA的tomcat中产生一个work目录

![image-20220712204927025](image/image-20220712204927025.png)

 狂神电脑的地址： C:\Users\Administrator.IntelliJIdea2018.1\system\tomcat\Unnamed_javaweb-sessioncookie\work\Catalina\localhost\ROOT\org\apache\jsp

![image-20220712204951124](image/image-20220712204951124.png)



**浏览器向服务器发送请求，不管访问什么资源（JSP），其实都是在访问Servlet**

JSP最终也会被转换成为一个Java类！

**JSP本质上就是一个Servlet**

```java
//初始化
public void _jspInit() {
}
//销毁
public void _jspDestroy() {
}
//JSPService
public void _jspService(.HttpServletRequest request,HttpServletResponse
response)
```

1、判断请求

2、内置一些对象

```java
final javax.servlet.jsp.PageContext pageContext; //页面上下文
javax.servlet.http.HttpSession session = null; //session
final javax.servlet.ServletContext application; //applicationContext
final javax.servlet.ServletConfig config; //config
javax.servlet.jsp.JspWriter out = null; //out
final java.lang.Object page = this; //page：当前页面
HttpServletRequest request //请求
HttpServletResponse response //响应
```

3、输出页面前增加的代码

```java
response.setContentType("text/html"); //设置响应的页面类型
pageContext = _jspxFactory.getPageContext(this, request, response,
null, true, 8192, true);
_jspx_page_context = pageContext;
application = pageContext.getServletContext();
config = pageContext.getServletConfig();
session = pageContext.getSession();
out = pageContext.getOut();
_jspx_out = out;
```

以上的这些个对象我们可以在JSP页面中直接使用！

![image-20220712205046094](image/image-20220712205046094.png)

讲解：

在JSP页面中；

只要是JAVA代码就会原封不动的输出；

如果是HTML代码，就会被转换为：

```java
out.write("<html>\r\n");
```

这样的格式，输出到前端！

#### 8.3、JSP基础语法

任何语言都有自己的语法，JAVA中有。JSP作为java技术的一种应用，它拥有一些自己扩充的语法（了 解，知道即可！），Java所有语法都支持！



> JSP表达式

```jsp
<%--JSP表达式
作用：用来将程序的输出，输出到客户端
<%= 变量或者表达式%>
--%>
<%= new java.util.Date()%>
```



> JSP脚本片段

```jsp
<%--jsp脚本片段--%>
<%
    int sum = 0;
    for (int i = 1; i <=100 ; i++) {
    sum+=i;
    }
    out.println("<h1>Sum="+sum+"</h1>");
%>
```



> 脚本片段的再实现

```jsp
<%
    int x = 10;
    out.println(x);
%>
<p>这是一个JSP文档</p>
<%
    int y = 2;
    out.println(y);
%>
<hr>
<%--在代码嵌入HTML元素--%>
<%
	for (int i = 0; i < 5; i++) {
%>
	<h1>Hello,World <%=i%> </h1>
<%
	}
%>
```



> JSP声明

```jsp
<%!
    static {
    	System.out.println("Loading Servlet!");
    }
    private int globalVar = 0;
    public void kuang(){
   		System.out.println("进入了方法Kuang！");
    }
%>

```

**jsp声明：会被编译到JSP生成的Java的类中！其他的，就会被生成到_jspService方法中！**

在jsp，嵌入Java代码即可！

```jsp
<%%>   jsp脚本片段
<%=%>  jsp表达式
<%!%>  jsp声明

<%--注释--%>
```

JSP的注释（<%----%>），不会在客户端的代码检查中显示，HTML（<!---->）的就会



#### 8.4、JSP指令

```jsp
<%@page args.... %>
<%@include file=""%>

<%--@include会将两个页面合二为一--%>
<%@include file="common/header.jsp"%>
<h1>网页主体</h1>
<%@include file="common/footer.jsp"%>

<hr>

<%--jSP标签
jsp:include：拼接页面，本质还是   三个
--%>
<jsp:include page="/common/header.jsp"/>
<h1>网页主体</h1>
<jsp:include page="/common/footer.jsp"/>
```



> IDEA启动小技巧

![image-20220712205311152](image/image-20220712205311152.png)



#### 8.5、9大内置对象

- PageContext    存东西
- Request        存东西
- Response    
- Session      存东西
- Application     【SerlvetContext】   存东西
- Config    【ServletConfig】
- out    输出
- page   不用了解
- exception   异常



```java
pageContext.setAttribute("name1","秦疆1号"); //保存的数据只在一个页面中有效
request.setAttribute("name2","秦疆2号"); //保存的数据只在一次请求中有效，请求转发会携带这个数据
session.setAttribute("name3","秦疆3号"); //保存的数据只在一次会话中有效，从打开浏览器到关闭浏览器
application.setAttribute("name4","秦疆4号"); //保存的数据只在服务器中有效，从打开服务器到关闭服务器
```

request：客户端向服务器发送请求，产生的数据，用户看完了就没用了，比如：新闻。

session：客户端向服务器发送请求，产生的数据，用户用完一会还有用。比如：购物车。

application：客户端向服务器发送请求，产生的数据，一个用户用完了，其他用户还可能使用，比如：聊天数据。

![image-20220712205412808](image/image-20220712205412808.png)

![image-20220713212559923](image/image-20220713212559923.png)

> JSP页面取值方式

使用EL表达式在页面上取值

${}   等价于  <%=%>

假如页面上变量a为空，使用${a}取值：页面就不会显示

使用 <%=a%>取值，页面会显示null



> JSP页面转发

```java
pageContext.forward("/index.jsp");
// 相当于在后端写
request.getRequestDispatcher("index.jsp").forward(request,response);
```



> JVM双亲委派机制

相关文章：https://blog.csdn.net/xishining/article/details/124693243

1、Java类加载的过程

Java类的加载过程是动态的，它不会一次性把程序所有的类全部加载后再运行，而是先保障程序运行的基础类加载到JVM虚拟机中，其他的类，一般是再需要的时候才会去加载，这样的运行机制也达到了节约内存的目的。

当JVM虚拟机加载某个class文件的时候，采用的是双亲委派模式（任务委派模式），就是将请求交给父类去处理。

2、类装载的方式

隐式装载：程序在运行过程中当碰到通过new 等方式生成对象时，隐式调用类装载器加载对应的类到JVM中。

显式装载：通过class.forName()等方法，显式加载需要的类

3、双亲委派机制的概念

双亲委派机制是指当一个类加载器收到某个类加载请求时，该类加载器首先会把请求委派给父类加载器。每个类加载器都是如此，它会先委托给父类加载器在自己的搜索范围内找不到对应的类时，该类加载器才会去尝试自己加载。

4、双亲委派模式的工作流程

![image-20220712205817098](image/image-20220712205817098.png)

Application ClassLoader（写的项目） 收到一个类加载请求时，首先它自己不会先去尝试加载这个类，而是先将这个加载请求委派给父类加载器Extension ClassLoader（扩展类加载器<JAVA_HOME>\lib\ext）去加载。

如果Extension ClassLoader收到一个类加载请求时，先将加载请求委派给父类加载器Bootstrap ClassLoader（类的根目录<JAVA_HOME>\lib）去完成。

如果Bootstrap ClassLoader加载失败(在<JAVA_HOME>\lib中未找到所需类)，就会让Extension ClassLoader尝试加载，如果加载成功了就不再让Extension ClassLoader加载，过程结束。

如果Extension ClassLoader也加载失败，就会使用Application ClassLoader加载如果加载成功了就不再让Application ClassLoader加载，过程结束。

如果Application ClassLoader也加载失败，就会使用自定义加载器去尝试加载。

如果所有的加载都失败了，就会抛出ClassNotFoundException异常。

理解：执行的情况都是由Bootstrap ClassLoader先加载，失败了轮到Extension ClassLoader加载，再失败了轮到Application ClassLoader，最后轮到自定义加载器加载。一般情况下大家写的java程序都是Application ClassLoader进行加载的。



5、双亲委派模型的核心代码

```java
protected Class<?> loadClass(String name, boolean resolve) throws ClassNotFoundException
{
    synchronized (getClassLoadingLock(name)) {
    // 首先，检查这类是否已经被加载过了
        Class<?> c = findLoadedClass(name);
        if (c == null) {
            long t0 = System.nanoTime();
            try {
                if (parent != null) {
                    //如果存在父类加载器，则取找该类的父类加载器
                    c = parent.loadClass(name, false);
                } else {
                    //返回由引导类加载器加载的类；如果未找到，则返回 null。
                    c = findBootstrapClassOrNull(name);
                }
            } catch (ClassNotFoundException e) {
                // 如果父类加载器抛出ClassNotFoundException异常
                // 则说明父类加载器无法完成加载请求
            }
 
            if (c == null) {
                // 在父类加载器无法加载时
                // 再调用本身的findClass方法来进行加载
                long t1 = System.nanoTime();
                c = findClass(name);
 
                // 这是定义类加载器；记录统计数据
                sun.misc.PerfCounter.getParentDelegationTime().addTime(t1 - t0);
                sun.misc.PerfCounter.getFindClassTime().addElapsedTimeFrom(t1);
                sun.misc.PerfCounter.getFindClasses().increment();
            }
        }
        if (resolve) {
            resolveClass(c);
        }
        return c;
    }
}
```

6、双亲委派机制的作用

- 防止加载同一个class文件。通过委托的方式去询问父级是否已经加载过该class，如果加载过了就不需要重新加载了。从而保证了数据安全。
- 通过委托的方式，保证JAVA核心class不被篡改，即使被篡改也不会被加载，即使被加载也不会是同一个class对象，因为不同的加载器加载同一个.class也不是同一个Class对象。这样则保证了Class的执行安全。



#### 8.6、JSP标签、JSTL标签、EL表达式

```xml
<!-- JSTL表达式的依赖 -->
<dependency>
    <groupId>javax.servlet.jsp.jstl</groupId>
    <artifactId>jstl-api</artifactId>
    <version>1.2</version>
</dependency>
<!-- standard标签库 -->
<dependency>
    <groupId>taglibs</groupId>
    <artifactId>standard</artifactId>
    <version>1.1.2</version>
</dependency>
```



> EL表达式：${}

- 获取数据
- 执行运算
- 获取web开发的常用对象



> JSP标签

```jsp
<%--jsp:include 引入其他页面--%>
<%--
http://localhost:8080/jsptag.jsp?name=kuangshen&age=12   转发页面并携带参数
--%>
<jsp:forward page="/jsptag2.jsp">
    <jsp:param name="name" value="kuangshen"></jsp:param>
    <jsp:param name="age" value="12"></jsp:param>
</jsp:forward>
```



> JSTL表达式

JSTL标签库的使用就是为了弥补HTML标签的不足；它自定义许多标签，可以提供我们使用，标签的功能和Java代码一样！

**格式化标签** 

**SQL标签** 

**XML 标签** 

**核心标签 （掌握部分）**

![image-20220712205856039](image/image-20220712205856039.png)



> JSTL标签库使用步骤

- 引入对应的taglib
- 使用其中的方法
- **在Tomcat也需要引入jstl包，否则会报错：JSTL解析错误**

```elm
下面说下<%@ page isELIgnored="false"%>的作用：

在每个JSP中可以指定该JSP是否使用EL。在page directive中的isELIgnored属性用来指定是否忽略。格式为：

＜%@ page isELIgnored＝"true|false"%＞

如果设定为true，也就是EL被忽略，那么JSP中的表达式被当成字符串处理。
```

**参数调用**

```jsp
 <input type="text" name="username" value="${param.username}">
${param.username}
```



c：if

```jsp
<head>
	<title>Title</title>
</head>
<body>
<h4>if测试</h4>
<hr>
<form action="coreif.jsp" method="get">
    <%--
    EL表达式获取表单中的数据
    ${param.参数名}
    --%>
    <input type="text" name="username" value="${param.username}">
    <input type="submit" value="登录">
</form>
<%--判断如果提交的用户名是管理员，则登录成功--%>
<c:if test="${param.username=='admin'}" var="isAdmin">
	<c:out value="管理员欢迎您！"/>
</c:if>
<%--自闭合标签--%>
<c:out value="${isAdmin}"/>
</body>

```

c:choose c:when

```jsp
<body>
<%--定义一个变量score，值为85--%>
<c:set var="score" value="55"/>
<c:choose>
    <c:when test="${score>=90}">
    你的成绩为优秀
    </c:when>
    <c:when test="${score>=80}">
    你的成绩为一般
    </c:when>
    <c:when test="${score>=70}">
    你的成绩为良好
    </c:when>
    <c:when test="${score<=60}">
    你的成绩为不及格
    </c:when>
</c:choose>
</body>
```

c:forEach

```jsp
<%
    ArrayList<String> people = new ArrayList<>();
    people.add(0,"张三");
    people.add(1,"李四");
    people.add(2,"王五");
    people.add(3,"赵六");
    people.add(4,"田六");
    request.setAttribute("list",people);
%>
<%--
    var , 每一次遍历出来的变量
    items, 要遍历的对象
    begin, 哪里开始
    end, 到哪里
    step, 步长
--%>
<c:forEach var="people" items="${list}">
	<c:out value="${people}"/> <br>
</c:forEach>
<hr>
<c:forEach var="people" items="${list}" begin="1" end="3" step="1" >
	<c:out value="${people}"/> <br>
</c:forEach>
```



# 9、JavaBean

实体类

JavaBean有特定性的写法：

- 必须有一个无参构造
- 属性必须私有化
- 必须有对应的get/set方法

**一般用来和数据库的字段做映射ORM**

ORM ：对象关系映射 

- 表--->类 
- 字段-->属性 
- 行记录---->对象

**people表**

![image-20220713225749873](image/image-20220713225749873.png)

```java
class People{
    private int id;
    private String name;
    private int id;
    private String address;
}

class A{
    new People(1,"秦疆1号",3，"西安");
    new People(2,"秦疆2号",3，"西安");
    new People(3,"秦疆3号",3，"西安");
}
```



# 10、MVC三层架构

- 什么是MVC：Model、View、Controller     模型、视图、控制器



#### 10.1、以前的架构

![image-20220713225820939](image/image-20220713225820939.png)

用户直接访问控制层，控制层就可以直接操作数据库；

```java
servlet--CRUD-->数据库
弊端：程序十分臃肿，不利于维护
servlet的代码中：处理请求、响应、视图跳转、处理JDBC、处理业务代码、处理逻辑代码
架构：没有什么是加一层解决不了的！
程序猿调用
↑
JDBC （实现该接口）
↑
Mysql Oracle SqlServer ....（不同厂商）
```



#### 10.2、MVC三层架构

![image-20220713225841942](image/image-20220713225841942.png)

Model

- 业务处理：业务逻辑（service）
- 数据持久层：CRUD（Dao-数据持久化对象）

View

- 展示数据
- 提供链接发起Servlet请求（a，form，img......）

Controller（Servlet）

- 接收用户的请求：（req：请求参数、Session信息）
- 交给业务层处理对应的代码
- 控制视图的跳转

```java
登录--->接收用户的登录请求--->处理用户的请求（获取用户登录的参数，username，
password）---->交给业务层处理登录业务（判断用户名密码是否正确：事务）--->Dao层查询
用户名和密码是否正确-->数据库
```



# 11、Filter（重点）

比如Shiro安全框架技术就是用Filter来实现的

Filter：过滤器，用来过滤网站的数据；

- 处理中文乱码
- 登录验证

（比如用来过滤网上骂人的话，我***我自己 0-0）

![image-20220713225900409](image/image-20220713225900409.png)



> Filter开发步骤

1、导包

2、编写过滤器

- 导包不要错（注意）

![image-20220713225927548](image/image-20220713225927548.png)



实现Filter接口，重写对应的方法即可

```java
public class CharacterEncodingFilter implements Filter {
	//初始化：web服务器启动，就以及初始化了，随时等待过滤对象出现！
    public void init(FilterConfig filterConfig) throws ServletException {
    	System.out.println("CharacterEncodingFilter初始化");
    }
    //Chain : 链
    /*
    1. 过滤中的所有代码，在过滤特定请求的时候都会执行
    2. 必须要让过滤器继续同行
    chain.doFilter(request,response);
    */
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        request.setCharacterEncoding("utf-8");
        response.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=UTF-8");
        System.out.println("CharacterEncodingFilter执行前....");
        chain.doFilter(request,response); //让我们的请求继续走，如果不写，
        程序到这里就被拦截停止！
        System.out.println("CharacterEncodingFilter执行后....");
    }
    //销毁：web服务器关闭的时候，过滤器会销毁
    public void destroy() {
    	System.out.println("CharacterEncodingFilter销毁");
    }
}
```

3、在web.xml中配置 Filter

```xml
<filter>
    <filter-name>CharacterEncodingFilter</filter-name>
    <filter-class>com.kuang.filter.CharacterEncodingFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>CharacterEncodingFilter</filter-name>
    <!--只要是 /servlet的任何请求，会经过这个过滤器-->
    <url-pattern>/servlet/*</url-pattern>
    <!--<url-pattern>/*</url-pattern>-->
    <!-- 别偷懒写个 /* -->
</filter-mapping>

```

> ```xml
> [2022-12-29 10:09:24,626] 工件 filter:war exploded: 正在部署工件，请稍候…
> 29-Dec-2022 22:09:28.137 INFO [RMI TCP Connection(3)-127.0.0.1] org.apache.jasper.servlet.TldScanner.scanJars At least one JAR was scanned for TLDs yet contained no TLDs. Enable debug logging for this logger for a complete list of JARs that were scanned but no TLDs were found in them. Skipping unneeded JARs during scanning can improve startup time and JSP compilation time.
> 					filter初始化····
> [2022-12-29 10:09:28,285] 工件 filter:war exploded: 工件已成功部署
> [2022-12-29 10:09:28,285] 工件 filter:war exploded: 部署已花费 3,659 毫秒
> 29-Dec-2022 22:09:34.403 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deploying web application directory D:\Eclipse\Tomcat\webapps\manager
> 29-Dec-2022 22:09:34.481 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deployment of web application directory D:\Eclipse\Tomcat\webapps\manager has finished in 78 ms
> 				filter过滤前·····
> 				filter过滤后···
> D:\Eclipse\Tomcat\bin\catalina.bat stop
> Using CATALINA_BASE:   "C:\Users\zhang\AppData\Local\JetBrains\IntelliJIdea2021.3\tomcat\047ddbff-3cd6-4091-90e9-2c52f6484695"
> Using CATALINA_HOME:   "D:\Eclipse\Tomcat"
> Using CATALINA_TMPDIR: "D:\Eclipse\Tomcat\temp"
> Using JRE_HOME:        "C:\Program Files\Java\jdk1.8.0_261"
> Using CLASSPATH:       "D:\Eclipse\Tomcat\bin\bootstrap.jar;D:\Eclipse\Tomcat\bin\tomcat-juli.jar"
> 29-Dec-2022 22:09:54.789 INFO [main] org.apache.catalina.core.StandardServer.await A valid shutdown command was received via the shutdown port. Stopping the Server instance.
> 29-Dec-2022 22:09:54.789 INFO [main] org.apache.coyote.AbstractProtocol.pause Pausing ProtocolHandler ["http-nio-8080"]
> 29-Dec-2022 22:09:54.848 INFO [main] org.apache.coyote.AbstractProtocol.pause Pausing ProtocolHandler ["ajp-nio-8009"]
> 29-Dec-2022 22:09:54.900 INFO [main] org.apache.catalina.core.StandardService.stopInternal Stopping service Catalina
> 				filter销毁中····
> ```



# 12、监听器

实现一个监听器的接口；（有N种监听器）

1、编写一个监听器

实现监听器的接口...

依赖的jar包

![image-20220713225955940](image/image-20220713225955940.png)

代码

```java
//统计网站在线人数 ： 统计session
public class OnlineCountListener implements HttpSessionListener {
    //创建session监听： 看你的一举一动
    //一旦创建Session就会触发一次这个事件！
    public void sessionCreated(HttpSessionEvent se) {
        ServletContext ctx = se.getSession().getServletContext();
        System.out.println(se.getSession().getId());
        Integer onlineCount = (Integer)
        ctx.getAttribute("OnlineCount");
        if (onlineCount==null){
        	onlineCount = new Integer(1);
        }else {
            int count = onlineCount.intValue();
            onlineCount = new Integer(count+1);
        }
        ctx.setAttribute("OnlineCount",onlineCount);
    }
    //销毁session监听
    //一旦销毁Session就会触发一次这个事件！
    public void sessionDestroyed(HttpSessionEvent se) {
        ServletContext ctx = se.getSession().getServletContext();
        Integer onlineCount = (Integer)
        ctx.getAttribute("OnlineCount");
        if (onlineCount==null){
        	onlineCount = new Integer(0);
        }else {
        	int count = onlineCount.intValue();
        	onlineCount = new Integer(count-1);
        }
        ctx.setAttribute("OnlineCount",onlineCount);
    }
    /*
    Session销毁：
    1. 手动销毁 getSession().invalidate();
    2. 自动销毁
    */
}
```

2、web.xml中注册监听器

```xml
<!--注册监听器-->
<listener>
	<listener-class>com.kuang.listener.OnlineCountListener</listenerclass>
</listener>
```

3、看情况是否使用！



# 13、过滤器、监听器常见应用

监听器：GUI（图形界面编程）编程中经常使用；

```java
public class TestPanel {
    public static void main(String[] args) {
        Frame frame = new Frame("中秋节快乐"); //新建一个窗体
        Panel panel = new Panel(null); //面板
        frame.setLayout(null); //设置窗体的布局
        frame.setBounds(300,300,500,500);
        frame.setBackground(new Color(0,0,255)); //设置背景颜色
        panel.setBounds(50,50,300,300);
        panel.setBackground(new Color(0,255,0)); //设置背景颜色
        frame.add(panel);
        frame.setVisible(true);
        //监听事件，监听关闭事件   
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
            	super.windowClosing(e);
            }
        });
    }
}

```

知识点：当实现一个接口不想重写里边的所有方法时，可以把这个接口变成抽象类，就可以实现想要的方法了。



> 用户登录程序思路

用户登录之后才能进入主页！用户注销后就不能进入主页了！

​	1、用户登录之后，向Session中放入用户的数据

​	2、进入主页的时候要判断用户是否已经登录；要求：在过滤中实现！

```java
HttpServletRequest request = (HttpServletRequest) req;
HttpServletResponse response = (HttpServletResponse) resp;
if (request.getSession().getAttribute(Constant.USER_SESSION)==null){
	response.sendRedirect("/error.jsp");
}
chain.doFilter(request,response);
```



# 14、JDBC

什么是JDBC：Java连接数据库！

![image-20220714201313651](image/image-20220714201313651.png)

需要jar包的支持：

- java.sql
- javax.sql
- mysql-conneter-java… 连接驱动（必须要导入）



实验环境搭建

```sql
CREATE TABLE users(
    id INT PRIMARY KEY,
    `name` VARCHAR(40),
    `password` VARCHAR(40),
    email VARCHAR(60),
    birthday DATE
);
INSERT INTO users(id,`name`,`password`,email,birthday)
VALUES(1,'张三','123456','zs@qq.com','2000-01-01');
INSERT INTO users(id,`name`,`password`,email,birthday)
VALUES(2,'李四','123456','ls@qq.com','2000-01-01');
INSERT INTO users(id,`name`,`password`,email,birthday)
VALUES(3,'王五','123456','ww@qq.com','2000-01-01');

SELECT * FROM users;
```



导入数据库依赖

```xml
<!--mysql的驱动-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.47</version>
</dependency>
```

IDEA中连接数据库：

![image-20220714201910698](image/image-20220714201910698.png)

**JDBC 固定步骤：** 

	1. 加载驱动 
	2. 连接数据库,代表数据库 
	3. 向数据库发送SQL的对象Statement : CRUD 
	4. 编写SQL （根据业务，不同的SQL）
	5. 执行SQL 
	6. 关闭连接（先开的后关）

```java
public class TestJdbc {
    public static void main(String[] args) throws ClassNotFoundException,SQLException {
        //配置信息
        //useUnicode=true&characterEncoding=utf-8 解决中文乱码
        String url="jdbc:mysql://localhost:3306/jdbc?
        useUnicode=true&characterEncoding=utf-8";
        String username = "root";
        String password = "123456";
        //1.加载驱动
        Class.forName("com.mysql.jdbc.Driver");
        //2.连接数据库,代表数据库
        Connection connection = DriverManager.getConnection(url, username,
        password);
        //3.向数据库发送SQL的对象Statement,PreparedStatement : CRUD
        Statement statement = connection.createStatement();
        //4.编写SQL
        String sql = "select * from users";
        //5.执行查询SQL，返回一个 ResultSet ： 结果集
        ResultSet rs = statement.executeQuery(sql);
        while (rs.next()){
            System.out.println("id="+rs.getObject("id"));
            System.out.println("name="+rs.getObject("name"));
            System.out.println("password="+rs.getObject("password"));
            System.out.println("email="+rs.getObject("email"));
            System.out.println("birthday="+rs.getObject("birthday"));
        }
        //6.关闭连接，释放资源（一定要做） 先开后关
        rs.close();
        statement.close();
        connection.close();
    }
}

```



**预编译SQL**

```java
public class TestJDBC2 {
    public static void main(String[] args) throws Exception {
        //配置信息
        //useUnicode=true&characterEncoding=utf-8 解决中文乱码
        String url="jdbc:mysql://localhost:3306/jdbc?
        useUnicode=true&characterEncoding=utf-8";
        String username = "root";
        String password = "123456";
        //1.加载驱动
        Class.forName("com.mysql.jdbc.Driver");
        //2.连接数据库,代表数据库
        Connection connection = DriverManager.getConnection(url, username,
        password);
        //3.编写SQL
        String sql = "insert into users(id, name, password, email,
        birthday) values (?,?,?,?,?);";
        //4.预编译
        PreparedStatement preparedStatement =connection.prepareStatement(sql);
        preparedStatement.setInt(1,2);//给第一个占位符？ 的值赋值为1；
        preparedStatement.setString(2,"狂神说Java");//给第二个占位符？ 的值赋值
        为狂神说Java；
        preparedStatement.setString(3,"123456");//给第三个占位符？ 的值赋值为
        123456；
        preparedStatement.setString(4,"24736743@qq.com");//给第四个占位符？ 的
        值赋值为1；
        preparedStatement.setDate(5,new Date(new
        java.util.Date().getTime()));//给第五个占位符？ 的值赋值为new Date(new
        java.util.Date().getTime())；
        //5.执行SQL
        int i = preparedStatement.executeUpdate();
        if (i>0){
        	System.out.println("插入成功@");
        }
        //6.关闭连接，释放资源（一定要做） 先开后关
        preparedStatement.close();
        connection.close();
    }
}
```



# 15、事务

要么都成功，要么都失败！

ACID原则：保证数据的安全。

```java
开启事务
事务提交 commit()
事务回滚 rollback()
关闭事务
    
转账：
A:1000
B:1000
    
A(900) --100--> B(1100)
```



**Junit单元测试**

依赖

```xml
<!--单元测试-->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
</dependency>
```

简单使用 

@Test注解只有在方法上有效，只要加了这个注解的方法，就可以直接运行！

```java
@Test
public void test(){
	System.out.println("Hello");
}
```

成功

![image-20220714215126175](image/image-20220714215126175.png)

失败的时候是红色的：

![image-20220714215340729](image/image-20220714215340729.png)



**搭建一个环境**

```sql
CREATE TABLE account(
    id INT PRIMARY KEY AUTO_INCREMENT,
    `name` VARCHAR(40),
    money FLOAT
);
INSERT INTO account(`name`,money) VALUES('A',1000);
INSERT INTO account(`name`,money) VALUES('B',1000);
INSERT INTO account(`name`,money) VALUES('C',1000);
```

```java
@Test
public void test() {
    //配置信息
    //useUnicode=true&characterEncoding=utf-8 解决中文乱码
    String url="jdbc:mysql://localhost:3306/jdbc?
    useUnicode=true&characterEncoding=utf-8";
    String username = "root";
    String password = "123456";
    Connection connection = null;
    //1.加载驱动
    try {
        Class.forName("com.mysql.jdbc.Driver");
        //2.连接数据库,代表数据库
        connection = DriverManager.getConnection(url, username, password);
        //3.通知数据库开启事务,false 开启
        connection.setAutoCommit(false);
        String sql = "update account set money = money-100 where name ='A'";
        connection.prepareStatement(sql).executeUpdate();
        //制造错误
        //int i = 1/0;
        String sql2 = "update account set money = money+100 where name = 'B'";
        connection.prepareStatement(sql2).executeUpdate();
        connection.commit();//以上两条SQL都执行成功了，就提交事务！
        System.out.println("success");
    } catch (Exception e) {
        try {
            //如果出现异常，就通知数据库回滚事务
            connection.rollback();
        } catch (SQLException e1) {
            e1.printStackTrace();
        }
    	e.printStackTrace();
    }finally {
        try {
        	connection.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

https://blog.csdn.net/bell_love/article/details/106157413





# 16、SMBMS项目

手敲代码gitee地址：https://gitee.com/guo_chunlin/gcl_product

项目架构

![img](https://img-blog.csdnimg.cn/20200516122458676.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70)



数据库：

![img](https://img-blog.csdnimg.cn/20200516122532275.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70)



**项目如何搭建？**
考虑是不是用maven？ jar包，依赖



### 16.1、搭建项目准备工作

1、搭建一个maven web项目

2、配置Tomcat

3、测试是否能跑起来

4、导入项目中需要的jar包

jsp，Servlet，mysql驱动jstl，stand…

```xml
<dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
    </dependency>
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>5.1.47</version>
    </dependency>
    <dependency>
      <groupId>javax.servlet.jsp</groupId>
      <artifactId>jsp-api</artifactId>
      <version>2.2</version>
    </dependency>
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>4.0.1</version>
    </dependency>
    <dependency>
      <groupId>taglibs</groupId>
      <artifactId>standard</artifactId>
      <version>1.1.2</version>
    </dependency>
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>jstl</artifactId>
      <version>1.2</version>
    </dependency>
    <dependency>
        <groupId>org.codehaus.plexus</groupId>
        <artifactId>plexus-utils</artifactId>
        <version>3.0</version>
    </dependency>
    <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>fastjson</artifactId>
      <version>1.2.78</version>
    </dependency>
  </dependencies>
```

5、构建项目包结构

![在这里插入图片描述](https://img-blog.csdnimg.cn/202005161230352.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70)



6、编写实体类

1. ROM映射:表-类映射



7、编写基础公共类
	1.数据库配置文件（mysql5.xx和8.xx的编写有差异）

```properties
driver=com.mysql.jdbc.Driver
#在和mysql传递数据的过程中，使用unicode编码格式，并且字符集设置为utf-8
url=jdbc:mysql://127.0.0.1:3306/smbms?useSSL=false&useUnicode=true&characterEncoding=utf-8
user=root
password=root
```



​	2.编写数据库的公共类（BaseDao.java）

```java
package com.kuang.dao;

import java.io.IOException;
import java.io.InputStream;
import java.sql.*;
import java.util.Properties;

/**
 * @description:操作数据库的基类--静态类
 * @author: GuoCL
 * @date: 2022/7/23
 */
public class BaseDao {
    static {//静态代码块，在类加载的时候执行
        init();
    }

    private static String driver;
    private static String url;
    private static String user;
    private static String password;

    // 初始化连接参数，从配置文件里获得
    public static void init(){
        Properties params = new Properties();
        String configFile = "db.properties";
        InputStream is = BaseDao.class.getClassLoader().getResourceAsStream(configFile);
        try {
            params.load(is);
        } catch (IOException e) {
            e.printStackTrace();
        }
        driver=params.getProperty("driver");
        url=params.getProperty("url");
        user=params.getProperty("user");
        password=params.getProperty("password");
        
    }

    /**
     *@description:获取数据库连接
     *@param
     *@return {@link Connection}
     *@author: GuoCL
     *@date: 2022/07/23 01:00
     */
    public static Connection getConnection(){
        Connection connection = null;
        try {
            Class.forName(driver);
            connection = DriverManager.getConnection(url, user, password);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return connection;
    }

    /**
     *@description:查询操作
     *@param
     * @param connection
     * @param pstm
     * @param rs
     * @param sql
     * @param params
     *@return {@link ResultSet}
     *@author: GuoCL
     *@date: 2022/07/23 01:08
     */
    public static ResultSet execute(Connection connection, PreparedStatement pstm, 
                                    ResultSet rs, String sql, Object[] params) throws Exception {
        pstm = connection.prepareStatement(sql);
        for (int i = 0; i < params.length; i++) {
            pstm.setObject(i+1, params[i]);
        }
        rs = pstm.executeQuery();
        return rs;
    }

    /**
     *@description:更新操作
     *@param
     * @param connection
     * @param pstm
     * @param sql
     * @param params
     *@return {@link int}
     *@author: GuoCL
     *@date: 2022/07/23 01:15
     */
    public static int execute(Connection connection, PreparedStatement pstm,
                              String sql, Object[] params) throws Exception {
        int updateRows = 0;
        pstm = connection.prepareStatement(sql);
        for (int i = 0; i < params.length; i++) {
            pstm.setObject(i+1, params[i]);
        }
        System.out.println("修改方法SQL---》" + pstm);
        updateRows = pstm.executeUpdate();
        System.out.println("修改方法返回值---》" + updateRows);
        return updateRows;
    }

    /**
     *@description:释放资源
     *@param
     * @param connection
     * @param pstm
     * @param rs
     *@return {@link boolean}
     *@author: GuoCL
     *@date: 2022/07/23 01:22
     */
    public static boolean closeResource(Connection connection, PreparedStatement pstm,
                                        ResultSet rs){
        boolean flag = true;
        if (rs != null){
            try {
                rs.close();
                //GC回收
                rs = null;
            } catch (SQLException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
                flag = false;
            }
        }
        if (pstm != null){
            try {
                pstm.close();
                //GC回收
                pstm = null;
            } catch (SQLException e) {
                e.printStackTrace();
                flag = false;
            }
        }
        if (connection != null){
            try {
                connection.close();
                //GC回收
                connection = null;
            } catch (SQLException e) {
                e.printStackTrace();
                flag = false;
            }
        }
        return flag;
    }
}
```

​	3.编写字符编码过滤器

```java
package com.kuang.filter;

import javax.servlet.*;
import java.io.IOException;

/**
 * 字符编码过滤器
 * 过滤所有请求
 */
public class CharacterEncoding implements Filter {
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        servletRequest.setCharacterEncoding("UTF-8");
        servletResponse.setCharacterEncoding("UTF-8");
        filterChain.doFilter(servletRequest, servletResponse);
    }

    public void destroy() {

    }
}
```

```xml
<!-- 字符编码过滤器 -->
  <filter>
    <filter-name>CharacterEncodingFilter</filter-name>
    <filter-class>com.kuang.filter.CharacterEncoding</filter-class>
  </filter>
  <filter-mapping>
    <filter-name>CharacterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>
```





8、导入静态资源



### 16.2、登录功能实现

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200516125301633.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70)



1、编写前端页面

2、设置首页

​	1.设置欢迎首页

```xml
<welcome-file-list>
    <welcome-file>login.jsp</welcome-file>
</welcome-file-list>
```

3、编写dao层用户登录的接口

```java
/**
     * 用户登录
     * @param connection
     * @param userCode
     * @return
     * @throws Exception
     */
    public User getLoginUser(Connection connection, String userCode) throws Exception;
```

4、编写dao层接口的实现类

```java
/**
     * 持久层只做查询数据库的内容
     * @param connection
     * @param userCode
     * @return
     */
    public User getLoginUser(Connection connection, String userCode) throws Exception {
        // 准备三个对象
        PreparedStatement pstm = null;
        ResultSet rs = null;
        User user = null;
        // 判断是否连接成功
        if (null != connection){
            String sql = "select * from smbms_user where userCode=?";
            Object[] params = {userCode};
            rs = BaseDao.execute(connection, pstm, rs, sql, params);
            if (rs.next()){
                user = new User();
                user.setId(rs.getInt("id"));
                user.setUserCode(rs.getString("userCode"));
                user.setUserName(rs.getString("userName"));
                user.setUserPassword(rs.getString("userPassword"));
                user.setGender(rs.getInt("gender"));
                user.setBirthday(rs.getDate("birthday"));
                user.setPhone(rs.getString("phone"));
                user.setAddress(rs.getString("address"));
                user.setUserRole(rs.getInt("userRole"));
                user.setCreatedBy(rs.getInt("createdBy"));
                user.setCreationDate(rs.getTimestamp("creationDate"));
                user.setModifyBy(rs.getInt("modifyBy"));
                user.setModifyDate(rs.getTimestamp("modifyDate"));
            }
            BaseDao.closeResource(null, pstm, rs);
        }

        return user;
    }
```

5、业务层接口

```java
/**
     * 用户登录
     * @param userCode
     * @param password
     * @return
     */
    public User login(String userCode, String password);
```

6、业务层实现类

```java
 /**
     *
     * @param userCode
     * @param password
     * @return
     */
    public User login(String userCode, String password) {
        Connection connection = null;
        //通过业务层调用对应的具体数据库操作
        User user = null;
        try {
            connection = BaseDao.getConnection();
            user = userDao.getLoginUser(connection, userCode);
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            BaseDao.closeResource(connection, null, null);
        }
        return user;
    }
```

7、编写Servlet

```java
package com.kuang.servlet.user;

import com.kuang.pojo.User;
import com.kuang.service.user.UserService;
import com.kuang.service.user.UserServiceImpl;
import com.kuang.util.Constants;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class LoginServlet extends HttpServlet {

    /**
     * 接收用户参数，调用业务层、转发视图
     * @param req
     * @param resp
     * @throws ServletException
     * @throws IOException
     */
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("login ============ ");
        //获取用户名和密码
        String userCode = req.getParameter("userCode");
        String userPassword = req.getParameter("userPassword");
        //调用service方法，进行用户匹配
        UserService userService = new UserServiceImpl();
        User user = userService.login(userCode, userPassword);
        if (user != null){
            //登录成功
            //放入Session
            req.getSession().setAttribute(Constants.USER_SESSION, user);
            //页面跳转（frame.jsp）
            resp.sendRedirect("jsp/frame.jsp");
        }else {
            //页面跳转（login.jsp）带出提示信息--转发
            req.setAttribute("error", "用户名或密码不正确");
            req.getRequestDispatcher("login.jsp").forward(req, resp);
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

8、注册Servlet

```xml
 <servlet>
    <servlet-name>LoginServlet</servlet-name>
    <servlet-class>com.kuang.servlet.user.LoginServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>LoginServlet</servlet-name>
    <url-pattern>/login.do</url-pattern>
  </servlet-mapping>
```

9、测试访问,保证以上功能可以成功。



### 16.3、登录功能优化

注销功能
思路：移除session，返回登录页面

```java
package com.kuang.servlet.user;

import com.kuang.util.Constants;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class LogoutServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //清除session
        req.getSession().removeAttribute(Constants.USER_SESSION);
        //返回登录页面
        resp.sendRedirect(req.getContextPath() + "/login.jsp");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

注册xml

```xml
<servlet>
    <servlet-name>LogoutServlet</servlet-name>
    <servlet-class>com.kuang.servlet.user.LogoutServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>LogoutServlet</servlet-name>
    <url-pattern>/jsp/logout.do</url-pattern>
  </servlet-mapping>
```



### 16.4、登录拦截优化

编写一个过滤器，并注册

```java
package com.kuang.filter;

import com.kuang.pojo.User;
import com.kuang.util.Constants;

import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class SysFilter implements Filter {
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        HttpServletRequest request = (HttpServletRequest) servletRequest;
        HttpServletResponse response = (HttpServletResponse) servletResponse;

        //过滤器，从session中获取用户
        User user = (User) request.getSession().getAttribute(Constants.USER_SESSION);
        if (user == null){
            //已经被移除或者注销了，或者未登录
            response.sendRedirect(request.getContextPath() + "/error.jsp");
        }else {
            filterChain.doFilter(request, response);
        }
    }

    public void destroy() {

    }
}
```

注册xml

```xml
<!-- 用户登录过滤器 -->
  <filter>
    <filter-name>SysFilter</filter-name>
    <filter-class>com.kuang.filter.SysFilter</filter-class>
  </filter>
  <filter-mapping>
    <filter-name>SysFilter</filter-name>
    <url-pattern>/jsp/*</url-pattern>
  </filter-mapping>
```

测试，登录，注销，权限，都要保证OK



### 16.5、密码修改

1、导入前端素材

2、写项目，建议从底层向上写

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200516180913135.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70)

3、UserDao接口

```java
/**
     * 修改密码
     * @param connection
     * @param id
     * @param password
     * @return
     */
    public int updatePwd(Connection connection, int id, String password) throws Exception;

```

4、UserDao接口实现类

```java
 /**
     * 修改当前密码
     * @param connection
     * @param id
     * @param password
     * @return
     */
    public int updatePwd(Connection connection, int id, String password) throws Exception {
        PreparedStatement pstm = null;
        int execute = 0;
        if (connection != null){
            String sql = "update smbms_user set userPassword = ? where id = ?";
            Object[] params = {password, id};
            execute = BaseDao.execute(connection, pstm, sql, params);
            BaseDao.closeResource(null, pstm, null);
        }
        return execute;
    }
```

5、UserService接口

```java
 /**
     * 修改密码
     * @param id
     * @param password
     * @return
     */
    public boolean updatePwd(int id, String password);
```

6、UserService实现类

```java
    public boolean updatePwd(int id, String password) {
        Connection connection = null;
        boolean flag = false;
        try {
            connection = BaseDao.getConnection();
            if (userDao.updatePwd(connection, id, password) > 0){
                flag = true;
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            BaseDao.closeResource(connection, null, null);
        }
        return flag;
    }
```

7、servlet记得实现复用，要提取出方法！
在 **dao层** 和 **service层** 自己写映射类和实现类
下面是 **servlet层** 的主体

```java
package com.kuang.servlet.user;

import com.alibaba.fastjson.JSONArray;
import com.kuang.pojo.Role;
import com.kuang.pojo.User;
import com.kuang.service.user.UserService;
import com.kuang.service.user.UserServiceImpl;
import com.kuang.servlet.Role.RoleService;
import com.kuang.servlet.Role.RoleServiceImpl;
import com.kuang.util.Constants;
import com.kuang.util.PageSupport;
import org.codehaus.plexus.util.StringUtils;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class UserServlet extends HttpServlet {

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("调用了UserServlet方法");
        //循环利用一个Servlet
        String method = req.getParameter("method");
        if (method != null){
            if ("savepwd".equals(method)){
                //调用修改密码方法
                updatePwd(req, resp);
            }
        }
    }

    /**
     * 调用修改密码方法
     * @param req
     * @param resp
     */
    public void updatePwd(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        Object o = req.getSession().getAttribute(Constants.USER_SESSION);
        String newPassword = req.getParameter("newpassword");
        boolean flag = false;
        if (o != null && StringUtils.isNotBlank(newPassword)){
            UserService userService = new UserServiceImpl();
            flag = userService.updatePwd(((User)o).getId(), newPassword);
        }
        if (flag) {
            req.setAttribute("message", "密码修改成功，请退出，使用新密码登录");
            // 密码修改成功,移除session(移除后不能再次修改密码,建议不移除)
            req.getSession().removeAttribute(Constants.USER_SESSION);
        }else {
            //修改密码失败
            req.setAttribute("message", "密码修改失败");
        }
        req.getRequestDispatcher("/jsp/pwdmodify.jsp").forward(req, resp);
    }

}
```

注册xml

```xml
<servlet>
    <servlet-name>UserServlet</servlet-name>
    <servlet-class>com.kuang.servlet.user.UserServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>UserServlet</servlet-name>
    <url-pattern>/jsp/user.do</url-pattern>
  </servlet-mapping>
```



8、测试



### 16.6、优化密码修改使用Ajax

1、阿里巴巴的fastjson

```xml
<!-- https://mvnrepository.com/artifact/com.alibaba/fastjson -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.68</version>
</dependency>
```

2、后台代码修改

导入阿里的包

```xml
<!-- https://mvnrepository.com/artifact/com.alibaba/fastjson -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.68</version>
</dependency>
```



```java
package com.kuang.servlet.user;

import com.alibaba.fastjson.JSONArray;
import com.kuang.pojo.Role;
import com.kuang.pojo.User;
import com.kuang.service.user.UserService;
import com.kuang.service.user.UserServiceImpl;
import com.kuang.servlet.Role.RoleService;
import com.kuang.servlet.Role.RoleServiceImpl;
import com.kuang.util.Constants;
import com.kuang.util.PageSupport;
import org.codehaus.plexus.util.StringUtils;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class UserServlet extends HttpServlet {

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("调用了UserServlet方法");
        //循环利用一个Servlet
        String method = req.getParameter("method");
        if (method != null){
            if ("savepwd".equals(method)){
                //调用修改密码方法
                updatePwd(req, resp);
            }else if ("pwdmodify".equals(method)){
                pwdmodify(req, resp);
            }else if ("ucexist".equals(method)){
                userCodeExist(req, resp);
            }
        }
    }

    /**
     * 判断用户账号是否可用
     * @param req
     * @param resp
     */
    public void userCodeExist(HttpServletRequest req, HttpServletResponse resp) throws IOException {
        String userCode = req.getParameter("userCode");

        HashMap<String, String> resultMap = new HashMap<String, String>();
        if (StringUtils.isBlank(userCode)) {
            //userCode == null || userCode.equals("")
            resultMap.put("userCode", "exist");
        } else {
            UserService userService = new UserServiceImpl();
            User user = userService.selectUserCodeExist(userCode);
            if (null != user) {
                resultMap.put("userCode", "exist");
            } else {
                resultMap.put("userCode", "notexist");
            }
        }
        //把roleList转换成json对象输出
        resp.setContentType("application/json");
        PrintWriter outPrintWriter = resp.getWriter();
        outPrintWriter.write(JSONArray.toJSONString(resultMap));
        outPrintWriter.flush();
        outPrintWriter.close();
    }

    /**
     * 调用修改密码方法
     * @param req
     * @param resp
     */
    public void updatePwd(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        Object o = req.getSession().getAttribute(Constants.USER_SESSION);
        String newPassword = req.getParameter("newpassword");
        boolean flag = false;
        if (o != null && StringUtils.isNotBlank(newPassword)){
            UserService userService = new UserServiceImpl();
            flag = userService.updatePwd(((User)o).getId(), newPassword);
        }
        if (flag) {
            req.setAttribute("message", "密码修改成功，请退出，使用新密码登录");
            // 密码修改成功,移除session(移除后不能再次修改密码,建议不移除)
            req.getSession().removeAttribute(Constants.USER_SESSION);
        }else {
            //修改密码失败
            req.setAttribute("message", "密码修改失败");
        }
        req.getRequestDispatcher("/jsp/pwdmodify.jsp").forward(req, resp);
    }

    /**
     * 验证旧密码
     * @param req
     * @param resp
     */
    public void pwdmodify(HttpServletRequest req, HttpServletResponse resp) throws IOException {
        Object o = req.getSession().getAttribute(Constants.USER_SESSION);
        String oldpassword = req.getParameter("oldpassword");
        Map<String, String> resultMap = new HashMap<String, String>();
        if (o==null){
            resultMap.put("result","seesionerror");
        }else if (StringUtils.isBlank(oldpassword)){
            //输入密码为空
            resultMap.put("result","error");
        }else {
            String userPassword = ((User)o).getUserPassword();//seesion中的用户密码
            if (oldpassword.equals(userPassword)){
                resultMap.put("result","true");
            }else {
                resultMap.put("result","false");
            }
        }

        //把map转换为接送格式输出
        resp.setContentType("application/json");
        PrintWriter outPrintWriter = resp.getWriter();
        outPrintWriter.write(JSONArray.toJSONString(resultMap));
        outPrintWriter.flush();
        outPrintWriter.close();


    }
}
```

3、测试



### 16.7、用户管理实现

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200517210107269.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70)



1. 导入分页的工具类-PageSupport
2. 用户列表页面导入-userlist.jsp



> 获取用户数量

1.userDao

```java
/**
     * 根据用户名或者角色查询用户总数
     * @param connection
     * @param username
     * @param userRole
     * @return
     */
    public int getUserCount(Connection connection, String username, int userRole) throws Exception;
```

2.UserDaoImpl

```java
/**
     * 根据用户名或者角色查询用户总数
     * @param connection
     * @param username
     * @param userRole
     * @return
     */
    public int getUserCount(Connection connection, String username, int userRole) throws Exception {
        PreparedStatement pstm = null;
        ResultSet rs = null;
        int count = 0;
        if (connection != null){
            StringBuffer sql = new StringBuffer();
            sql.append("select count(1) as count from smbms_user u, smbms_role r where u.userRole = r.id");
            List<Object> list = new ArrayList();
            if (StringUtils.isNotBlank(username)){
                sql.append(" and u.userName like ?");
                list.add("%" + username + "%");
            }
            if (userRole > 0){
                sql.append(" and u.userRole = ?");
                list.add(userRole);
            }
            Object[] params = list.toArray();
            System.out.println("sql ----> " + sql.toString());
            rs = BaseDao.execute(connection, pstm, rs, sql.toString(), params);
            if (rs.next()){
                count = rs.getInt("count");
            }
            BaseDao.closeResource(null, pstm, rs);
        }
        return count;
    }
```

3.UserService

```java
/**
     * 查询记录数
     * @param username
     * @param userRole
     * @return
     */
    public int getUserCount(String username, int userRole);
```

4.UserServiceImpl

```java
 /**
     * 查询记录数
     * @param queryUserName
     * @param queryUserRole
     * @return
     */
    public int getUserCount(String queryUserName, int queryUserRole) {
        Connection connection = null;
        int count = 0;
        System.out.println("queryUserName ---- > " + queryUserName);
        System.out.println("queryUserRole ---- > " + queryUserRole);
        try {
            connection = BaseDao.getConnection();
            count = userDao.getUserCount(connection, queryUserName, queryUserRole);
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            BaseDao.closeResource(connection, null, null);
        }
        return count;
    }

```



> #### 获取用户列表

1、UserDao

```java
 /**
     * 通过条件查询-userList
     * @param connection
     * @param userName
     * @param userRole
     * @param currentPageNo
     * @param pageSize
     * @return
     */
    public List<User> getUserList(Connection connection, String userName, int userRole, int currentPageNo, int pageSize) throws Exception;
```

2、UserDaoImpl

```java
 /**
     * 通过条件查询-userList
     * @param connection
     * @param userName
     * @param userRole
     * @param currentPageNo
     * @param pageSize
     * @return
     */
    public List<User> getUserList(Connection connection, String userName, int userRole, int currentPageNo, int pageSize) throws Exception {
        PreparedStatement pstm = null;
        ResultSet rs = null;
        List<User> userList = new ArrayList<User>();
        if (connection != null){
            StringBuffer sql = new StringBuffer();
            sql.append("select u.*, r.roleName as userRoleName from smbms_user u,smbms_role r where u.userRole = r.id");
            // 参数值
            List<Object> list = new ArrayList<Object>();
            if (StringUtils.isNotBlank(userName)) {
                sql.append(" and u.userName like ?");
                list.add("%" + userName + "%");
            }
            if (userRole > 0) {
                sql.append(" and u.userRole = ?");
                list.add(userRole);
            }
            // 在mysql数据库中，分页使用 limit  startIndex -->开始个数，pageSize -->查询个数; 总数
            sql.append(" order by creationDate DESC limit ?, ?");
            currentPageNo = (currentPageNo - 1) * pageSize;
            list.add(currentPageNo);
            list.add(pageSize);

            Object[] params = list.toArray();
            System.out.println("sql ----> " + sql.toString());
            rs = BaseDao.execute(connection, pstm, rs, sql.toString(), params);
            while (rs.next()) {
                User _user = new User();
                _user.setId(rs.getInt("id"));
                _user.setUserCode(rs.getString("userCode"));
                _user.setUserName(rs.getString("userName"));
                _user.setGender(rs.getInt("gender"));
                _user.setBirthday(rs.getDate("birthday"));
                _user.setPhone(rs.getString("phone"));
                _user.setUserRole(rs.getInt("userRole"));
                _user.setUserRoleName(rs.getString("userRoleName"));
                userList.add(_user);
            }
            BaseDao.closeResource(null, pstm, rs);
        }
        return userList;
    }
```

3、UserService

```java
 /**
     * 根据条件查询用户列表
     * @param queryUserName
     * @param queryUserRole
     * @param currentPageNo
     * @param pageSize
     * @return
     */
    public List<User> getUserList(String queryUserName, int queryUserRole, int currentPageNo, int pageSize);
```

4、UserServiceImpl

```java
 /**
     * 根据条件查询用户列表
     * @param queryUserName
     * @param queryUserRole
     * @param currentPageNo
     * @param pageSize
     * @return
     */
    public List<User> getUserList(String queryUserName, int queryUserRole, int currentPageNo, int pageSize) {
        Connection connection = null;
        List<User> userList = null;
        System.out.println("queryUserName ---- > " + queryUserName);
        System.out.println("queryUserRole ---- > " + queryUserRole);
        System.out.println("currentPageNo ---- > " + currentPageNo);
        System.out.println("pageSize ---- > " + pageSize);
        try {
            connection = BaseDao.getConnection();
            userList = userDao.getUserList(connection, queryUserName, queryUserRole, currentPageNo, pageSize);
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            BaseDao.closeResource(connection, null, null);
        }
        return userList;
    }
```



> #### 获取角色操作

为了我们的职责统一，我们可以把**角色的操作**单独放在一个包中，和pojo类对应。。。

1、RoleDao

```java
package com.kuang.dao.Role;

import com.kuang.pojo.Role;

import java.sql.Connection;
import java.util.List;

public interface RoleDao {

    /**
     * 获取角色列表
     * @param connection
     * @return
     */
    public List<Role> getRoleList(Connection connection) throws Exception;
}
```

2、RoleDaoIpml

```java
package com.kuang.dao.Role;

import com.kuang.dao.BaseDao;
import com.kuang.pojo.Role;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.util.ArrayList;
import java.util.List;

public class RoleDaoImpl implements RoleDao{

    /**
     * 获取角色列表
     * @param connection
     * @return
     */
    public List<Role> getRoleList(Connection connection) throws Exception {
        PreparedStatement pstm = null;
        ResultSet rs = null;
        List<Role> roleList = new ArrayList<Role>();
        if (connection != null) {
            String sql = "select * from smbms_role";
            Object[] params = {};
            rs = BaseDao.execute(connection, pstm, rs, sql, params);
            while (rs.next()) {
                Role _role = new Role();
                _role.setId(rs.getInt("id"));
                _role.setRoleCode(rs.getString("roleCode"));
                _role.setRoleName(rs.getString("roleName"));
                roleList.add(_role);
            }
            BaseDao.closeResource(null, pstm, rs);
        }

        return roleList;
    }
}
```

3、RoleService

```java
package com.kuang.service.Role;

import com.kuang.pojo.Role;

import java.util.List;

public interface RoleService {

    /**
     * 角色列表查询
     * @return
     */
    public List<Role> getRoleList();
}
```

4、RoleServiceIpml

```java
package com.kuang.service.Role;

import com.kuang.dao.BaseDao;
import com.kuang.dao.Role.RoleDao;
import com.kuang.dao.Role.RoleDaoImpl;
import com.kuang.pojo.Role;

import java.sql.Connection;
import java.util.List;

public class RoleServiceImpl implements RoleService{

    private RoleDao roleDao;
    public RoleServiceImpl(){
        roleDao = new RoleDaoImpl();
    }

    /**
     * 角色列表查询
     * @return
     */
    public List<Role> getRoleList() {
        Connection connection = null;
        List<Role> roleList = null;
        try {
            connection = BaseDao.getConnection();
            roleList = roleDao.getRoleList(connection);
        } catch (Exception e) {
            e.printStackTrace();
        }finally{
            BaseDao.closeResource(connection, null, null);
        }
        return roleList;
    }
}
```



> #### 用户显示的Servlet

1. 获取用户前端的数据（查询）
2. 判断请求是否需要执行，看参数的值判断
3. 为了实现分页，需要计算出当前页面和总页面，页面大小…
4. 用户列表展示
5. 返回前端

```java
package com.kuang.servlet.user;

import com.alibaba.fastjson.JSONArray;
import com.kuang.pojo.Role;
import com.kuang.pojo.User;
import com.kuang.service.user.UserService;
import com.kuang.service.user.UserServiceImpl;
import com.kuang.service.Role.RoleService;
import com.kuang.service.Role.RoleServiceImpl;
import com.kuang.util.Constants;
import com.kuang.util.PageSupport;
import org.codehaus.plexus.util.StringUtils;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class UserServlet extends HttpServlet {

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("调用了UserServlet方法");
        //循环利用一个Servlet
        String method = req.getParameter("method");
        if (method != null){
            if ("savepwd".equals(method)){
                //调用修改密码方法
                updatePwd(req, resp);
            }else if ("pwdmodify".equals(method)){
                pwdmodify(req, resp);
            }else if ("query".equals(method)){
                query(req, resp);
            }else if ("add".equals(method)){
                add(req, resp);
            }else if ("getrolelist".equals(method)){
                getrolelist(req, resp);
            }else if ("ucexist".equals(method)){
                userCodeExist(req, resp);
            }
        }
    }

    /**
     * 判断用户账号是否可用
     * @param req
     * @param resp
     */
    public void userCodeExist(HttpServletRequest req, HttpServletResponse resp) throws IOException {
        String userCode = req.getParameter("userCode");

        HashMap<String, String> resultMap = new HashMap<String, String>();
        if (StringUtils.isBlank(userCode)) {
            //userCode == null || userCode.equals("")
            resultMap.put("userCode", "exist");
        } else {
            UserService userService = new UserServiceImpl();
            User user = userService.selectUserCodeExist(userCode);
            if (null != user) {
                resultMap.put("userCode", "exist");
            } else {
                resultMap.put("userCode", "notexist");
            }
        }
        //把roleList转换成json对象输出
        resp.setContentType("application/json");
        PrintWriter outPrintWriter = resp.getWriter();
        outPrintWriter.write(JSONArray.toJSONString(resultMap));
        outPrintWriter.flush();
        outPrintWriter.close();
    }

    /**
     * 查询用户角色
     * @param req
     * @param resp
     */
    public void getrolelist(HttpServletRequest req, HttpServletResponse resp) throws IOException {
        RoleService roleService = new RoleServiceImpl();
        List<Role> roleList = roleService.getRoleList();
        //把roleList转换成json对象输出
        resp.setContentType("application/json");
        PrintWriter outPrintWriter = resp.getWriter();
        outPrintWriter.write(JSONArray.toJSONString(roleList));
        outPrintWriter.flush();
        outPrintWriter.close();
    }

    /**
     * 查询用户列表
     * @param req
     * @param resp
     */
    public void query(HttpServletRequest req, HttpServletResponse resp) {
        //从前端获取数据
        String queryUserName = req.getParameter("queryname");
        String temp = req.getParameter("queryUserRole");
        String pageIndex = req.getParameter("pageIndex");
        int queryUserRole = 0;

        //获取用户列表
        UserService userService = new UserServiceImpl();
        List<User> userList = null;

        //第一次走这个请求，一定是第一页，页面大小是固定的
        //设置页面容量
        int pageSize = 5;//把它设置在配置文件里,后面方便修改
        //当前页码
        int currentPageNo = 1;

        if (queryUserName == null) {
            queryUserName = "";
        }
        if (temp != null && !temp.equals("")){
            queryUserRole = Integer.parseInt(temp);
        }
        if (pageIndex != null){
            currentPageNo = Integer.parseInt(pageIndex);
        }
        //获取用户总数（分页	上一页：下一页的情况）
        //总数量（表）
        int totalCount = userService.getUserCount(queryUserName, queryUserRole);

        //总页数支持
        PageSupport pageSupport = new PageSupport();
        pageSupport.setCurrentPageNo(currentPageNo);
        pageSupport.setPageSize(pageSize);
        pageSupport.setTotalCount(totalCount);

        //总共有几页
        int totalPageCount =pageSupport.getTotalPageCount();

        //控制首页和尾页
        if (currentPageNo < 1){
            currentPageNo = 1;
        }else if (currentPageNo > totalPageCount){
            //如果页面大于了最后一页就显示最后一页
            currentPageNo = totalPageCount;
        }

        userList = userService.getUserList(queryUserName, queryUserRole, currentPageNo, pageSize);
        req.setAttribute("userList", userList);
        RoleServiceImpl roleService = new RoleServiceImpl();
        List<Role> roleList = roleService.getRoleList();
        req.setAttribute("roleList", roleList);
        req.setAttribute("totalCount", totalCount);
        req.setAttribute("currentPageNo", currentPageNo);
        req.setAttribute("totalPageCount", totalPageCount);
        req.setAttribute("queryUserName", queryUserName);
        req.setAttribute("queryUserRole", queryUserRole);

        //返回前端
        try {
            req.getRequestDispatcher("userlist.jsp").forward(req, resp);
        } catch (ServletException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }

    }

    /**
     * 调用修改密码方法
     * @param req
     * @param resp
     */
    public void updatePwd(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        Object o = req.getSession().getAttribute(Constants.USER_SESSION);
        String newPassword = req.getParameter("newpassword");
        boolean flag = false;
        if (o != null && StringUtils.isNotBlank(newPassword)){
            UserService userService = new UserServiceImpl();
            flag = userService.updatePwd(((User)o).getId(), newPassword);
        }
        if (flag) {
            req.setAttribute("message", "密码修改成功，请退出，使用新密码登录");
            // 密码修改成功,移除session(移除后不能再次修改密码,建议不移除)
            req.getSession().removeAttribute(Constants.USER_SESSION);
        }else {
            //修改密码失败
            req.setAttribute("message", "密码修改失败");
        }
        req.getRequestDispatcher("/jsp/pwdmodify.jsp").forward(req, resp);
    }

    /**
     * 验证旧密码
     * @param req
     * @param resp
     */
    public void pwdmodify(HttpServletRequest req, HttpServletResponse resp) throws IOException {
        Object o = req.getSession().getAttribute(Constants.USER_SESSION);
        String oldpassword = req.getParameter("oldpassword");
        Map<String, String> resultMap = new HashMap<String, String>();
        if (o==null){
            resultMap.put("result","seesionerror");
        }else if (StringUtils.isBlank(oldpassword)){
            //输入密码为空
            resultMap.put("result","error");
        }else {
            String userPassword = ((User)o).getUserPassword();//seesion中的用户密码
            if (oldpassword.equals(userPassword)){
                resultMap.put("result","true");
            }else {
                resultMap.put("result","false");
            }
        }

        //把map转换为接送格式输出
        resp.setContentType("application/json");
        PrintWriter outPrintWriter = resp.getWriter();
        outPrintWriter.write(JSONArray.toJSONString(resultMap));
        outPrintWriter.flush();
        outPrintWriter.close();


    }
}
```



# 17、文件上传下载

搭建环境等可参考：https://blog.csdn.net/qq_54897873/article/details/118551792?spm=1001.2101.3001.6650.7&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-7-118551792-blog-114682781.pc_relevant_multi_platform_featuressortv2removedup&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-7-118551792-blog-114682781.pc_relevant_multi_platform_featuressortv2removedup&utm_relevant_index=11

### 17.1、搭建环境

可参考上述链接

### 17.2、配置Tomcat以及下载jar包

配置Tomcat可参考上述链接

common-io以及common-fileupload包

[Maven Repository: commons-fileupload » commons-fileupload (mvnrepository.com)](https://mvnrepository.com/artifact/commons-fileupload/commons-fileupload)

[Maven Repository: commons-io » commons-io (mvnrepository.com)](https://mvnrepository.com/artifact/commons-io/commons-io)

### 17.3、文件上传原理

![img](https://img-blog.csdnimg.cn/20200708013333768.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTE0ODk5Nw==,size_16,color_FFFFFF,t_70#pic_center)

### 17.4、上传文件注意事项

![img](https://img-blog.csdnimg.cn/20200708013345217.png#pic_center)

### 17.5、需要用到的类

ServletFileUpload负责处理上传的文件数据，并将表单中每个输入项封装成一个FileItem对象，在使用ServletFileUpload对象解析请求时需要DiskFileItemFactory对象。所以哦，我们需要在进行解析工作前构造好DiskFileItemFactory对象，通过ServletFileUpload对象的构造方法或ServletFileItemFactory()方法设置ServletFileUpload对象的fileItemFactory属性

```tex
get: 上传文件大小有限制
post:上传文件大小无限制
```




> ### FileItem类

在HTML页面input必须有name < input type=“file” name=“filename” >

**表单如果包含一个文件上传输入项的话，这个表单的enctype属性就必须设置为multipart/form-date**

```html
<form action="" method="post" enctype="multipart/form-data">
  上传用户: <input type="text" name="username"><br>
  <p><input type="file" name="file1"></p>
  <p><input type="file" name="file2"></p>
  <p><input type="submit"> | <input type="reset"></p>
</form>
```

浏览器表单的类型如果为multipart/form-data，在服务器端想获取数据就要通过流。



> 常用方法介绍

```java
//isFormField方法用于判断FileItem类对象封装的数据是一个普通文本表单还是一个文件表单，如果是普通文本表单字段则返回true，否则返回false
boolean isFormField();

//getFieldName方法用于返回表单标签name属性的值
String getFieldName();
//getString方法用于将FileItem对象中保存的数据流内容以一个字符串返回
String getString();

//getName方法用于获得文件上传字段中的文件名
String getName();

//以流的形式返回上传文件的内容数据
InputStream getInputStream();

//delete方法用来清空FileItem类对象中存放的主体内容，如果主体内容呗保存在临时文件中，delete方法将删除该临时文件
void delete();
```



> ### ServletFileUploda类

ServletFileUploda负责处理上传的文件数据，并将表单中每个输入项封装成一个FileItem对象中，使用其parseRequest(HttpservletRequest)方法可以将通过表单中每一个HTML标签提交的数据封装成一个FileItem对象，然后以List列表的形式返回。使用该方法处理上传文件简答易用。



### 17.6、代码编写

UploadFileServlet

```java
package com.wang.servlet;

import org.apache.commons.fileupload.FileItem;
import org.apache.commons.fileupload.FileUploadException;
import org.apache.commons.fileupload.ProgressListener;
import org.apache.commons.fileupload.disk.DiskFileItemFactory;
import org.apache.commons.fileupload.servlet.ServletFileUpload;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.List;
import java.util.UUID;

public class FileServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //判断上传的文件是普通表单还是带文件的表单
        if (!ServletFileUpload.isMultipartContent(request)){
            return;//终止方法运行，说明这是一个普通的表单，直接返回
        }

        //创建上传文件的保存路径，建议在WEB-INF路径下，安全，用户无法直接访问上传的文件；
        String uploadPath = this.getServletContext().getRealPath("/WEB-INF/upload");
        File uploadFile = new File(uploadPath);
        if (uploadFile.exists()){//.exists()取反
            uploadFile.mkdir();//创建这个目录
        }

        //缓存，临时文件
        //临时路径，加入文件超过了预期的大小，我们就把它放到一个临时文件中，过几天自动删除，或者提醒用户转存为永久
        String tmpPath = this.getServletContext().getRealPath("/WEB-INF/upload");
        File file = new File(tmpPath);
        if (file.exists()){//.exists()取反
            file.mkdir();//创建这个临时目录
        }

        // 处理上传的文件,一般都需要通过流来获取,我们可以使用request.getInputstream(),原生态的文件上传流获取,十分麻烦
        // 但是我们都建议使用 Apache的文件上传组件来实现, common-fileupload,它需要依赖于commons-io组件;


        try {
            // 创建DiskFileItemFactory对象，处理文件路径或者大小限制
            DiskFileItemFactory factory = getDiskFileItemFactory(file);
            /*
             * //通过这个工厂设置一个缓冲区,当上传的文件大于这个缓冲区的时候,将他放到临时文件 factory.setSizeThreshold(1024 *
             * 1024); //缓存区大小为1M factory.setRepository (file);//临时目录的保存目录,需要一个File
             */

            // 2、获取ServletFileUpload
            ServletFileUpload upload = getServletFileUpload(factory);

            // 3、处理上传文件
            // 把前端请求解析，封装成FileItem对象，需要从ServletFileUpload对象中获取
            String msg = uploadParseRequest(upload, request, uploadPath);

            // Servlet请求转发消息
            System.out.println(msg);
            if(msg.equals("文件上传成功!")) {
                // Servlet请求转发消息
                request.setAttribute("msg",msg);
                request.getRequestDispatcher("info.jsp").forward(request, response);
            }else {
                msg ="请上传文件";
                request.setAttribute("msg",msg);
                request.getRequestDispatcher("info.jsp").forward(request, response);
            }

        } catch (FileUploadException e) {
            e.printStackTrace();
        }
    }

    public static DiskFileItemFactory getDiskFileItemFactory(File file) {
        DiskFileItemFactory factory = new DiskFileItemFactory();
        // 通过这个工厂设置一个缓冲区,当上传的文件大于这个缓冲区的时候,将他放到临时文件中;
        factory.setSizeThreshold(1024 * 1024);// 缓冲区大小为1M
        factory.setRepository(file);// 临时目录的保存目录,需要一个file
        return factory;
    }

    public static ServletFileUpload getServletFileUpload(DiskFileItemFactory factory) {
        ServletFileUpload upload = new ServletFileUpload(factory);
        // 监听上传进度
        upload.setProgressListener(new ProgressListener() {

            // pBYtesRead:已读取到的文件大小
            // pContextLength:文件大小
            public void update(long pBytesRead, long pContentLength, int pItems) {
                System.out.println("总大小：" + pContentLength + "已上传：" + pBytesRead);
            }
        });

        // 处理乱码问题
        upload.setHeaderEncoding("UTF-8");
        // 设置单个文件的最大值
        upload.setFileSizeMax(1024 * 1024 * 10);
        // 设置总共能够上传文件的大小
        // 1024 = 1kb * 1024 = 1M * 10 = 10м

        return upload;
    }

    public static String uploadParseRequest(ServletFileUpload upload, HttpServletRequest request, String uploadPath)
            throws FileUploadException, IOException {

        String msg = "";

        // 把前端请求解析，封装成FileItem对象
        List<FileItem> fileItems = upload.parseRequest(request);
        for (FileItem fileItem : fileItems) {
            if (fileItem.isFormField()) {// 判断上传的文件是普通的表单还是带文件的表单
                // getFieldName指的是前端表单控件的name;
                String name = fileItem.getFieldName();
                String value = fileItem.getString("UTF-8"); // 处理乱码
                System.out.println(name + ": " + value);
            } else {// 判断它是上传的文件

                // ============处理文件==============

                // 拿到文件名
                String uploadFileName = fileItem.getName();
                System.out.println("上传的文件名: " + uploadFileName);
                if (uploadFileName.trim().equals("") || uploadFileName == null) {
                    continue;
                }

                // 获得上传的文件名/images/girl/paojie.png
                String fileName = uploadFileName.substring(uploadFileName.lastIndexOf("/") + 1);
                // 获得文件的后缀名
                String fileExtName = uploadFileName.substring(uploadFileName.lastIndexOf(".") + 1);

                /*
                 * 如果文件后缀名fileExtName不是我们所需要的 就直按return.不处理,告诉用户文件类型不对。
                 */

                System.out.println("文件信息[件名: " + fileName + " ---文件类型" + fileExtName + "]");
                // 可以使用UID（唯一识别的通用码),保证文件名唯
                // 0UID. randomUUID(),随机生一个唯一识别的通用码;
                String uuidPath = UUID.randomUUID().toString();

                // ================处理文件完毕==============

                // 存到哪? uploadPath
                // 文件真实存在的路径realPath
                String realPath = uploadPath + "/" + uuidPath;
                // 给每个文件创建一个对应的文件夹
                File realPathFile = new File(realPath);
                if (!realPathFile.exists()) {
                    realPathFile.mkdir();
                }
                // ==============存放地址完毕==============


                // 获得文件上传的流
                InputStream inputStream = fileItem.getInputStream();
                // 创建一个文件输出流
                // realPath =真实的文件夹;
                // 差了一个文件;加上翰出文件的名产"/"+uuidFileName
                FileOutputStream fos = new FileOutputStream(realPath + "/" + fileName);
                System.out.println("path:"+realPath + "/" + fileName);
                // 创建一个缓冲区
                byte[] buffer = new byte[1024 * 1024];
                // 判断是否读取完毕
                int len = 0;
                // 如果大于0说明还存在数据;
                while ((len = inputStream.read(buffer)) > 0) {
                    fos.write(buffer, 0, len);
                }
                // 关闭流
                fos.close();
                inputStream.close();

                msg = "文件上传成功!";
                fileItem.delete(); // 上传成功,清除临时文件
                //=============文件传输完成=============
            }
        }
        return msg;

    }
}
```

编写info.jsp

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

配置xml

```xml
<servlet>
    <servlet-name>FileServlet</servlet-name>
    <servlet-class>com.wang.servlet.FileServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>FileServlet</servlet-name>
    <url-pattern>/upload.do</url-pattern>
</servlet-mapping>
```



# 18、基于JavaMail的Java邮件发送

### 18.1、邮件服务器与传输协议

- 要在网络上实现邮件功能，必须要有专门的邮件服务器。这些邮件服务器类似于现实生活中的邮局，它主要负责接收用户投递过来的邮件，并把邮件投递到邮件接收者的电子邮箱中。

- SMTP服务器地址：一般是 smtp.xxx.com，比如163邮箱是smtp.163.com，qq邮箱是smtp.qq.com。

- SMTP协议

  通常把处理用户smtp请求(邮件发送请求)的服务器称之为SMTP服务器(邮件发送服务器)。

- POP3协议

  通常把处理用户pop3请求(邮件接收请求)的服务器称之为POP3服务器(邮件接收服务器)。



### 18.2、Java发送邮件

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190720161625525.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Jhb2xpbmd5ZQ==,size_16,color_FFFFFF,t_70)



**1、使用到的jar包：**

mail.jar     http://www.java2s.com/Code/Jar/j/Downloadjavaxmailjar.htm
activation.jar   http://www.java2s.com/Code/Jar/j/Downloadjavaxactivation30preludejar.htm

**2、QQ邮箱需获取相应的权限：**

QQ邮箱–>邮箱设置–>账户–>POP3/IMAP/SMTP/Exchange/CardDAV/CalDAV服务 开启POP3/SMTP服务，然后获取16位授权码（注意不要将授权码泄露，一个账户可以拥有多个授权码）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190720161540301.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Jhb2xpbmd5ZQ==,size_16,color_FFFFFF,t_70)



### 18.3、**Java实现纯文本邮件发送**

```java
package org.westos.email;

import com.sun.mail.util.MailSSLSocketFactory;

import javax.mail.*;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;
import java.security.GeneralSecurityException;
import java.util.Properties;

public class SendEamil {
    public static void main(String[] args) throws MessagingException, GeneralSecurityException {
        //创建一个配置文件并保存
        Properties properties = new Properties();

        properties.setProperty("mail.host","smtp.qq.com");

        properties.setProperty("mail.transport.protocol","smtp");

        properties.setProperty("mail.smtp.auth","true");


        //QQ存在一个特性设置SSL加密
        MailSSLSocketFactory sf = new MailSSLSocketFactory();
        sf.setTrustAllHosts(true);
        properties.put("mail.smtp.ssl.enable", "true");
        properties.put("mail.smtp.ssl.socketFactory", sf);

        //创建一个session对象
        Session session = Session.getDefaultInstance(properties, new Authenticator() {
            @Override
            protected PasswordAuthentication getPasswordAuthentication() {
                return new PasswordAuthentication("619046217@qq.com","16位授权码");
            }
        });

        //开启debug模式
        session.setDebug(true);

        //获取连接对象
        Transport transport = session.getTransport();

        //连接服务器
        transport.connect("smtp.qq.com","619046217@qq.com","16位授权码");

        //创建邮件对象
        MimeMessage mimeMessage = new MimeMessage(session);

        //邮件发送人
        mimeMessage.setFrom(new InternetAddress("619046217@qq.com"));

        //邮件接收人
        mimeMessage.setRecipient(Message.RecipientType.TO,new InternetAddress("875203654@qq.com"));

        //邮件标题
        mimeMessage.setSubject("Hello Mail");

        //邮件内容
        mimeMessage.setContent("我的想法是把代码放进一个循环里","text/html;charset=UTF-8");

        //发送邮件
        transport.sendMessage(mimeMessage,mimeMessage.getAllRecipients());

        //关闭连接
        transport.close();
    }
}
```



### 18.4、**Java实现文本图片附件复杂的邮件发送**

1、MIME（多用途互联网邮件扩展类型）

- MimeBodyPart类

javax.mail.internet.MimeBodyPart类 表示的是一个MIME消息，它和MimeMessage类一样都是从Part接口继承过来。

- MimeMultipart类

javax.mail.internet.MimeMultipart是抽象类 Multipart的实现子类,它用来组合多个MIME消息。一个MimeMultipart对象可以包含多个代表MIME消息的MimeBodyPart对象

```java
package org.westos.email;

import com.sun.mail.util.MailSSLSocketFactory;

import javax.activation.DataHandler;
import javax.activation.FileDataSource;
import javax.mail.*;
import javax.mail.internet.*;
import java.security.GeneralSecurityException;
import java.util.Properties;

public class SendComplexEmail {
    public static void main(String[] args) throws GeneralSecurityException, MessagingException {
        Properties prop = new Properties();
        prop.setProperty("mail.host", "smtp.qq.com");  设置QQ邮件服务器
        prop.setProperty("mail.transport.protocol", "smtp"); // 邮件发送协议
        prop.setProperty("mail.smtp.auth", "true"); // 需要验证用户名密码

        // QQ邮箱设置SSL加密
        MailSSLSocketFactory sf = new MailSSLSocketFactory();
        sf.setTrustAllHosts(true);
        prop.put("mail.smtp.ssl.enable", "true");
        prop.put("mail.smtp.ssl.socketFactory", sf);

        //1、创建定义整个应用程序所需的环境信息的 Session 对象
        Session session = Session.getDefaultInstance(prop, new Authenticator() {
            @Override
            protected PasswordAuthentication getPasswordAuthentication() {
                //传入发件人的姓名和授权码
                return new PasswordAuthentication("619046217@qq.com","16位授权码");
            }
        });

        //2、通过session获取transport对象
        Transport transport = session.getTransport();

        //3、通过transport对象邮箱用户名和授权码连接邮箱服务器
        transport.connect("smtp.qq.com","619046217@qq.com","16位授权码");

        //4、创建邮件,传入session对象
        MimeMessage mimeMessage = complexEmail(session);

        //5、发送邮件
        transport.sendMessage(mimeMessage,mimeMessage.getAllRecipients());

        //6、关闭连接
        transport.close();


    }

    public static MimeMessage complexEmail(Session session) throws MessagingException {
        //消息的固定信息
        MimeMessage mimeMessage = new MimeMessage(session);

        //发件人
        mimeMessage.setFrom(new InternetAddress("619046217@qq.com"));
        //收件人
        mimeMessage.setRecipient(Message.RecipientType.TO,new InternetAddress("619046217@qq.com"));
        //邮件标题
        mimeMessage.setSubject("带图片和附件的邮件");

        //邮件内容
        //准备图片数据
        MimeBodyPart image = new MimeBodyPart();
        DataHandler handler = new DataHandler(new FileDataSource("E:\\IdeaProjects\\WebEmail\\resources\\测试图片.png"));
        image.setDataHandler(handler);
        image.setContentID("test.png"); //设置图片id

        //准备文本
        MimeBodyPart text = new MimeBodyPart();
        text.setContent("这是一段文本<img src='cid:test.png'>","text/html;charset=utf-8");

        //附件
        MimeBodyPart appendix = new MimeBodyPart();
        appendix.setDataHandler(new DataHandler(new FileDataSource("E:\\IdeaProjects\\WebEmail\\resources\\测试文件.txt")));
        appendix.setFileName("test.txt");

        //拼装邮件正文
        MimeMultipart mimeMultipart = new MimeMultipart();
        mimeMultipart.addBodyPart(image);
        mimeMultipart.addBodyPart(text);
        mimeMultipart.setSubType("related");//文本和图片内嵌成功

        //将拼装好的正文内容设置为主体
        MimeBodyPart contentText = new MimeBodyPart();
        contentText.setContent(mimeMultipart);

        //拼接附件
        MimeMultipart allFile = new MimeMultipart();
        allFile.addBodyPart(appendix);//附件
        allFile.addBodyPart(contentText);//正文
        allFile.setSubType("mixed"); //正文和附件都存在邮件中，所有类型设置为mixed


        //放到Message消息中
        mimeMessage.setContent(allFile);
        mimeMessage.saveChanges();//保存修改

        return mimeMessage;
    }
}
```



### 18.5、**JavaWeb发送邮件(网站注册成功发送提示邮件)**

1、User

```java
package org.westos.mail;

public class User {
    private String name;
    private String password;
    private String mail;

    public User() {
    }

    public User(String name, String password, String mail) {
        this.name = name;
        this.password = password;
        this.mail = mail;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getMail() {
        return mail;
    }

    public void setMail(String mail) {
        this.mail = mail;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                ", password='" + password + '\'' +
                ", mail='" + mail + '\'' +
                '}';
    }
}
```



2、Servlet

```java
package org.westos.mail;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class Servlet extends javax.servlet.http.HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doGet(request,response);
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) {
        //处理前端请求
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        String email = request.getParameter("email");

        //将信息封装进user对象
        User user = new User(username, password, email);

        SendMail sendMail = new SendMail(user);
        sendMail.start(); //开启线程

        request.setAttribute("msg","发送成功");
        try {
            request.getRequestDispatcher("msg.jsp").forward(request,response);
        } catch (ServletException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }


    }
}
```

3、**SengMail**

```java
package org.westos.mail;

import com.sun.mail.util.MailSSLSocketFactory;

import javax.mail.*;
import javax.mail.internet.AddressException;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;
import java.security.GeneralSecurityException;
import java.security.PublicKey;
import java.util.Properties;

public class SendMail extends Thread {
    //发件人信息
    private String From = "619046217@qq.com";
    //发件人邮箱
    private String recipient = "619046217@qq.com";
    //邮箱密码
    private String password = "16位授权码";
    //邮件发送的服务器
    private String host = "smtp.qq.com";

    //收件人信息
    private User user;
    public SendMail(User user){
        this.user = user;
    }

    @Override
    public void run() {
        try {
            Properties properties = new Properties();

            properties.setProperty("mail.host","smtp.qq.com");

            properties.setProperty("mail.transport.protocol","smtp");

            properties.setProperty("mail.smtp.auth","true");

            //QQ存在一个特性设置SSL加密
            MailSSLSocketFactory sf = null;
            try {
                sf = new MailSSLSocketFactory();
            } catch (GeneralSecurityException e) {
                e.printStackTrace();
            }
            sf.setTrustAllHosts(true);
            properties.put("mail.smtp.ssl.enable", "true");
            properties.put("mail.smtp.ssl.socketFactory", sf);

            //创建一个session对象
            Session session = Session.getDefaultInstance(properties, new Authenticator() {
                @Override
                protected PasswordAuthentication getPasswordAuthentication() {
                    return new PasswordAuthentication(recipient,password);
                }
            });

            //开启debug模式
            session.setDebug(true);

            //获取连接对象
            Transport transport = null;
            try {
                transport = session.getTransport();
            } catch (NoSuchProviderException e) {
                e.printStackTrace();
            }

            //连接服务器
            transport.connect(host,From,password);


            //创建一个邮件发送对象
            MimeMessage mimeMessage = new MimeMessage(session);
            //邮件发送人
            mimeMessage.setFrom(new InternetAddress(recipient));

            //邮件接收人
            mimeMessage.setRecipient(Message.RecipientType.TO,new InternetAddress(user.getMail()));

            //邮件标题
            mimeMessage.setSubject("网站注册成功");

            //邮件内容
            mimeMessage.setContent("网站注册成功，密码为"+user.getPassword()+"，请妥善保管密码","text/html;charset=UTF-8");

            //发送邮件
            transport.sendMessage(mimeMessage,mimeMessage.getAllRecipients());

            transport.close();

        }catch (Exception e){
            e.printStackTrace();
        }

    }

}
```

4、**register.jsp**

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>注册页面</title>
</head>
<body>

<form action="${pageContext.request.contextPath}/a.do" method="post">
    <p>用户名：<input type="text" name="username" required></p>
    <p>密码：<input type="password" name="password" required></p>
    <p>邮箱：<input type="email" name="email" required></p>
    <p><input type="submit" value="提交"></p>
</form>
</body>
</html>
```

5、**msg.jsp**

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

6、**web.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <servlet>
        <servlet-name>Servlet</servlet-name>
        <servlet-class>org.westos.mail.Servlet</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>Servlet</servlet-name>
        <url-pattern>/a.do</url-pattern>
    </servlet-mapping>
</web-app>
```



### 18.6、遇到一些问题

参考：

https://blog.csdn.net/qq_34823218/article/details/107131845?spm=1001.2101.3001.6650.5&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-5-107131845-blog-106379856.pc_relevant_multi_platform_whitelistv1&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-5-107131845-blog-106379856.pc_relevant_multi_platform_whitelistv1&utm_relevant_index=10









































