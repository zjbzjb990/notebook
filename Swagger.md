# Swagger

## 简介

### 前后端分离

vue+SpringBoot

- 后端：后端控制层，服务层，数据访问层
- 前端：前端控制层，视图层
  - 前后端交互方式：API接口
  - 前后端相对独立，松耦合
  - 前后端甚至可以部署到不同的服务器上面

## 2.Swagger

是世界上最流行的API框架

RestFull Api文档在线自动生成工具==》Api文档与API接口定义同步更新

直接运行，可以在线**测试API接口**

支持多种语言：java , Php

官网：API Documentation & Design Tools for Teams | Swagger

## 3.Springboot集成swagger

### 3.1创建项目

![image-20230223225935347](SpringBoot-images/image-20230223225935347.png)

### 3.2导入依赖

```xml
<dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-boot-starter</artifactId>
            <version>3.0.0</version>
        </dependency>
```



### 3.3创建Controller软件包

HelloController.java

```java
@RestController
public class HelloController {
    @RequestMapping("/hello")
    public String hello(){
        return "hello";
    }
}

```

运行

![image-20230223230417773](SpringBoot-images/image-20230223230417773.png)

### 3.4创建Config软件包

SwaggerConfig.java

```java
@Configuration
@EnableSwagger2   //开启swagger2
public class SwaggerConfig {
}
```

运行

![image-20230224000545761](SpringBoot-images/image-20230224000545761.png)

### 注：

若出现此报错

