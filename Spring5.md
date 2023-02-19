# Spring5

Spring参考笔记

https://blog.csdn.net/qq_48575500/article/details/123370114

https://blog.csdn.net/qq_41286666/article/details/123786690

Typora 常用快捷键大全

https://blog.csdn.net/D_huili/article/details/125301376

## 1.1 简介

**spring理念：**为了解决软件开发的复杂性，使现有的技术更加容易使用，本身是一个大杂烩。

SSH：Struct2 + Spring + Hibernate

**SSM: SpringMVC + Spring + Mybatis**

SSH：Struct2+Spring+Hibernate

SSM：SpringMVC+Spring+Mybatis

- 官网：https://spring.io/projects/spring-framework#overview

- 官方下载地址：https://repo.spring.io/release/org/springframework/spring/

- GitHub：https://github.com/spring-projects/spring-framework

  Maven项目需要导入的依赖：

  - spring-webmvc

    ```java
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>6.0.4</version>
    </dependency>
    
    ```

  - spring-jdbc

```java
<!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>6.0.4</version>
</dependency>

```

## 1.2 优点

- Spring是一个开源的免费的框架（容器）！

- Spring是一个轻量级的、非入侵式的框架！（非入侵：可以随意在任何项目里面导入）

- **控制反转（IOC），面向切面编程（AOP）！ （面试）**

- 支持事务的处理，对框架整合的支持！

  **总结一句话：Spring就是一个轻量级的控制反转（IOC）和面向切面编程（AOP）的框架！**

## 1.3 组成

![image-20230204232504282](C:\Users\zhang\Desktop\notebook\Spring-images\image-20230204232504282.png)

1. **Spring Core**

   Core封装包是框架的最基础部分，提供IOC和依赖注入特性。这里的基础概念是BeanFactory，它提供对Factory模式的经典实现来消除对程序性单例模式的需要，并真正地允许你从程序逻辑中分离出依赖关系和配置。

2. **Spring Context**

   构建于Core封装包基础上的Context封装包，提供了一种框架式的对象访问方法，有些象JNDI注册器。Context封装包的特性得自于Beans封装包，并添加了对国际化（I18N）的支持（例如资源绑定），事件传播，资源装载的方式和Context的透明创建，比如说通过Servlet 容器。

3. **Spring Dao**

   DAO (Data Access Object)提供了JDBC的抽象层，它可消除冗长的JDBC编码和解析数据库厂商特有的错误代码。并且，JDBC封装包还提供了一种比编程性更好的声明性事务管理方法，不仅仅是实现了特定接口，而且对所有的POJOs（plain old Java objects）都适用。

4. **Spring ORM**

   ORM 封装包提供了常用的“对象/关系”映射APIs的集成层。其中包括JPA、JDO、hibernate和iBatis 。利用ORM封装包，可以混合使用所有spring提供的特性进行“对象/关系”映射，如前边提到的简单声明性事务管理。

5. **Spring AOP**

   Spring的AOP 封装包提供了符合AOP Alliance规范的面向方面的编程实现，让你可以定义，例如方法拦截器（method-interceptors）和切点（pointcuts），从逻辑上讲，从而减弱代码的功能耦合，清晰的被分离开。而且，利用source-level的元数据功能，还可以将各种行为信息合并到你的代码中。

6. **Spring Web**

   Spring中的Web 包提供了基础的针对Web开发的集成特性，例如多方文件上传，利用Servlet listeners进行IOC容器初始化和针对Web的ApplicationContext。当与WebWork或Struts一起使用Spring时，这个包使Spring可与其他框架结合。

7. **Spring Web MVC**

   Spring中的MVC封装包提供了Web应用的Model-View-Controller（MVC）实现。Spring 的MVC框架并不是仅仅提供一种传统的实现，它提供了一种清晰的分离模型，在领域模型代码和Web Form之间。并且，还可以借助Spring框架的其他特性。

8. **Spring 三大核心思想**

   **DI(依赖注入),IOC(控制反转),AOP(面向切面编程)**

## 1.4 拓展

![image-20230204233229808](C:\Users\zhang\Desktop\notebook\Spring-images\image-20230204233229808.png)

- **SpringBoot：**

一个快速开发的脚手架
**约定大于配置**
基于SpringBoot可以快速开发单个微服务

- **SpringCloud：**

SpringCloud是**基于SpringBoot实现的**
但是要学好SpringBoot，**Spring和SpringMVC是前提！SpringBoot承上启下！**

**弊端：发展太久，违背原来的理念，配置十分繁琐！**

## 2. IOC理论推导

控制反转（IOC），它其实是一种设计思想；而实现这种思想的方式有很多！

### 2.1、原来的方式

- Dao层接口(UserDao)

  ```jav
  package com.zhang.dao;
  
  public interface UserDao {
      void getUser();
  }
  ```

- Dao层接口实现类(UserDaoImpl)

  ```java
  package com.zhang.dao;
  
  //重写接口中的方法！
  /*
   * 重写：方法名、参数类型、参数个数之类的都要相同
   * 重载：只要求方法名相同，参数类型和参数个数等可以不同
   * */
  public class UserDaoImpl implements UserDao{
      @Override
      public void getUser() {
          System.out.println("默认获取用户的数据！");
      }
  }
  ```

- Service层（业务层）接口(UserService)

  ```java
  package com.zhang.Service;
  
  public interface UserService {
      void getUser();
  }
  ```

- Service层（业务层）接口实现类(UserServiceImpl)

  ```java
  package com.zhang.Service;
  
  import com.zhang.dao.UserDao;
  import com.zhang.dao.UserDaoImpl;
  
  public class UserServiceImpl implements UserService{
      private UserDao userDao= new UserDaoImpl();
  
      @Override
      public void getUser() {
          userDao.getUser();
      }
  }
  ```

- 测试(MyTest)

  ```java
  import com.zhang.Service.UserService;
  import com.zhang.Service.UserServiceImpl;
  import com.zhang.dao.UserDaoImpl;
  
  public class MyTest {
      public static void main(String[] args) {
          UserService userService = new UserServiceImpl();
          userService.getUser();
      }
  }
  ```

### 2.2、改变

```java
public class UserServiceImpl implements UserService{
    private UserDao userDao;
    //利用set方法进行动态的实现值的注入！
    public void setUserDao(UserDao userDao){
        this.userDao = userDao;
    }
    @Override
    public void getUser() {
        userDao.getUser();
    }
}
```

**总结：如果按照原来的模式，用户需求一旦发生改变，程序员就需要在业务层实现类里面新创建实例对象；如果代码量大会很麻烦，成本昂贵！**

- 原来，程序是业务层主动创建对象，控制权在程序猿手上
- 使用**set注入**后，业务层程序不在具有主动性，而是变成了**被动的接收对象**，直接给业务层传递一个对象即可，自己不需要new
- 这种思想，从本质上解决了问题；程序猿**不再去管理对象的创建了**
- 系统的**耦合性（模块与模块间的依赖程序）大大降低**

## 3.IOC本质

![image-20230205004632234](Spring-images/image-20230205004632234.png)

**IOC本质：**

**控制反转IoC（Inversion of Control）**，是一种**设计思想**，**DI（依赖注入）**是实现**IoC**的一种方法，也有人认为**DI**只是**IoC**的另一种说法。没有IoC的程序中，我们使用面向对象编程，对象的创建与对象间的依赖关系完全硬编码在程序中，对象的创建由程序自己控制，控制反转后将对象的创建转移给第三方，个人认为所谓控制反转就是：**获得依赖对象的方式反转了。**

