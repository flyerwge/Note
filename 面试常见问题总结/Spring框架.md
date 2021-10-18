# Spring框架

## 1 Spring基础

Spring是一个开源应用框架，旨在降低应用程序开发的复杂度，提高系统的可维护性

Spring 特性：轻量、控制反转、面向容器、面向切面和框架灵活

### 1.1 Spring Bean

- 它们是构成用户应用程序主干的对象
- Bean由Spring IOC容器管理
- 它们由Spring IOC容器实例化、配置、装配和管理
- Bean是基于用户提供给容器的配置元数据创建

### 1.2  Spring 中 Bean的生命周期

在传统的Java应用中，bean的生命周期很简单，使用Java关键字new进行Bean的实例化，然后Bean就可以使用了，一旦Bean不再被使用，则由Java自动进行垃圾回收。

Spring 管理Bean的生命周期：

1. 实例化：实例化一个bean对象；
2. 属性赋值：为bean设置相关属性和依赖；
3. 初始化：
4. 销毁：

### 1.3 Spring中Bean的作用域

- singleton：Spring中bean默认是单例的；
- prototype：每次请求都会创建一个新的bean实例；
- request：每一次HTTP请求都会产生一个新的bean，该bean仅在当前HTTP request内有效；
- session：每一次HTTP请求都会产生一个新的bean，该bean仅在当前HTTP session内有效；
- global-session：全局session作用域，仅仅在基于portlet的web应用中才有意义；

### 1.4 Spring 中的单例bean的线程安全问题

单例bean存在线程安全问题，因为当多个线程操作同一个对象的时候，对这个对象的非静态成员变量的写操作存在线程安全问题；

解决方法：1）在bean对象中尽量避免定义可变的成员变量；2）在类中定义一个ThreadLocal成员变量，将需要的可变成员变量保存在ThreadLocal中；

### 1.5 Spring装配

当bean在Spring容器中组合在一起时，被称为bean装配。Spring容器需要知道需要什么bean，以及容器应该如何使用依赖注入来将bean绑定在一起，同时装配bean。

### 1.6 Spring自动装配方式

Spring容器能够自动装配bean，即可以通过检查BeanFactory的内容让Spring自动解析bean的协作者；

自动装配的不同模式：

- no：默认设置，没有自动装配；
- byName：根据bean的名称注入对象依赖项；
- byType：根据类型注入对象依赖项；
- 构造函数：通过调用类的构造函数来注入依赖项；
- autodetect：首先容器尝试通过构造函数使用autowire装配，如果不能，则尝试通过byType自动装配。

### 1.7 Spring中的事务传播行为

事务传播行为是为了解决业务层方法之间互相调用的事务问题。当事务方法被另一个事务方法调用时，必须指定事务应该如何传播

### 1.8 Spring注解

- @SpringBootApplication：包含@Configuration、@EnableAutoConfiguration、@ComponentScan；通常用在主类上；
- @Configuration：指出该类是bean配置的信息源；
- @EnableAutoConfiguration：让Spring Boot根据应用所声明的依赖来对Spring框架进行自动配置；
- @ComponentScan：组件扫描
- @Repository：用于标注数据访问组件，即DAO组件；
- @Service：用于标注业务层组件
- @RestController：用于标注控制层组件，包含@Controller和@ResponseBody，返回JSON/XML数据；
- @Controller：用于标注控制层组件，返回页面；
- @ResponseBody：将Java对象转为json格式的数据；
- @Component：泛指组件，当组件不好归类时，可以使用这个注解进行标注；
- @Bean：放在方法上面，产生一个Bean，并交给Spring管理；
- @RequestMapping：用来处理请求地址映射，可用于类或方法上；

## 2 Spring IOC

控制反转：指一个对象依赖的其他对象将会在容器的初始化完成后主动将其依赖的对象传递给它，而不需要这个对象自己创建或者查找其依赖的对象。对象之间的相互依赖关系交给IOC容器来管理，并由IOC容器完成对象的注入。

### 2.1 如何实现一个简单的IOC容器

一个简单的思路是利用HashMap存储所有实例，key代表标签的id，value存储对应的实例；

### 2.2 Spring IOC控制反转依赖注入和new对象的区别

- new对象单例中如果要做到注入的效果就是在类的头部进行实例化对象，这个时候不管该对象使用与否都贯穿类的始终。该类对象不被回收，这个实例化对象也不会被回收。
- 依赖注入指的是调用者使用到被调用对象才会从Spring容器中取出依赖的对象注入到使用的类中，如果不用则会放回Spring容器的对象池中，做到内存节省并且代码的耦合度也降低。

## 3 Spring AOP面向切面编程

能够将那些与业务无关，却为业务模块所共同调用的逻辑或责任（例如事务处理、日志管理、权限控制等）封装起来，便于减少系统的重复代码，降低模块间的耦合度，并有利于未来的可扩展性和可维护性。

### 3.1 AOP的基本概念

- 切入点：选择指定的方法进行织入，用切点来筛选连接点，选中我们想要的那些方法
- 通知：我们想要的功能（如日志），用来组件Aspect到底需要处理哪些逻辑
- 切面：通知和切入点的结合
- 织入：创建代理对象，把切面应用到代理对象上的过程

## 4 Spring MVC

目的：将M和V的实现代码分离，使同一个程序可以有不同的表现形式

- 数据模型层（Model）:负责数据逻辑的处理和实验数据操作；
- 视图层（View）:负责格式化数据并呈现给用户；
- 控制层（Controller）：负责接收并转发请求，对请求进行处理后，指定视图，并将响应结果发送给客户端；

## 5 Spring Cloud微服务

### 5.1 Nacos与Eureka比较

项目中选用Nacos的原因？

1. Nacos功能强大，几乎原生支持所有服务，并能够提供控制台管理；
2. Nacos是纯国产，有中文文档，入门简单；
3. Eureka2.0闭源

## 6 Nginx原理

正向代理：用户无法正常访问外部资源，通过代理的方式，让用户绕过防火墙，从而连接到目标网络或者服务

反向代理：以代理服务器来接收连接请求，然后将请求转发给内部网络上的服务器，并将从服务器上得到的结果返回给网络上请求连接的客户端，此时代理服务器对外表现就是一个服务器。