```java
Error starting ApplicationContext. To display the conditions report re-run your application with 'debug' enabled.
2023-02-23 23:43:43.298 ERROR 8860 --- [           main] o.s.boot.SpringApplication               : Application run failed

org.springframework.context.ApplicationContextException: Failed to start bean 'documentationPluginsBootstrapper'; nested exception is java.lang.NullPointerException
    at org.springframework.context.support.DefaultLifecycleProcessor.doStart(DefaultLifecycleProcessor.java:181) ~[spring-context-5.3.25.jar:5.3.25]
    at org.springframework.context.support.DefaultLifecycleProcessor.access$200(DefaultLifecycleProcessor.java:54) ~[spring-context-5.3.25.jar:5.3.25]
    at org.springframework.context.support.DefaultLifecycleProcessor$LifecycleGroup.start(DefaultLifecycleProcessor.java:356) ~[spring-context-5.3.25.jar:5.3.25]
    at java.lang.Iterable.forEach(Iterable.java:75) ~[na:1.8.0_261]
    at org.springframework.context.support.DefaultLifecycleProcessor.startBeans(DefaultLifecycleProcessor.java:155) ~[spring-context-5.3.25.jar:5.3.25]
    at org.springframework.context.support.DefaultLifecycleProcessor.onRefresh(DefaultLifecycleProcessor.java:123) ~[spring-context-5.3.25.jar:5.3.25]
    at org.springframework.context.support.AbstractApplicationContext.finishRefresh(AbstractApplicationContext.java:935) ~[spring-context-5.3.25.jar:5.3.25]
    at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:586) ~[spring-context-5.3.25.jar:5.3.25]
    at org.springframework.boot.web.servlet.context.ServletWebServerApplicationContext.refresh(ServletWebServerApplicationContext.java:147) ~[spring-boot-2.7.9.jar:2.7.9]
    at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:731) [spring-boot-2.7.9.jar:2.7.9]
    at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:408) [spring-boot-2.7.9.jar:2.7.9]
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:307) [spring-boot-2.7.9.jar:2.7.9]
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:1303) [spring-boot-2.7.9.jar:2.7.9]
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:1292) [spring-boot-2.7.9.jar:2.7.9]
    at com.zhang.SpringBootSwaggerApplication.main(SpringBootSwaggerApplication.java:10) [classes/:na]
Caused by: java.lang.NullPointerException: null
    at springfox.documentation.spring.web.WebMvcPatternsRequestConditionWrapper.getPatterns(WebMvcPatternsRequestConditionWrapper.java:56) ~[springfox-spring-webmvc-3.0.0.jar:3.0.0]
    at springfox.documentation.RequestHandler.sortedPaths(RequestHandler.java:113) ~[springfox-core-3.0.0.jar:3.0.0]
    at springfox.documentation.spi.service.contexts.Orderings.lambda$byPatternsCondition$3(Orderings.java:89) ~[springfox-spi-3.0.0.jar:3.0.0]
    at java.util.Comparator.lambda$comparing$77a9974f$1(Comparator.java:469) ~[na:1.8.0_261]
    at java.util.TimSort.countRunAndMakeAscending(TimSort.java:355) ~[na:1.8.0_261]
    at java.util.TimSort.sort(TimSort.java:220) ~[na:1.8.0_261]
    at java.util.Arrays.sort(Arrays.java:1512) ~[na:1.8.0_261]
    at java.util.ArrayList.sort(ArrayList.java:1464) ~[na:1.8.0_261]
    at java.util.stream.SortedOps$RefSortingSink.end(SortedOps.java:387) ~[na:1.8.0_261]
    at java.util.stream.Sink$ChainedReference.end(Sink.java:258) ~[na:1.8.0_261]
    at java.util.stream.Sink$ChainedReference.end(Sink.java:258) ~[na:1.8.0_261]
    at java.util.stream.Sink$ChainedReference.end(Sink.java:258) ~[na:1.8.0_261]
    at java.util.stream.Sink$ChainedReference.end(Sink.java:258) ~[na:1.8.0_261]
    at java.util.stream.AbstractPipeline.copyInto(AbstractPipeline.java:483) ~[na:1.8.0_261]
    at java.util.stream.AbstractPipeline.wrapAndCopyInto(AbstractPipeline.java:472) ~[na:1.8.0_261]
    at java.util.stream.ReduceOps$ReduceOp.evaluateSequential(ReduceOps.java:708) ~[na:1.8.0_261]
    at java.util.stream.AbstractPipeline.evaluate(AbstractPipeline.java:234) ~[na:1.8.0_261]
    at java.util.stream.ReferencePipeline.collect(ReferencePipeline.java:499) ~[na:1.8.0_261]
    at springfox.documentation.spring.web.plugins.WebMvcRequestHandlerProvider.requestHandlers(WebMvcRequestHandlerProvider.java:81) ~[springfox-spring-webmvc-3.0.0.jar:3.0.0]
    at java.util.stream.ReferencePipeline$3$1.accept(ReferencePipeline.java:193) ~[na:1.8.0_261]
    at java.util.ArrayList$ArrayListSpliterator.forEachRemaining(ArrayList.java:1384) ~[na:1.8.0_261]
    at java.util.stream.AbstractPipeline.copyInto(AbstractPipeline.java:482) ~[na:1.8.0_261]
    at java.util.stream.AbstractPipeline.wrapAndCopyInto(AbstractPipeline.java:472) ~[na:1.8.0_261]
    at java.util.stream.ReduceOps$ReduceOp.evaluateSequential(ReduceOps.java:708) ~[na:1.8.0_261]
    at java.util.stream.AbstractPipeline.evaluate(AbstractPipeline.java:234) ~[na:1.8.0_261]
    at java.util.stream.ReferencePipeline.collect(ReferencePipeline.java:499) ~[na:1.8.0_261]
    at springfox.documentation.spring.web.plugins.AbstractDocumentationPluginsBootstrapper.withDefaults(AbstractDocumentationPluginsBootstrapper.java:107) ~[springfox-spring-web-3.0.0.jar:3.0.0]
    at springfox.documentation.spring.web.plugins.AbstractDocumentationPluginsBootstrapper.buildContext(AbstractDocumentationPluginsBootstrapper.java:91) ~[springfox-spring-web-3.0.0.jar:3.0.0]
    at springfox.documentation.spring.web.plugins.AbstractDocumentationPluginsBootstrapper.bootstrapDocumentationPlugins(AbstractDocumentationPluginsBootstrapper.java:82) ~[springfox-spring-web-3.0.0.jar:3.0.0]
    at springfox.documentation.spring.web.plugins.DocumentationPluginsBootstrapper.start(DocumentationPluginsBootstrapper.java:100) ~[springfox-spring-web-3.0.0.jar:3.0.0]
    at org.springframework.context.support.DefaultLifecycleProcessor.doStart(DefaultLifecycleProcessor.java:178) ~[spring-context-5.3.25.jar:5.3.25]
    ... 14 common frames omitted


进程已结束,退出代码1
```

解决办法

```yaml
spring:
  mvc:
    pathmatch:
      matching-strategy: ant_path_matcher
```

## 4.配置Swagger

### 4.1Swagger的Bean实例Docket

SwaggerConfig.java

```java
package com.zhang.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import springfox.documentation.service.ApiInfo;
import springfox.documentation.service.Contact;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2;

import java.util.ArrayList;

@Configuration
@EnableSwagger2
public class SwaggerConfig {
    //配置Swagger的Bean实例
    @Bean
    public Docket docket(){
        return new Docket(DocumentationType.SWAGGER_2)
                .apiInfo(apiInfo());
    }

    //配置Swagger信息
    private ApiInfo apiInfo(){
        //作者信息
        Contact contact= new Contact("张", "http://www.zhang.com", "1419166829@qq.com");
        return new ApiInfo(
                "张学习Swagger3.0",
                "冲冲冲",
                "v1.0",
                "http://www.zhang.com",
                contact,
                "Apache 2.0",
                "http://www.apache.org/licenses/LICENSE-2.0",
                new ArrayList()
        );
    }
}
```