采用XML方式配置Bean的时候，Bean的定义信息是和实现分离的，而采用注解的方式可以把两者合为一体，Bean的定义信息直接以注解的形式定义在实现类中，从而达到了零配置的目的。

控制反转是一种通过描述（**XML或注解**）并通过第三方去生产或获取特定对象的方式。在**Spring中实现控制反转的是IoC容器，其实现方法是依赖注入（Dependency Injection，DI）。**


## 4.HelloSpring

在这里可以找到SpringFramework的版本以及对应的文档(英文)

https://docs.spring.io/spring-framework/docs/

1. 创建新的Maven模块，编写实体类(Hello)

   ```java
   package com.zhang.pojo;
   
   public class Hello {
       private String str;
   
       public String getStr() {
           return str;
       }
   
       public void setStr(String str) {
           this.str = str;
       }
   
       @Override
       public String toString() {
           return "Hello{" +
                   "str='" + str + '\'' +
                   '}';
       }
   
   }
   ```

2. 编写bean.xml配置文件

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
     https://www.springframework.org/schema/beans/spring-beans.xsd">
       <!--使用Spring来创建对象，在Spring这些都称为Bean
       类型 变量名 = new 类型();
       Hello hello = new Hello();
   
       id = 变量名
       class = new的对象
       property 相当于给对象中的属性设置一个值！
           -->
       <bean id="hello" class="com.zhang.pojo.Hello">
           <property name="str" value="Spring"/>
       </bean>
   </beans>
   ```

3. 测试

   ```java
   import com.zhang.pojo.Hello;
   import org.springframework.context.ApplicationContext;
   import org.springframework.context.support.ClassPathXmlApplicationContext;
   
   public class MyTest {
       public static void main(String[] args) {
           //获取Spring的上下文对象
           ApplicationContext context = new ClassPathXmlApplicationContext("bean.xml");
   
           //我们的对象现在都在Spring中的管理了，我们需要使用，直接去里面取出来就可以！
           Hello hello = (Hello) context.getBean("hello");
           System.out.println(hello.toString());
       }
   }
   ```

   **思考：**

   1. Hello对象是谁创建的？

       Hello对象是由**Spring创建**的。

   2. Hello对象的属性是怎么设置的？

       Hello对象的属性是由**Spring容器**设置的。

   **控制**： 谁来控制对象的创建，传统应用程序的对象是由程序本身控制创建的，**使用Spring后，对象是由Spring来创建的。**

   **反转**： 程序本身不创建对象，而变成**被动的接收对象。**

   **依赖注入**： 就是利用**set方法**来进行**注入**的。

   **IOC**是一种编程思想，由主动的编程变成被动的接收。

   到了现在，我们彻底不用在程序中去改动了，要实现不同的操作，只需要在xml配置文件中进行修改，所谓的IOC，一句话搞定：**对象由Spring来创建，管理，装配！**

   例子（2.1、2.2）：

   bean.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
     https://www.springframework.org/schema/beans/spring-beans.xsd">
       <!--使用Spring来创建对象，在Spring这些都称为Bean
       类型 变量名 = new 类型();
       Hello hello = new Hello();
   
       id = 变量名
       class = new的对象
       property 相当于给对象中的属性设置一个值！
           -->
       <bean id="oracleImpl" class="com.zhang.dao.UserDaoOracleImpl" />
       <bean id="mysqlImpl" class="com.zhang.dao.UserDaoMysqlImpl" />
   
       <bean id="UserServiceImpl" class="com.zhang.Service.UserServiceImpl">
       <!--
              ref: 引用Spring容器中创建好的对象
              value：具体的值（基本数据类型）
              -->
           <property name="userDao" ref="oracleImpl"></property>
       </bean>
   </beans>
   
   ```

   MyTest.java

   ```java
   import com.zhang.Service.UserService;
   import com.zhang.Service.UserServiceImpl;
   import com.zhang.dao.UserDao;
   import com.zhang.dao.UserDaoImpl;
   import com.zhang.dao.UserDaoMysqlImpl;
   import com.zhang.dao.UserDaoOracleImpl;
   import org.springframework.context.ApplicationContext;
   import org.springframework.context.support.ClassPathXmlApplicationContext;
   
   public class MyTest {
       public static void main(String[] args) {
           //拿到Spring容器
           ApplicationContext applicationContext = new ClassPathXmlApplicationContext("bean.xml");
   
           //需要什么，就get什么
           UserServiceImpl userServiceImpl = (UserServiceImpl) applicationContext.getBean("UserServiceImpl");
           userServiceImpl.getUser();
       }
   }
   
   ```

   **此时，我们只需要在bean.xml中修改即可**。**彻底不用在程序中去改动了**

## 5. IOC创建对象的方式

1. 使用**无参构造**创建对象(默认)

   ```xml
   <bean id="user" class="com.zhang.pojo.User">
           <property name="name" value="阿花"/>
       </bean>
   ```

2. 假设要使用**有参构造**创建对象。

   - 通过下标的方式【index】

     ```xml
      <bean id="user" class="com.zhang.pojo.User">
             <constructor-arg index="0" value="阿花" />
         </bean>
     ```

   - 通过参数类型【type】（**不建议使用**）

     ```xml
     <bean id="user" class="com.zhang.pojo.User">
             <constructor-arg type="java.lang.String" value="阿花2号"/>
         </bean>
     ```

   - 通过参数名【name】（**常用**）

     ```xml
     <bean id="user" class="com.zhang.pojo.User">
         <constructor-arg name="name" value="阿花三号" />
     </bean>
     ```

**总结：在配置文件被加载的时候，Spring容器中的对象就已经被初始化了**

**注：Spring创建对象是单例**

## 6. Spring配置

### 6.1 取别名(alias)

作用就是给一个bean（类对象）起别名：这样的话我们测试执行时，user和userNew都可以访问创建的类对象

```xm
<bean id="user" class="com.zhang.pojo.User">
        <property name="name" value="阿花"/>
    </bean>
    <alias name="user" alias="userHua"/>
```

### 6.2 Bean的配置

- id：bean的唯一标识符，也就是相当于创建的对象名

- class：bean对象所对应的全限定名（包名+类名）

- name：也可以用来给该bean对象起别名，更高级（可以取多个别名，然后用逗号、空格、分号等分隔开）

- property子标签：给对象中的属性设置一个值

  ```xml
  <bean id="user" class="com.zhang.pojo.User" name="ahua, xiaomei">
          <property name="name" value="阿花"/>
      </bean>
  ```

### 6.3 import

一般用于团队开发使用，它可以将**多个配置文件导入合并为一个总的**，等到需要加载配置文件的时候只需要加载这一个总的就OK了

**applicationContext.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
  https://www.springframework.org/schema/beans/spring-beans.xsd">
    <import resource="beans.xml" />
</beans>
```

## 7. 依赖注入(DI)

### 7.1 构造器注入

前面已经介绍过，参考5、IOC创建对象的方式

### 7.2 Set方式注入【重点】

依赖注入：**Set注入**

- 依赖：bean对象的创建**依赖spring容器**
- 注入：bean对象的所有属性由**容器注入**

【环境搭建】

1. Address.java

   ```java
   public class Address {
       private String address;
   
       public String getAddress() {
           return address;
       }
   
       public void setAddress(String address) {
           this.address = address;
       }
   }
   ```

   

2. Student.java

   ```java
   public class Student {
       private String name;
       private Address address;
       private String[] books;
       private List<String> hobbys;
       private Map<String,String> card;
       private Set<String> games;
       private String wife;
       private Properties info;
   
       public String getName() {
           return name;
       }
   
       public void setName(String name) {
           this.name = name;
       }
   
       public Address getAddress() {
           return address;
       }
   
       public void setAddress(Address address) {
           this.address = address;
       }
   
       public String[] getBooks() {
           return books;
       }
   
       public void setBooks(String[] books) {
           this.books = books;
       }
   
       public List<String> getHobbys() {
           return hobbys;
       }
   
       public void setHobbys(List<String> hobbys) {
           this.hobbys = hobbys;
       }
   
       public Map<String, String> getCard() {
           return card;
       }
   
       public void setCard(Map<String, String> card) {
           this.card = card;
       }
   
       public Set<String> getGames() {
           return games;
       }
   
       public void setGames(Set<String> games) {
           this.games = games;
       }
   
       public String getWife() {
           return wife;
       }
   
       public void setWife(String wife) {
           this.wife = wife;
       }
   
       public Properties getInfo() {
           return info;
       }
   
       public void setInfo(Properties info) {
           this.info = info;
       }
   
       @Override
       public String toString() {
           return "Student{" +
                   "name='" + name + '\'' +
                   ", address=" + address +
                   ", books=" + Arrays.toString(books) +
                   ", hobbys=" + hobbys +
                   ", card=" + card +
                   ", games=" + games +
                   ", wife='" + wife + '\'' +
                   ", info=" + info +
                   '}';
       }
   }
   ```

   

3. beans.xml

   ```xml
   <bean id="student" class="com.zhang.pojo.Student">
           <property name="name" value="阿花" />
       </bean>
   ```

   

4. 测试MyTest.java

   ```jav
   public class MyTest {
       public static void main(String[] args) {
           ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
           Student student = (Student) context.getBean("student");
           System.out.println(student.getName());
           System.out.println(student.getAddress());
   
       }
   }
   ```

完善注入信息

```xml
<bean id="address" class="com.zhang.pojo.Address" >
        <property name="address" value="河南省"/>
    </bean>
    <bean id="student" class="com.zhang.pojo.Student">
        <!--    普通值注入    -->
        <property name="name" value="阿花" />
        <!--    Bean注入    -->
        <property name="address" ref="address"/>

        <!--    数组注入    -->
        <property name="books">
            <array>
                <value>红楼梦</value>
                <value>西游记</value>
                <value>三国演义</value>
                <value>水浒传</value>
            </array>
        </property>
        <!-- List注入      -->
        <property name="hobbys">
            <list>
                <value>代码</value>
                <value>篮球</value>
                <value>乒乓球</value>
                <value>看电影</value>
            </list>
        </property>
        <!-- Map注入      -->
        <property name="card">
            <map>
                <entry key="身份证" value="1111000384" />
                <entry key="银行卡" value="222222222222" />
            </map>
        </property>
        <!-- Set注入      -->
        <property name="games">
            <set>
                <value>LOL1</value>
                <value>LOL2</value>
                <value>LOL3</value>
            </set>
        </property>
        <!-- Null注入      -->
        <property name="wife">
            <null></null>
        </property>

        <!-- Properties      -->
        <property name="info">
            <props>
                <prop key="学号">110101</prop>
                <prop key="性别">男</prop>
                <prop key="username">阿花</prop>
                <prop key="password">11119999</prop>
            </props>
        </property>

    </bean>