运行

![image-20230224003006610](SpringBoot-images/image-20230224003006610.png)

## 5.配置扫描接口及开关

### 5.1扫描接口

Docket.select()

```java
  //配置Swagger的Bean实例
    @Bean
    public Docket docket(){
        return new Docket(DocumentationType.SWAGGER_2)
                .select()
                //RequestHandlerSelectors,配置要扫描接口的方式
                .apis(RequestHandlerSelectors.basePackage("com.zhang.controller"))
                .build()
                .apiInfo(apiInfo());

    }
```

运行

这次界面就只有controller包下的hellocontroller接口

**![image-20230224004039232](SpringBoot-images/image-20230224004039232.png)**

```java
//配置Swagger的Bean实例
    @Bean
    public Docket docket(){
        return new Docket(DocumentationType.SWAGGER_2)
                .select()
                //RequestHandlerSelectors,配置要扫描接口的方式
                //basePackage 指定扫描的包
                //any() 扫描全部
                //none() 不扫描
                //withMethodAnnotation 扫描方法上的注解
                //withClassAnnotation 扫描类上的注解 参数是一个注解的反射对象
                .apis(RequestHandlerSelectors.basePackage("com.zhang.controller"))
                // .paths() 过滤 哪个路径  只扫描/zhang下的
                .paths(PathSelectors.ant("/zhang/**"))
//                .apis(RequestHandlerSelectors.withMethodAnnotation(GetMapping.class))
                .build()
                .apiInfo(apiInfo());

    }
```

### 5.2Swagger开关

```java
  //.enable() 是否启动Swagger；false or true
                .build()
                .enable(false)
                .apiInfo(apiInfo());
```



运行

![image-20230224005316349](SpringBoot-images/image-20230224005316349.png)

### 5.3问：Swagger在生产时使用，发布时不使用？

1. 判断是否为生产环境flag=false
2. 注入.enable(false)

1.生产环境-dev 发布环境-pro

application-dev.yml

```yaml
server:
  port: 8082
```

application-pro.yml

```yaml
server:
  port: 8081
```

application.yml

```yaml
spring:
  profiles:
    active: dev
```

2.注入.enable(false)

```java
        //设置要显示的Swagger环境
        Profiles profiles = Profiles.of("dev");
        //获取项目环境,通过environment.acceptsProfiles()判断是否在生产环境中
        boolean flag = environment.acceptsProfiles(profiles);
    

		.enable(flag)

```

运行

注：此时为dev下的端口号8082

![image-20230224011551548](SpringBoot-images/image-20230224011551548.png)

若更改端口号为8081

![image-20230224011620571](SpringBoot-images/image-20230224011620571.png)

## 6.Api分组和接口注释

### 6.1Api分组

```java
.groupName("张")
```

![image-20230224012118896](SpringBoot-images/image-20230224012118896.png)

#### 6.1.1 如何配置多个分组

```java
@Bean
    public Docket docket1(){
        return new Docket(DocumentationType.SWAGGER_2).groupName("a");
    }
    @Bean
    public Docket docket2(){
        return new Docket(DocumentationType.SWAGGER_2).groupName("b");
    }
    @Bean
    public Docket docket3(){
        return new Docket(DocumentationType.SWAGGER_2).groupName("c");
    }
```

运行

![image-20230224013325389](SpringBoot-images/image-20230224013325389.png)

### 6.2实体类配置

pojo--->User.java

```java
public class User {
    public String username;
    public String password;
}
```

HelloController

```java
//只要接口中，返回值存在实体类，就会被Swagger扫描到Swagger中
@PostMapping("/user")
public User user(){
    return new User();
}
```

运行

![image-20230224014200047](SpringBoot-images/image-20230224014200047.png)

### 6.3接口注释

### 6.3.1 @ApiModel注释

```java
@ApiModel("实体类")
public class User {
    @ApiModelProperty("用户名")
    public String username;
    @ApiModelProperty("密码")
    public String password;
}
```

运行

![image-20230224014452548](SpringBoot-images/image-20230224014452548.png)

### 6.3.2 @ApiOperation注释【 放在方法上】

```java
   //Operation接口  放在方法上
    @ApiOperation("Hello控制类")
    @GetMapping("/hello2")
    public String hello2(@ApiParam("用户名") String username){
        return "hello"+username;
    }
```



运行

![image-20230224015111679](SpringBoot-images/image-20230224015111679.png)

## 7.小结

- 我们可以通过Swagger给一些比较难以理解的属性或者接口，增加注释信息
- 接口文档实时更新
- 可以在线测试
- 是一个非常优秀的工具，几乎所有大公司都使用
- 注意点：在正式发布的时候，关闭swagger.出于安全考虑，节省内存。