```

### 7.3 拓展方式注入[p命名空间和c命名空间]

注意：在使用两个命名空间时，前提需要在头文件里面添加约束！

```xml
xmlns:p="http://www.springframework.org/schema/p"
xmlns:c="http://www.springframework.org/schema/c"
```

User.java

```java
public class User {
    private String name;
    private int age;
//    c命名空间需要有参构造
    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public User() {

    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

userbeans.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
  https://www.springframework.org/schema/beans/spring-beans.xsd">
    <!-- p命名空间注入(无参构造)  可以直接注入属性 property   -->
    <bean id="user" class="com.zhang.pojo.User" p:name="阿花" p:age="18"></bean>

    <!-- c命名空间注入(有参构造器)  可以直接注入属性 property   -->
    <bean id="user2" class="com.zhang.pojo.User" c:name="小强" c:age="19" ></bean>
</beans>
```

MyTest.java

```java
@Test
    public void testP(){
        ApplicationContext context = new ClassPathXmlApplicationContext("userbeans.xml");
        User user =  context.getBean("user2",User.class);
        System.out.println(user.toString());
    }
```

### 7.4 Bean作用域

|  singleton  | (Default) Scopes a single bean definition to a single object instance for each Spring IoC container. |
| :---------: | ------------------------------------------------------------ |
|  prototype  | Scopes a single bean definition to any number of object instances. |
|   request   | Scopes a single bean definition to the lifecycle of a single HTTP request. That is, each HTTP request has its own instance of a bean created off the back of a single bean definition. Only valid in the context of a web-aware Spring ApplicationContext. |
|   session   | Scopes a single bean definition to the lifecycle of an HTTP Session. Only valid in the context of a web-aware Spring ApplicationContext. |
| application | Scopes a single bean definition to the lifecycle of a ServletContext. Only valid in the context of a web-aware Spring ApplicationContext. |
|  websocket  | Scopes a single bean definition to the lifecycle of a WebSocket. Only valid in the context of a web-aware Spring ApplicationContext. |

1. **单例模式**（Spring默认机制）

The Singleton Scope[singleton单例模式：（Spring默认的）]

![image-20230207144357420](Spring-images/image-20230207144357420.png)

```xml
<bean id="user2" class="com.zhang.pojo.User" c:name="小强" c:age="19" scope="singleton" ></bean>
```

2. **原型模式**：每次从容器中get的时候，都会产生一个新的对象。

   ```xml
   <bean id="user2" class="com.zhang.pojo.User" c:name="小强" c:age="19" scope="prototype" ></bean>
   ```

   ![image-20230207145035921](Spring-images/image-20230207145035921.png)

3. 其余的request、session、application等只能在web开发中使用到

## 8. Bean的自动装配

- 自动装配是Spring满足**Bean依赖**的一种方式。
- Spring会在**上下文中自动寻找**，并自动给bean装配属性。

1. 在**xml**中**显式**的配置。
2. 在**java**中**显示**配置。
3. **隐式的自动装配bean【重要】**。

### 8.1 测试

测试实体类：People,Cat,Dog

beans.xml

```xml
<bean id="cat" class="com.zhang.pojo.Cat"></bean>

    <bean id="dog" class="com.zhang.pojo.Dog"></bean>

    <bean id="people" class="com.zhang.pojo.People">
        <property name="name" value="阿花"></property>
        <property name="cat" ref="cat"></property>
        <property name="dog" ref="dog"></property>
    </bean>
```

测试

```java
@Test
    public void test1(){
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        People people = context.getBean("people", People.class);
        people.getCat().shout();
        people.getDog().shout();
    }
```

### 8.2 ByName自动装配

**byName:会自动在容器上下文中查找，和自己对象set方法后面的值对应的beanid。**

**弊端：bean标签里面的id只能取只能取属性名Xx（setXx），其他的不能识别；也就是说一个实体类属性只能对应一个setXx方法，那么也就一个bean**

beans.xml

```xml
<bean id="cat" class="com.zhang.pojo.Cat"></bean>

    <bean id="dog" class="com.zhang.pojo.Dog"></bean>

    <bean id="people" class="com.zhang.pojo.People" autowire="byName">
        <property name="name" value="阿花"></property>
    </bean>
```



### 8.3 ByType自动装配

**byType:会自动在容器上下文中查找，和自己对象属性类型相同的bean，需要保证属性类型全局唯一 。**

**弊端：通过实体类中的每个属性的类型来在容器中进行上下文的查找；也就是说一个属性类型只能对应一个bean（而且id可省略–根据属性的类型进行查找，不是根据id）**

beans.xml

```xml
<bean id="cat" class="com.zhang.pojo.Cat"></bean>
    <bean id="dog" class="com.zhang.pojo.Dog"></bean>

    <bean id="people" class="com.zhang.pojo.People" autowire="byType">
        <property name="name" value="阿花"></property>
    </bean>
或
<bean  class="com.zhang.pojo.Cat"></bean>
    <bean class="com.zhang.pojo.Dog"></bean>
    <bean id="people" class="com.zhang.pojo.People" autowire="byType">
        <property name="name" value="阿花"></property>
    </bean>
```

**总结：**

- byName自动装配：保证所有的bean的id唯一，id与setXx中的Xx一致
- byType自动装配：保证所有的class唯一，class与属性类型一致

### 8.4 使用注解实现自动装配

jdk1.5支持的注解，Spring2.5就支持注解了

使用注解的**前提**：

- **导入约束** context约束。

- **开启支持**  <context:annotation-config/>

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    https://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context
    https://www.springframework.org/schema/context/spring-context.xsd">
      
    <context:annotation-config/>
  </beans>
  ```

- **配置注解**

1. **@Autowired**【默认通过byType方式，当匹配到多个同类型时，再通过byName方式】

使用Autowired，可以不用再编写set方法，前提是自动装配的属性在IOC容器中存在，且符合名字bytype。

如果@Autowired自动装配的环境比较复杂，自动装配无法通过@Autowired完成时，可以使用@Qualifier（value=”***“）去配置@Autowired的使用，指定一个唯一的bean对象注入。

```java
@Autowired
    @Qualifier(value = "cat")
    private Cat cat;
```

使用规则：

- 直接在属性上使用，或者在对应属性的setXx方法

- 而且如果使用该注解，那么实体类中不要写对应的set方法（前提是：开启了**注解支持**）

- @Autowired：可以给该注解赋值一个参数

  @Autowired(required = false) *赋值为false，那么这个属性可以为空值*

- 注意：视频提到bean里面的id符合byName的命名规则，但是测试时，不符合也能成功，需要进一步的验证！

  - 验证后
  - 该注解先通过id进行自动匹配
  - 匹配不到通过class进行自动匹配

2. **@Nullable** 字段标记了这个注解，表明该字段可以为null

3. ##### @Resource注解：（使用方式和@Autowired注解类似）

   ```java
   @Resource(name = "dog123")
   private Dog dog;
   @Resource(name = "cat123")
   private Cat cat;
   ```

   **总结**
   **都是用来自动装配的，都可以放在属性字段上**
   **@Autowired通过先通过byType的方式实现，而且必须要求这个对象存在！【常用】**
   **@Resource默认通过byName的方式实现，如果找不到名字，则通过byType实现！如果两个都找不到的情况下，就报错！【常用】**
   **执行顺序不同：@Autowired默认先通过byType的方式实现，@Resource默认先通过byName方式实现**

## 9. 使用注解开发

### 9.1、环境搭建

在Spring4之后，使用注解开发都要导入aop的jar包

![image-20230207221901886](Spring-images/image-20230207221901886.png)

- 使用注解需要导入约束，开启注解支持

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
          https://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/context
          https://www.springframework.org/schema/context/spring-context.xsd">
      <!--指定要扫描的包，这个包下的注解就会生效-->
      <context:component-scan base-package="com.zhang.pojo"/>
      <!--开启注解支持！-->
      <context:annotation-config/>
  </beans>
  ```

  ### 9.2、bean对象如何注解

  @Component， 放在实体类的类名前面

  等价于<bean id="user" class="com.zhang.pojo.User"></bean>

  ```java
  //@Component组件
  //等价于<bean id="user" class="com.zhang.pojo.User"></bean>
  @Component
  public class User {
      public String name="阿花";
  }
  ```

  ### 9.3、属性如何注解

  @Value注解用于给实体类的属性赋值, 放在属性上或者属性对应的setXx方法上都可以

  ```xml
  Value()  相当于 <property name="name" value="阿花"/>
  ```

```java
    //Value()  相当于 <property name="name" value="阿花"/>
	//    @Value("阿花")
    public String name;
    @Value("阿花")
    public void setName(String name) {
        this.name = name;
    }
}
```

### 9.4、衍生的注解

@Component注解有几个衍生注解，我们在web开发中，会按照mvc架构进行分层！

```jav
dao层：@Repository 

service层：@Service

controller层：@Controller
```

这四个注解的**功能都是一样的**，**都代表将某个类注册到Spring中，来装配bean**

扫描com.zhang下所有的包

```xml
<!--指定要扫描的包，这个包下的注解就会生效-->
    <context:component-scan base-package="com.zhang"/>
```

### 9.5、自动装配如何注解

- @Autowired
- @Nullable
- @Qualifier
- @Resource

### 9.6、作用域

**@Scope**注解：用来设置实体类的**单例模式、原型模式**等

```java
@Component
@Scope("singleton")
public class User {
    //Value()  相当于 <property name="name" value="阿花"/>
//    @Value("阿花")
    public String name;
    @Value("阿花")
    public void setName(String name) {
        this.name = name;
    }
}
```

### 9.7、小结

xml配置文件与注解：

- xml更加万能，适用于任何场合，便于维护
- 注解维护复杂

xml与注解最佳搭配：

- xml用来管理bean
- 注解用来完成属性的注入

使用注意：

- 在使用注解的时候一定不要忘记，开启注解支持，和扫描使用注解的包

  ```xml
  <!--指定要扫描的包，这个包下的注解就会生效-->
  <context:component-scan base-package="com.zhang"/>
  <!--开启注解支持！-->
  <context:annotation-config/>
  ```

  

## 10. 用JAVA的方式配置Spring(JavaConfig)

现在不使用Spring配置文件（applicationContext.xml），而是全部交给java来进行配置。

**JavaConfig**是Spring的一个子项目，在Spring4之后，它成为了一个核心功能

实体类：

```java
@Component
public class User {
    @Value("阿花")
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                '}';
    }
}
```

配置类：

```java
//@Configuration，类中出现这个表示该类是一个配置类，就相当于beans.xml配置文件
@Configuration
//扫描同一包下的bean
@ComponentScan("com.zhang.pojo")
//合并配置类 相当于合并多个xml配置文件
@Import(ZhangConfig2.class)
public class ZhangConfig {
    //注册一个bean对象
    //方法名(getUser)：代表bean标签的id属性
    //方法返回类型(User)：代表bean的class属性
    //方法返回值(new User())：要注入到bean的对象
    @Bean
    public User getUser(){
        return new User();
    }
}
```

测试类

```java
public class MyTest {
    @Test
    public void test1(){
        //如果完全使用java来配置Spring,
        // 那么需要AnnotationConfigApplicationContext来获取Spring容器，
        // 通过加载配置类 对象的方式
        ApplicationContext context = new AnnotationConfigApplicationContext(ZhangConfig.class);
        //“getUser”是java配置类里面对应bean的方法名称
        User user = context.getBean("user",User.class);
        System.out.println(user.getName());
    }
}
```

## 11. 代理模式(23种设计模式之一)

**什么是代理模式？–因为这就是SpringAOP（面向切面编程）的底层【面试：SpringAOP和SpringMVC】**

**代理模式：**

- **静态代理**
- **动态代理**

### 11.1 静态代理

代理模式的**优点**：

- 操作更加纯粹，直接面向代理对象即可
- 可以在代理角色里添加新的业务
- 实现了业务的分工
- 公共业务发生扩展的时候，方便集中管理

代理模式**缺点**：

- 一个真实角色（客户）就需要一个代理对象，**代码量翻倍**，开发效率降低！

**角色分析**：

- 抽象角色：一般使用接口或者是抽象类来解决
- 真实角色：被代理的角色
- 代理角色：代理真实角色，代理真实角色后，我们一般会做些附属操作
- 客户：访问代理角色的人

![image-20230208011308427](Spring-images/image-20230208011308427.png)

Rent.java（接口）

```java
public interface Rent {
    public void rent();
}
```



Host.java

```java
//房东
public class Host  implements Rent{

    @Override
    public void rent() {
        System.out.println("房东要出租房子");
    }
}
```



Proxy.java

```java
//中介
public class Proxy implements Rent{
    private Host host;

    public Proxy() {
    }

    public Proxy(Host host) {
        this.host = host;
    }
    //看房子
    public void seeHouse(){
        System.out.println("中介带领看房子");
    }
    //租赁合同
    public void hetong(){
        System.out.println("签合同");
    }
    //中介费
    public void fare(){
        System.out.println("收中介费");
    }
    @Override
    public void rent() {
        seeHouse();
        host.rent();
        hetong();
        fare();
    }
}
```



Client.java

```java
public class Client {
    public static void main(String[] args) {
        //房东出租房子
        Host host = new Host();
        //代理帮中介出租，但 代理角色会有 附属操作
        Proxy proxy = new Proxy(host);
        //找中介租房
        proxy.rent();
        
    }

}
```

### 11.2 加深理解

- 接口(UserService.java)

  ```java
  public interface UserService {
      public void add();
      public void del();
      public void update();
      public void select();
  }
  ```

  

- 真实角色(UserServiceImpl.java)

  ```java
  //真实对象
  public class UserServiceImpl implements UserService{
  
      @Override
      public void add() {
          System.out.println("增加对象");
      }
  
      @Override
      public void del() {
          System.out.println("删除对象");
      }
  
      @Override
      public void update() {
          System.out.println("更改对象");
      }
  
      @Override
      public void select() {
          System.out.println("查询对象");
      }
  }
  ```

  

- 代理角色(UserServiceProxy.ava)

  ​	在继承UserService的基础上(不改变原有代码的基础上，增加了附加操作【log日志功能】)

  ​	此时，用户只需要通过代理就可实现操作

  ```java
  public class UserServiceProxy implements UserService{
      UserService userService;
  
      public void setUserService(UserServiceImpl userService){
          this.userService = userService;
      }
      @Override
      public void add() {
          log("add");
          System.out.println("add方法");
      }
  
      @Override
      public void del() {
          log("del");
          System.out.println("del方法");
      }
  
      @Override
      public void update() {
          log("update");
          System.out.println("update方法");
      }
  
      @Override
      public void select() {
          log("select");
          System.out.println("select方法");
      }
      public void log(String msg){
          System.out.println("使用了"+msg+"方法");
      }
  }
  ```

  

- 客户访问(Client.java)

  ```java
  public class Client {
      public static void main(String[] args) {
          UserServiceImpl userService = new UserServiceImpl();
          UserServiceProxy proxy = new UserServiceProxy();
          proxy.setUserService(userService);
          proxy.add();
      }
  }
  ```

  ![image-20230208025024383](Spring-images/image-20230208025024383.png)

### 11.3 动态代理

- 动态代理和静态代理角色一样。
- 动态代理类是**动态生成**的，不是直接写好的。
- 动态代理分类：**基于接口** 的动态代理、**基于类**的动态代理。
  **基于接口 ----- JDK动态代理。**
  **基于类 ------ cglib**
  **java字节码实现 ------ javasist**

**动态代理的好处：**

- 静态代理的**所有好处**。
- 一个动态代理类**代理**的是**一个接口**，一般就是一个对应的业务。
- 一个动态代理类可以**代理多个类**，只要是实现了同一个接口即可。

**了解两个类：**

- **Proxy**：代理
- **InvocationHandler**：调用处理程序

1. 接口

   ```java
   public interface Rent {
       public void rent();
   }
   ```

   

2. 真实角色

   ```JAVA
   //房东
   public class Host implements Rent {
   
       @Override
       public void rent() {
           System.out.println("房东要出租房子");
       }
   }
   ```

   

3. 动态代理类

   ```java
   //用这个类自动生成代理类
   public class ProxyInvocationHandler implements InvocationHandler {
   
       //被代理的接口
       private Rent rent;
       public void setRent(Rent rent){
           this.rent = rent;
       }
       //生成得到代理类
       public Object getProxy(){
           return Proxy.newProxyInstance(this.getClass().getClassLoader(), rent.getClass().getInterfaces(),this);
       }
   
       //处理代理实例，返回结果
       @Override
       public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
           //动态代理的本质，就是使用反射机制实现
           seeHouse();
           Object result = method.invoke(rent,args);
           return result;
       }
   
       public void seeHouse(){
           System.out.println("中介带看房子");
       }
   
   }
   ```

   

4. 客户端

   ```java
    public static void main(String[] args) {
           //真实角色
           Host host = new Host();
   
           //代理角色
           ProxyInvocationHandler handler = new ProxyInvocationHandler();
           //通过调用程序处理需要调用的接口对象
           handler.setRent(host);
           //proxy就是动态生成，我们并没有写它
           Rent proxy = (Rent) handler.getProxy();
   
           proxy.rent();
       }
   ```

   

**动态代理工具类模板：**

```jav
//用这个类自动生成代理类
public class ProxyInvocationHandler implements InvocationHandler {

    //被代理的接口
    private Object target;
    public void setTarget(Object target){
        this.target = target;
    }
    //生成得到代理类
    public Object getProxy(){
        return Proxy.newProxyInstance(this.getClass().getClassLoader(), target.getClass().getInterfaces(),this);
    }

    //处理代理实例，返回结果
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        log(method.getName());
        //动态代理的本质，就是使用反射机制实现
        Object result = method.invoke(target,args);
        return result;
    }

    public void log(String msg){
        System.out.println("执行了"+msg+"方法");
    }
}

```



**客户端：**

```jav
public static void main(String[] args) {
        //真实角色
        UserServiceImpl userService = new UserServiceImpl();
        //代理角色，不存在
        ProxyInvocationHandler phandler = new ProxyInvocationHandler();
        //设置要代理的对象
        phandler.setTarget(userService);
        //动态生成代理类
        UserService proxy = (UserService) phandler.getProxy();
        proxy.add();

    }
```



## 12. AOP(面向切面变编程）

### 12.1 什么是AOP

AOP（Aspect Oriented Programming）意为：

​	面向切面编程，通过**预编译方式**和**运行期动态代理**实现程序功能的统一维护的一种技术。

​	AOP是OOP的延续，是软件开发中的一个热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生范型。利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。

![image-20230208234530104](Spring-images/image-20230208234530104.png)

### 12.2 AOP在Spring中的作用

提供声明式事务；允许用户自定义切面

- ​	切面（ASPECT）：横切关注点被模块化的特殊对象。即，它是一个类。
- ​	通知（Advice）：切面必须要完成的工作。即，它是类中的一个方法。
- ​	目标（Target）：被通知对象。
- ​	代理（Proxy）：向目标对象应用通知之后创建的对象。
- ​	切入点（PointCut）：切面通知执行的“地点”的定义。
- ​	连接点（JointPoint）：与切入点匹配的执行点。

**横切关注点：** 跨越应用程序多个模块的方法或功能。即是，与我们业务逻辑无关的，但是我们需要关注的部分，就是横切关注点。如日志，安全，缓存，事务等等…
**切面（ASPECT）**：横切关注点被模块化的特殊对象。即，它是一个类。
**通知（Advice）**：切面必须要完成的工作。即，它是类中的一个方法。
**目标（Target）**：被通知对象。
**代理（Proxy）**：向目标对象应用通知之后创建的对象。
**切入点（PointCut）**：切面通知执行的“地点”的定义。
**连接点（JointPoint）**：与切入点匹配的执行点。

![image-20230208234820460](Spring-images/image-20230208234820460.png)

SpringAOP中，通过**Advice**定义横切逻辑，Spring中支持5种类型的Advice：就是SpringAOP在不改变原来代码的情况下，去增加新的业务功能。

![image-20230208234906790](Spring-images/image-20230208234906790.png)

### 12.3 使用Spring实现AOP

使用AOP前，需要导入依赖：

```xml
<!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.19</version>
    <scope>runtime</scope>
</dependency>
```



#### 方式一：使用原生的Spring API接口来实现【主要是SpringAPI接口实现】

定义接口和接口实现类

接口(UserService)

```java
public interface UserService {
    public void add();
    public void del();
    public void update();
    public void query();
}
```

实现类(UserServiceImpl)

```java
public class UserServiceImpl implements UserService{
    @Override
    public void add() {
        System.out.println("add了一个方法");
    }

    @Override
    public void del() {
        System.out.println("del了一个方法");
    }

    @Override
    public void update() {
        System.out.println("update了一个方法");
    }

    @Override
    public void query() {
        System.out.println("query了一个方法");
    }
}
```

构造两个新增的业务类（比如打印日志）

```java
Log
public class Log implements MethodBeforeAdvice {

    //method 要执行的目标对象的方法
    //objects 参数
    // target 目标对象
    @Override
    public void before(Method method, Object[] rags, Object target) throws Throwable {
        System.out.println(target.getClass().getName()+"的"+method.getName()+"被执行了");
    }
}

```

```java
AfterLog
public class AfterLog implements AfterReturningAdvice {

    //returnValue 返回值
    //method 要执行的目标对象的方法
    //objects 参数
    // target 目标对象
    @Override
    public void afterReturning(Object returnValue, Method method, Object[] args, Object target) throws Throwable {
        System.out.println("执行了"+method.getName()+"方法被执行，返回结果为"+returnValue);
    }
}
```

applicationContext.xml[注意  导入AOP约束]

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
        xsi:schemaLocation="http://www.springframework.org/schema/beans

        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">
    <!--指定要扫描的包，这个包下的注解就会生效-->
    <context:component-scan base-package="com.zhang"/>
    <!--开启注解支持！-->
    <context:annotation-config/>
    <!-- 注册 bean    -->
    <bean id="userService" class="com.zhang.service.UserServiceImpl"/>
    <bean id="log" class="com.zhang.log.Log"/>
    <bean id="afterLog" class="com.zhang.log.AfterLog"/>

    <!-- 配置AOP :需要导入AOP约束  -->
    <aop:config>
        <!--  切入点  expression表达式 execution(要执行的位置 修饰词 返回值 类名 方法名 参数)  -->
        <aop:pointcut id="pointcut" expression="execution(* com.zhang.service.UserServiceImpl.*(..))"/>
        <!-- 执行环绕增加       -->
        <aop:advisor advice-ref="log" pointcut-ref="pointcut"></aop:advisor>
        <aop:advisor advice-ref="afterLog" pointcut-ref="pointcut"></aop:advisor>
    </aop:config>
```

测试

```java
@Test
public void test1(){
    ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
    //！！！！！！！！！！！！！！！动态代理的是接口：！！！！！！！！！！！！！！！！！！！！
    //所以应该是UserService,而不是UserServiceImpl
    UserService userService = context.getBean("userService", UserService.class);
    userService.query();
}
```

#### 方式二：自定义来实现AOP【主要是切面定义】

**DiyPointCut**

```JAVA
public void before(){
        System.out.println("方法执行前");
    }
    public void after(){
        System.out.println("方法执行后");
    }
```

applicationContext.xml

```xml
<!--  方式二：自定义来实现AOP【主要是切面定义】  -->
        <bean id="diy" class="com.zhang.diy.DiyPointCut">
        </bean>

    <aop:config>
        <!--  切面     ref 引用的类   -->
        <aop:aspect ref="diy">
            <!-- 切入点           -->
            <aop:pointcut id="point" expression="execution(* com.zhang.service.UserServiceImpl.*(..))"/>
            <!-- 通知           -->
            <aop:before method="before" pointcut-ref="point"></aop:before>
            <aop:after method="after" pointcut-ref="point"></aop:after>
        </aop:aspect>
    </aop:config>
```



测试

```java
public void test1(){
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        //！！！！！！！！！！！！！！！动态代理的是接口：！！！！！！！！！！！！！！！！！！！！
        //所以应该是UserService,而不是UserServiceImpl
        UserService userService = context.getBean("userService", UserService.class);
        userService.query();
    }
```



#### 方式三：使用注解来实现

导入aspectjrt依赖

```xml
<!-- https://mvnrepository.com/artifact/aspectj/aspectjrt -->
        <dependency>
            <groupId>aspectj</groupId>
            <artifactId>aspectjrt</artifactId>
            <version>1.5.4</version>
        </dependency>
```

**AnnotationPointCut**

```java
//标注这个类是一个切面
@Aspect
public class AnnotationPointCut {
    @Before("execution(* com.zhang.service.UserServiceImpl.*(..))")
    public void before(){
        System.out.println("======方法执行前=====");
    }

    @After("execution(* com.zhang.service.UserServiceImpl.*(..))")
    public void after(){
        System.out.println("======方法执行后=====");
    }

    //在环绕增强中，可以给定一个参数，代表我们要获取处理切入的点
    @Around("execution(* com.zhang.service.UserServiceImpl.*(..))")
    public void around(ProceedingJoinPoint jp) throws Throwable {
        System.out.println("环绕前");
        //获得签名
        Signature signature = jp.getSignature();
        System.out.println("signature::::"+signature);
        System.out.println(jp.proceed());

        //执行方法
        Object proceed = jp.proceed(); //执行方法
        System.out.println("环绕后");

    }
```

applicationContext.xml

```xml
<!--  方式三：使用注解来实现  -->
    <bean id="annotationPointCut" class="com.zhang.diy.AnnotationPointCut"></bean>
    <!--  开启注解支持  默认JDK（proxy-target-class="false"）   cglib（proxy-target-class="true"）     -->
    <aop:aspectj-autoproxy />
```

## 13. 整合Mybatis

13.1 回忆Mybatis

步骤：

1. 导入相关jar包
   junit、mybatis、mysql数据库、spring相关的、aop植入、mybatis-spring

   

   ```xml
   <dependencies>
               <dependency>
                   <groupId>junit</groupId>
                   <artifactId>junit</artifactId>
                   <version>4.12</version>
               </dependency>
               <dependency>
                   <groupId>org.mybatis</groupId>
                   <artifactId>mybatis</artifactId>
                   <version>3.5.6</version>
               </dependency>
               <dependency>
                   <groupId>mysql</groupId>
                   <artifactId>mysql-connector-java</artifactId>
                   <version>5.1.47</version>
               </dependency>
               <dependency>
                   <groupId>org.springframework</groupId>
                   <artifactId>spring-webmvc</artifactId>
                   <version>5.2.0.RELEASE</version>
               </dependency>
               <!--Spring操作数据库的话，还需要一个spring-jdbc
                            -->
               <!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
               <dependency>
                   <groupId>org.springframework</groupId>
                   <artifactId>spring-jdbc</artifactId>
                   <version>5.2.0.RELEASE</version>
               </dependency>
               <dependency>
                   <groupId>org.aspectj</groupId>
                   <artifactId>aspectjweaver</artifactId>
                   <version>1.8.13</version>
               </dependency>
               <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
               <dependency>
                   <groupId>org.mybatis</groupId>
                   <artifactId>mybatis-spring</artifactId>
                   <version>2.0.2</version>
               </dependency>
               <dependency>
                   <groupId>org.projectlombok</groupId>
                   <artifactId>lombok</artifactId>
                   <version>1.18.10</version>
               </dependency>
       </dependencies>
   
   <resources>
               <resource>
                   <directory>src/main/resources</directory>
                   <includes>
                       <include>**/*.properties</include>
                       <include>**/*.xml</include>
                   </includes>
                   <filtering>false</filtering>
               </resource>
               <resource>
                   <directory>src/main/java</directory>
                   <includes>
                       <include>**/*.properties</include>
                       <include>**/*.xml</include>
                   </includes>
                   <filtering>false</filtering>
               </resource>
           </resources>
   ```

2. 编写配置文件

   ```java
   public interface UserMapper {
       public List<User> selectUser();
   }
   ```

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
           <!DOCTYPE mapper
                   PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
                   "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="com.zhang.mapper.UserMapper">
       <select id="selectUser" resultType="user">
           select * from user
       </select>
   </mapper>
   ```

   

3. 测试

   ```java
   public static void main(String[] args) throws IOException {
           String resources = "mybatis-config.xml";
           InputStream in = Resources.getResourceAsStream(resources);
           SqlSessionFactory build = new SqlSessionFactoryBuilder().build(in);
           SqlSession sqlSession = build.openSession();
   
           UserMapper mapper = sqlSession.getMapper(UserMapper.class);
           List<User> users = mapper.selectUser();
           for (User user : users) {
               System.out.println(user);
           }
       }
   ```

   

### 13.2 Mybatis-Spring

MyBatis-Spring 会帮助你将 MyBatis 代码无缝地整合到 Spring 中。

文档链接：http://mybatis.org/spring/zh/index.html

如果使用 Maven 作为构建工具，仅需要在 pom.xml 中加入以下代码即可：

```xml
        <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>2.0.2</version>
        </dependency>

```

**整合实现方式一：**

1. 引入Spring配置文件spring-dao.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xmlns:aop="http://www.springframework.org/schema/aop"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
   
           https://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/context
           https://www.springframework.org/schema/context/spring-context.xsd
           http://www.springframework.org/schema/aop
           https://www.springframework.org/schema/aop/spring-aop.xsd">
       <!--指定要扫描的包，这个包下的注解就会生效-->
       <context:component-scan base-package="com.zhang"/>
       <!--开启注解支持！-->
       <context:annotation-config/>
   
       <import resource="applicationContext.xml"/>
       <!--    -->
       <bean id="userMapper" class="com.zhang.mapper.UserMapperImpl">
           <property name="sqlSession" ref="sqlSession"></property>
       </bean>
   </beans>
   ```

   applicationContext.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xmlns:aop="http://www.springframework.org/schema/aop"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
   
           https://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/context
           https://www.springframework.org/schema/context/spring-context.xsd
           http://www.springframework.org/schema/aop
           https://www.springframework.org/schema/aop/spring-aop.xsd">
       <!-- DataSource:使用Spring数据源替换Mybatis配置   -->
       <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
           <property name="driverClassName" value="com.mysql.jdbc.Driver"></property>
           <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=false&amp;useUnicode=true&amp;characterEncoding=UTF-8&amp;serverTimezone=GMT"></property>
           <property name="username" value="root"></property>
           <property name="password" value="123456789"></property>
   
       </bean>
       <!--  sqlSessionFactory  -->
       <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
           <property name="dataSource" ref="dataSource" />
           <!-- 绑定Mybatis配置文件       -->
           <property name="configLocation" value="classpath:mybatis-config.xml"></property>
           <property name="mapperLocations" value="classpath:com/zhang/mapper/*.xml"></property>
       </bean>
       <!-- SqlSessionTemplate:就是我们所使用的sqlSession     -->
       <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
           <!-- 只能用构造器注入sqlSessionFactory，因为没有set方法       -->
           <constructor-arg index="0" ref="sqlSessionFactory"></constructor-arg>
       </bean>
   
   
   </beans>
   ```

   如果 MyBatis 在映射器类对应的路径下找不到与之相对应的映射器 XML 文件，那么也需要配置文件。这时有两种解决办法：第一种是手动在 MyBatis 的 XML 配置文件中的 `<mappers>` 部分中指定 XML 文件的类路径；第二种是设置工厂 bean 的 `mapperLocations` 属性。

   自 1.3.0 版本开始，新增的 `configuration` 属性能够在没有对应的 MyBatis XML 配置文件的情况下，直接设置 `Configuration` 实例。

2. 编写UserMapper接口的实现类UserMapperImpl，私有化sqlSessionTemplate

   ```java
   public class UserMapperImpl implements UserMapper{
   //    我们所有的操作，原来都是用sqlSession，现在都使用sqlSessionFactory
       private SqlSessionTemplate sqlSession;
       public void setSqlSession(SqlSessionTemplate sqlSession){
           this.sqlSession = sqlSession;
       }
       @Override
       public List<User> selectUser() {
           UserMapper mapper = sqlSession.getMapper(UserMapper.class);
           return mapper.selectUser();
       }
   ```

3. 将自己编写的实现类，注入到spring-dao配置文件中

   ```xml
   <bean id="userMapper" class="com.zhang.mapper.UserMapperImpl">
           <property name="sqlSession" ref="sqlSession"></property>
       </bean>
   ```

   

4. 测试

   ```java
   public static void main(String[] args) throws IOException {
           ApplicationContext context = new ClassPathXmlApplicationContext("spring-dao.xml");
           UserMapper userMapper = context.getBean("userMapper",UserMapper.class);
           System.out.println(userMapper.selectUser());
       }
   ```

整合后，mybatis-config.xml配置文件内容如下：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <typeAliases>
        <package name="com.zhang.pojo"/>
    </typeAliases>
</configuration>
```

**整合实现方式二**

1. 修改方式一中的UserMapperImpl文件

   ```java
   @Override
   public List<User> selectUser() {
       return getSqlSession().getMapper(UserMapper.class).selectUser();
   }
   ```

2. 注册到spring配置文件中

   ```xml
   <bean id="userMapper2" class="com.zhang.mapper.UserMapperImpl2">
           <property name="sqlSessionFactory" ref="sqlSessionFactory"></property>
       </bean>
   ```

   

3. 测试

   ```java
   @Test
   public void test(){
       ApplicationContext context = new ClassPathXmlApplicationContext("spring-dao.xml");
       UserMapper mapper2 = context.getBean("userMapper2",UserMapper.class);
       System.out.println(mapper2.selectUser());
   
   }
   ```

## 14. 声明式事务

### 14.1 回顾事务

- 把一组业务当成一个业务来做，要么都成功，要么都失败。
- 事务在项目开发中，十分重要，涉及到数据的一致性问题，不容马虎。
- 确保完整性和一致性。

**事务ACID原则：**

- **原子性**：事务是原子性操作，由一系列动作组成；事务的原子性确保动作要么全部完成，要么失败
- **一致性**：一旦所有事务完成，事务就要被提交；数据和资源满足业务规则的一致性状态
- **隔离性**：事务与事务之间隔离开来，互不干扰
- **持久性**：事务一旦完成被提交，无论系统发生什么错误，结果都不会受到影响，通常情况下，事务的结果被写到持久化存储器中

利用上面案例的代码新建一个项目，为userMapper接口新增两个方法，删除和增加用户；

```java
    //增加业务
    public int addUser(User user);
    //删除业务
    public int delUserById(int id);
```



UserMapper文件中，故意将deletes写错，测试是否能够删除。

```java
        <delete id="delUserById" parameterType="int">
        delete from user where id = #{id};
        </delete>

        <select id="selectUser" resultType="user">
        select * from user;
    </select>
```

编写接口的UserMapperImpl实现类

```java
@Override
    public List<User> selectUser() {
//        User user1 = new User(8, "阿黄", "000000");
        UserMapper11 mapper = getSqlSession().getMapper(UserMapper11.class);
//        mapper.addUser(user1);
        mapper.delUserById(7);
        return mapper.selectUser();
    }
    @Override
    public int delUserById(int id) {
        return getSqlSession().getMapper(UserMapper11.class).delUserById(id);
    }
```



测试类：

```java
public static void main(String[] args) throws IOException {
        ApplicationContext context = new ClassPathXmlApplicationContext("spring-dao.xml");
        UserMapper11 userMapper = context.getBean("userMapper11", UserMapper11.class);
        for (User user : userMapper.selectUser()) {
            System.out.println(user);
        }
    }
```

测试结果：sql异常，delete错误，但数据库中成功插入数据，无法删除。
Spring中提供了事务管理，只需要配置即可。

### 14.2 Spring中的事务管理

Spring在不同的事务管理API之上定义了一个**抽象层**，使得开发人员不必了解底层的事务管理API就可以使用Spring的事务管理机制。

Spring**支持**

- **编程式事务管理**
- **声明式的事务管理**。

编程式事务管理：

- 将事务管理代码嵌到业务方法中，来控制事务的提交和回滚

- 缺点：必须在每个事务的操作逻辑中包含额外的事务管理代码

声明式事务管理：

- 一般情况下比编程式事务管理好用
- 将事务管理代码从业务方法中分离出来，以声明的方式来实现业务管理
- 将事务管理作为横切关注点，通过AOP方法模块化
- Spring中通过SpringAOP框架支持声明式事务管理

使用Spring的事务管理，需要在头文件导入tx约束

JDBC事务

配置好事务管理器我们需要配置事务的通知

Spring事务的传播特性：

- propagation_requierd：如果当前没有事务，就新建一个事务；如果当前有事务，那么就加入到这个事务（常用：**默认**）
- propagation_supports：支持当前事务，如果没有当前事务，就以非事务方法进行
- propagation_mandatory：使用当前事务，如果没有当前事务就抛出异常
- propagation_required_new：新建事务，如果当前存在事务，就挂起当前事务
- propagation_not_supported：以非事务执行，如果当前存在事务，就挂起当前事务
- propagation_never：以非事务执行，如果当前存在事务，就抛出异常
- propagation_nested：如果当前存在事务，则在嵌套事务内执行；如果当前没有事务，则执行与propagation_requierd类似的操作
- 

## 15. 总结

- Spring的核心：控制反转（IOC）和面向切面编程（AOP）。

- 在Spring中，创建一个实体类后，需要在Spring的核心配置文件(**.xml)中，通过bean的方式进行注册。相当于一个大容器中有了各类的对象，想用的时候直接取就行。

- IOC利用有参构造创建对象的三种方式：下标赋值、类型创建、参数名。无参构造直接赋值即可。

- 在配置文件中通过bean的方式注册类，就和java中通过new的方式生成对象类似。

- 类取别名：alias。多个配置文件的合并：import。

- 依赖注入：就相当于给类中的属性进行赋值。注入方式有：通过构造器的方式、通过set方法的方式。通过set的方式需要类里面有相应属性的set方法。可以给多种类型参数赋值：普通值、数组、集合等。

- P命名空间给属性赋值（直接注入）、C命名空间给属性赋值（利用构造器）。使用前需要导入xml约束。

- Bean的作用域（scope）：单例模式（singleton）和原型模式（prototype）。

- Bean自动装配：Spring在容器或上下文中自动寻找，并自动给bean匹配属性。byName：利用bean的id确定匹配，而byType利用bean的class确定匹配。同时，可以使用注解@Autowired和@Resources来进行自动装配，前提要在核心配置文件中开启注解的支持。

- 使用注解开发：需要导入AOP的包和开启注解支持。在类的上面加上@Component等同于在核心配置文件中注册bean，在属性的上面加上@value（*）可以直接对属性值注入。

- 使用Java配置Spring：在类的上面加上@Configuration代表该类为配置类，在类中方法的上面加上@Bean类似在核心配置文件中注册，方法名相当于bean中的id，返回值等同于bean中的class属性。

- 代理模式包括的角色：抽象角色（接口或抽象类）、真实角色、代理角色、客户。真实角色和代理角色要实现同一个接口。代理角色可以增加一些额外的操作，而真实角色的代码不用修改。静态代理：一个真实角色需要一个代理角色进行针对性的管理。动态代理：代理类是动态生成的，可以定义生成代理类的工具类，一个动态代理类可以代理多个类，只要实现了同一个接口。

- Spring实现AOP：实现了在执行方法前和后，可以自定义一些操作。方式有：① 实现API的接口（类似MethodBeforeAdvice和AfterReturningAdvice），在核心配置文件中配置AOP，设定切入点和执行环绕增加。 ② 自定义类实现AOP（主要是切面定义），在核心配置文件中定义切面、切入点和方法通知。 ③ 使用注解实现：自定义类，标注为切面，对方法进行标注，开启注解。

- Spring和Mybatis的整合：固定模板。

- Spring中有针对事务的管理办法，在核心配置文件中配置事务的通知即可（固定模板）。
  