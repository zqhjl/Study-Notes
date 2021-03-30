这篇文章主要是想通过一些问题，加深大家对于 Spring 的理解，所以不会涉及太多的代码！这篇文章整理了挺长时间，下面的很多问题我自己在使用 Spring 的过程中也并没有注意，自己也是临时查阅了很多资料和书籍补上的。网上也有一些很多关于 Spring 常见问题/面试题整理的文章，我感觉大部分都是互相 copy，而且很多问题也不是很好，有些回答也存在问题。所以，自己花了一周的业余时间整理了一下，希望对大家有帮助。
{: id="20210330211656-6oaerig"}

## 1. 什么是 Spring 框架?
{: id="20210330211656-retdvh7"}

Spring 是一种轻量级开发框架，旨在提高开发人员的开发效率以及系统的可维护性。Spring 官网：[https://spring.io/](https://spring.io/)。
{: id="20210330211656-jqrzhr9"}

我们一般说 Spring 框架指的都是 Spring Framework，它是很多模块的集合，使用这些模块可以很方便地协助我们进行开发。这些模块是：核心容器、数据访问/集成,、Web、AOP（面向切面编程）、工具、消息和测试模块。比如：Core Container 中的 Core 组件是Spring 所有组件的核心，Beans 组件和 Context 组件是实现IOC和依赖注入的基础，AOP组件用来实现面向切面编程。
{: id="20210330211656-ymtj288"}

Spring 官网列出的 Spring 的 6 个特征:
{: id="20210330211656-aad0nia"}

- {: id="20210330211656-u1y37kq"}**核心技术** ：依赖注入(DI)，AOP，事件(events)，资源，i18n，验证，数据绑定，类型转换，SpEL。
  {: id="20210330211656-ov84y3p"}
- {: id="20210330211656-y0xx6ep"}**测试** ：模拟对象，TestContext框架，Spring MVC 测试，WebTestClient。
  {: id="20210330211656-ghscxan"}
- {: id="20210330211656-pn1ylqg"}**数据访问** ：事务，DAO支持，JDBC，ORM，编组XML。
  {: id="20210330211656-y32yq0w"}
- {: id="20210330211656-j7pyf6j"}**Web支持** : Spring MVC和Spring WebFlux Web框架。
  {: id="20210330211656-zhi279q"}
- {: id="20210330211656-oirnb0v"}**集成** ：远程处理，JMS，JCA，JMX，电子邮件，任务，调度，缓存。
  {: id="20210330211656-l31v260"}
- {: id="20210330211656-a0cr3cr"}**语言** ：Kotlin，Groovy，动态语言。
  {: id="20210330211656-kh9p62y"}
{: id="20210330211656-jqap2la"}

## 2. 列举一些重要的Spring模块？
{: id="20210330211656-z1atwu4"}

下图对应的是 Spring4.x 版本。目前最新的5.x版本中 Web 模块的 Portlet 组件已经被废弃掉，同时增加了用于异步响应式处理的 WebFlux 组件。
{: id="20210330211656-nkozh6w"}

![Spring主要模块](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-6/Spring主要模块.png)
{: id="20210330211656-qvvzkkb"}

- {: id="20210330211656-x2d6bb2"}**Spring Core：** 基础,可以说 Spring 其他所有的功能都需要依赖于该类库。主要提供 IoC 依赖注入功能。
  {: id="20210330211656-4yakipv"}
- {: id="20210330211656-eamjb2z"}**Spring  Aspects** ： 该模块为与AspectJ的集成提供支持。
  {: id="20210330211656-trvgxgg"}
- {: id="20210330211656-ncmvi6u"}**Spring AOP** ：提供了面向切面的编程实现。
  {: id="20210330211656-rd8ofjx"}
- {: id="20210330211656-zi2w55i"}**Spring JDBC** : Java数据库连接。
  {: id="20210330211656-yih5ehs"}
- {: id="20210330211656-2gfm7d2"}**Spring JMS** ：Java消息服务。
  {: id="20210330211656-35t350m"}
- {: id="20210330211656-n3krgih"}**Spring ORM** : 用于支持Hibernate等ORM工具。
  {: id="20210330211656-zzdqdbx"}
- {: id="20210330211656-4awvcbs"}**Spring Web** : 为创建Web应用程序提供支持。
  {: id="20210330211656-0wnnks4"}
- {: id="20210330211656-31tdi7b"}**Spring Test** : 提供了对 JUnit 和 TestNG 测试的支持。
  {: id="20210330211656-v30vafo"}
{: id="20210330211656-hw1wkvz"}

## 3. @RestController vs @Controller
{: id="20210330211656-xokictz"}

**`Controller` 返回一个页面**
{: id="20210330211656-3p9egqh"}

单独使用 `@Controller` 不加 `@ResponseBody`的话一般使用在要返回一个视图的情况，这种情况属于比较传统的Spring MVC 的应用，对应于前后端不分离的情况。
{: id="20210330211656-0azdrcx"}

![SpringMVC 传统工作流程](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-7/SpringMVC传统工作流程.png)
{: id="20210330211656-qn4wabb"}

**`@RestController` 返回JSON 或 XML 形式数据**
{: id="20210330211656-1m1scyu"}

但`@RestController`只返回对象，对象数据直接以 JSON 或 XML 形式写入 HTTP 响应(Response)中，这种情况属于 RESTful Web服务，这也是目前日常开发所接触的最常用的情况（前后端分离）。
{: id="20210330211656-hham8u0"}

![SpringMVC+RestController](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-7/SpringMVCRestController.png)
{: id="20210330211656-ck5u8g0"}

**`@Controller +@ResponseBody` 返回JSON 或 XML 形式数据**
{: id="20210330211656-ew8ssom"}

如果你需要在Spring4之前开发 RESTful Web服务的话，你需要使用`@Controller` 并结合`@ResponseBody`注解，也就是说`@Controller` +`@ResponseBody`= `@RestController`（Spring 4 之后新加的注解）。
{: id="20210330211656-jomcb9x"}

> `@ResponseBody` 注解的作用是将 `Controller` 的方法返回的对象通过适当的转换器转换为指定的格式之后，写入到HTTP 响应(Response)对象的 body 中，通常用来返回 JSON 或者 XML 数据，返回 JSON 数据的情况比较多。
> {: id="20210330211656-pfwz3x1"}
{: id="20210330211656-ngy8f4s"}

![Spring3.xMVC RESTfulWeb服务工作流程](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-7/Spring3.xMVCRESTfulWeb服务工作流程.png)
{: id="20210330211656-xis3tti"}

Reference:
{: id="20210330211656-71xlrvc"}

- {: id="20210330211656-9ilqbbq"}https://dzone.com/articles/spring-framework-restcontroller-vs-controller （图片来源）
  {: id="20210330211656-t1hhs25"}
- {: id="20210330211656-5m3cgmh"}https://javarevisited.blogspot.com/2017/08/difference-between-restcontroller-and-controller-annotations-spring-mvc-rest.html?m=1
  {: id="20210330211656-zjba28k"}
{: id="20210330211656-m3thrna"}

## 4. Spring IOC & AOP
{: id="20210330211656-slmpgk8"}

### 4.1 谈谈自己对于 Spring IoC 和 AOP 的理解
{: id="20210330211656-mp3gyg4"}

#### IoC
{: id="20210330211656-z0m558a"}

IoC（Inverse of Control:控制反转）是一种**设计思想**，就是 **将原本在程序中手动创建对象的控制权，交由Spring框架来管理。**  IoC 在其他语言中也有应用，并非 Spring 特有。 **IoC 容器是 Spring 用来实现 IoC 的载体，  IoC 容器实际上就是个Map（key，value）,Map 中存放的是各种对象。**
{: id="20210330211656-o8hw2y3"}

将对象之间的相互依赖关系交给 IoC 容器来管理，并由 IoC 容器完成对象的注入。这样可以很大程度上简化应用的开发，把应用从复杂的依赖关系中解放出来。  **IoC 容器就像是一个工厂一样，当我们需要创建一个对象的时候，只需要配置好配置文件/注解即可，完全不用考虑对象是如何被创建出来的。** 在实际项目中一个 Service 类可能有几百甚至上千个类作为它的底层，假如我们需要实例化这个 Service，你可能要每次都要搞清这个 Service 所有底层类的构造函数，这可能会把人逼疯。如果利用 IoC 的话，你只需要配置好，然后在需要的地方引用就行了，这大大增加了项目的可维护性且降低了开发难度。
{: id="20210330211656-k64b9h9"}

Spring 时代我们一般通过 XML 文件来配置 Bean，后来开发人员觉得 XML 文件来配置不太好，于是 SpringBoot 注解配置就慢慢开始流行起来。
{: id="20210330211656-m94kfuk"}

推荐阅读：https://www.zhihu.com/question/23277575/answer/169698662
{: id="20210330211656-fpu6ksn"}

**Spring IoC的初始化过程：**
{: id="20210330211656-xg2yhan"}

![Spring IoC的初始化过程](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-7/SpringIOC初始化过程.png)
{: id="20210330211656-ng3uk0n"}

IoC源码阅读
{: id="20210330211656-dag920t"}

- {: id="20210330211656-8kthr4l"}https://javadoop.com/post/spring-ioc
  {: id="20210330211656-0jh6ns2"}
{: id="20210330211656-wa7cx8w"}

#### AOP
{: id="20210330211656-xolzpbg"}

AOP(Aspect-Oriented Programming:面向切面编程)能够将那些与业务无关，**却为业务模块所共同调用的逻辑或责任（例如事务处理、日志管理、权限控制等）封装起来**，便于**减少系统的重复代码**，**降低模块间的耦合度**，并**有利于未来的可拓展性和可维护性**。
{: id="20210330211656-o9f5zm3"}

**Spring AOP就是基于动态代理的**，如果要代理的对象，实现了某个接口，那么Spring AOP会使用**JDK Proxy**，去创建代理对象，而对于没有实现接口的对象，就无法使用 JDK Proxy 去进行代理了，这时候Spring AOP会使用**Cglib** ，这时候Spring AOP会使用 **Cglib** 生成一个被代理对象的子类来作为代理，如下图所示：
{: id="20210330211656-ey0dh9m"}

![SpringAOPProcess](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-6/SpringAOPProcess.jpg)
{: id="20210330211656-dldv4l2"}

当然你也可以使用 AspectJ ,Spring AOP 已经集成了AspectJ  ，AspectJ  应该算的上是 Java 生态系统中最完整的 AOP 框架了。
{: id="20210330211656-qj3es0b"}

使用 AOP 之后我们可以把一些通用功能抽象出来，在需要用到的地方直接使用即可，这样大大简化了代码量。我们需要增加新功能时也方便，这样也提高了系统扩展性。日志功能、事务管理等等场景都用到了 AOP 。
{: id="20210330211656-m2ca249"}

### 4.2 Spring AOP 和 AspectJ AOP 有什么区别？
{: id="20210330211656-ivh75pe"}

**Spring AOP 属于运行时增强，而 AspectJ 是编译时增强。** Spring AOP 基于代理(Proxying)，而 AspectJ 基于字节码操作(Bytecode Manipulation)。
{: id="20210330211656-zk8126b"}

Spring AOP 已经集成了 AspectJ  ，AspectJ  应该算的上是 Java 生态系统中最完整的 AOP 框架了。AspectJ  相比于 Spring AOP 功能更加强大，但是 Spring AOP 相对来说更简单，
{: id="20210330211656-bkhrfdr"}

如果我们的切面比较少，那么两者性能差异不大。但是，当切面太多的话，最好选择 AspectJ ，它比Spring AOP 快很多。
{: id="20210330211656-dzeou0n"}

## 5. Spring bean
{: id="20210330211656-ag3m0nj"}

### 5.1 Spring 中的 bean 的作用域有哪些?
{: id="20210330211656-7g3kfgp"}

- {: id="20210330211656-tww89k4"}singleton : 唯一 bean 实例，Spring 中的 bean 默认都是单例的。
  {: id="20210330211656-pvhamam"}
- {: id="20210330211656-0ta76ef"}prototype : 每次请求都会创建一个新的 bean 实例。
  {: id="20210330211656-10z7u8q"}
- {: id="20210330211656-klu9gb0"}request : 每一次HTTP请求都会产生一个新的bean，该bean仅在当前HTTP request内有效。
  {: id="20210330211656-h5hq612"}
- {: id="20210330211656-8dln0mf"}session : 每一次HTTP请求都会产生一个新的 bean，该bean仅在当前 HTTP session 内有效。
  {: id="20210330211656-4l4tzqa"}
- {: id="20210330211656-jy0y7zv"}global-session： 全局session作用域，仅仅在基于portlet的web应用中才有意义，Spring5已经没有了。Portlet是能够生成语义代码(例如：HTML)片段的小型Java Web插件。它们基于portlet容器，可以像servlet一样处理HTTP请求。但是，与 servlet 不同，每个 portlet 都有不同的会话
  {: id="20210330211656-omar8gp"}
{: id="20210330211656-k5onh9l"}

### 5.2 Spring 中的单例 bean 的线程安全问题了解吗？
{: id="20210330211656-vx68jlx"}

的确是存在安全问题的。因为，当多个线程操作同一个对象的时候，对这个对象的成员变量的写操作会存在线程安全问题。
{: id="20210330211656-ffg4pfm"}

但是，一般情况下，我们常用的 `Controller`、`Service`、`Dao` 这些 Bean 是无状态的。无状态的 Bean 不能保存数据，因此是线程安全的。
{: id="20210330211656-lr8lpeu"}

常见的有 2 种解决办法：
{: id="20210330211656-vbvve66"}

2. {: id="20210330211656-sbop0np"}在类中定义一个 `ThreadLocal` 成员变量，将需要的可变成员变量保存在  `ThreadLocal`  中（推荐的一种方式）。
   {: id="20210330211656-bl59eyk"}
3. {: id="20210330211656-tyf7qn2"}改变 Bean 的作用域为 “prototype”：每次请求都会创建一个新的 bean 实例，自然不会存在线程安全问题。
   {: id="20210330211656-z4lq933"}
{: id="20210330211656-6ye7zyd"}

### 5.3 @Component 和 @Bean 的区别是什么？
{: id="20210330211656-nq6y4h4"}

1. {: id="20210330211656-cdy944w"}作用对象不同: `@Component` 注解作用于类，而`@Bean`注解作用于方法。
   {: id="20210330211656-9ccoxn2"}
2. {: id="20210330211656-2qc0mr2"}`@Component`通常是通过类路径扫描来自动侦测以及自动装配到Spring容器中（我们可以使用 `@ComponentScan` 注解定义要扫描的路径从中找出标识了需要装配的类自动装配到 Spring 的 bean 容器中）。`@Bean` 注解通常是我们在标有该注解的方法中定义产生这个 bean,`@Bean`告诉了Spring这是某个类的示例，当我需要用它的时候还给我。
   {: id="20210330211656-azk4q9t"}
3. {: id="20210330211656-wp9o3ih"}`@Bean` 注解比 `Component` 注解的自定义性更强，而且很多地方我们只能通过 `@Bean` 注解来注册bean。比如当我们引用第三方库中的类需要装配到 `Spring`容器时，则只能通过 `@Bean`来实现。
   {: id="20210330211656-807zjsv"}
{: id="20210330211656-r7ulnff"}

`@Bean`注解使用示例：
{: id="20210330211656-k6k3enc"}

```java
@Configuration
public class AppConfig {
    @Bean
    public TransferService transferService() {
        return new TransferServiceImpl();
    }

}
```
{: id="20210330211656-rd71s1q"}

上面的代码相当于下面的 xml 配置
{: id="20210330211656-ms52kxf"}

```xml
<beans>
    <bean id="transferService" class="com.acme.TransferServiceImpl"/>
</beans>
```
{: id="20210330211656-qi4jgew"}

下面这个例子是通过 `@Component` 无法实现的。
{: id="20210330211656-pjj3im1"}

```java
@Bean
public OneService getService(status) {
    case (status)  {
        when 1:
                return new serviceImpl1();
        when 2:
                return new serviceImpl2();
        when 3:
                return new serviceImpl3();
    }
}
```
{: id="20210330211656-40kj7x7"}

### 5.4 将一个类声明为Spring的 bean 的注解有哪些?
{: id="20210330211656-xuhhzpp"}

我们一般使用 `@Autowired` 注解自动装配 bean，要想把类标识成可用于 `@Autowired` 注解自动装配的 bean 的类,采用以下注解可实现：
{: id="20210330211656-t0f9wxo"}

- {: id="20210330211656-a5spby6"}`@Component` ：通用的注解，可标注任意类为 `Spring` 组件。如果一个Bean不知道属于哪个层，可以使用`@Component` 注解标注。
  {: id="20210330211656-hee85kc"}
- {: id="20210330211656-8cls0s3"}`@Repository` : 对应持久层即 Dao 层，主要用于数据库相关操作。
  {: id="20210330211656-4pnxfhp"}
- {: id="20210330211656-m4eepqj"}`@Service` : 对应服务层，主要涉及一些复杂的逻辑，需要用到 Dao层。
  {: id="20210330211656-s9o6dwt"}
- {: id="20210330211656-5c140xz"}`@Controller` : 对应 Spring MVC 控制层，主要用于接受用户请求并调用 Service 层返回数据给前端页面。
  {: id="20210330211656-b4gbxac"}
{: id="20210330211656-jta4182"}

### 5.5 Spring 中的 bean 生命周期?
{: id="20210330211656-znzkuqj"}

这部分网上有很多文章都讲到了，下面的内容整理自： ~~https://yemengying.com/2016/07/14/spring-bean-life-cycle/~~ (原作者可能不再维护这个博客，连接无法访问，可通过其 Github 仓库访问 [https://github.com/giraffe0813/giraffe0813.github.io](https://github.com/giraffe0813/giraffe0813.github.io)) ，除了这篇文章，再推荐一篇很不错的文章 ：[https://www.cnblogs.com/zrtqsk/p/3735273.html](https://www.cnblogs.com/zrtqsk/p/3735273.html) 。
{: id="20210330211656-ab9azgi"}

- {: id="20210330211656-toi1dlq"}Bean 容器找到配置文件中 Spring Bean 的定义。
  {: id="20210330211656-y0l96c2"}
- {: id="20210330211656-5z6lrhm"}Bean 容器利用 Java Reflection API 创建一个Bean的实例。
  {: id="20210330211656-c43b97i"}
- {: id="20210330211656-omguxi9"}如果涉及到一些属性值 利用 `set()`方法设置一些属性值。
  {: id="20210330211656-r5l0wg8"}
- {: id="20210330211656-5paropu"}如果 Bean 实现了 `BeanNameAware` 接口，调用 `setBeanName()`方法，传入Bean的名字。
  {: id="20210330211656-v6txiu6"}
- {: id="20210330211656-ael9120"}如果 Bean 实现了 `BeanClassLoaderAware` 接口，调用 `setBeanClassLoader()`方法，传入 `ClassLoader`对象的实例。
  {: id="20210330211656-z3emlru"}
- {: id="20210330211656-rpt95wq"}与上面的类似，如果实现了其他 `*.Aware`接口，就调用相应的方法。
  {: id="20210330211656-lvdij92"}
- {: id="20210330211656-4inkx25"}如果有和加载这个 Bean 的 Spring 容器相关的 `BeanPostProcessor` 对象，执行`postProcessBeforeInitialization()` 方法
  {: id="20210330211656-bhlg9s6"}
- {: id="20210330211656-d7381nh"}如果Bean实现了`InitializingBean`接口，执行`afterPropertiesSet()`方法。
  {: id="20210330211656-fv5hxwz"}
- {: id="20210330211656-9u7s5ub"}如果 Bean 在配置文件中的定义包含  init-method 属性，执行指定的方法。
  {: id="20210330211656-ogmy4ae"}
- {: id="20210330211656-eon5aq5"}如果有和加载这个 Bean的 Spring 容器相关的 `BeanPostProcessor` 对象，执行`postProcessAfterInitialization()` 方法
  {: id="20210330211656-negkcwf"}
- {: id="20210330211656-zxb03lv"}当要销毁 Bean 的时候，如果 Bean 实现了 `DisposableBean` 接口，执行 `destroy()` 方法。
  {: id="20210330211656-7je9w7s"}
- {: id="20210330211656-cbxt6bq"}当要销毁 Bean 的时候，如果 Bean 在配置文件中的定义包含 destroy-method 属性，执行指定的方法。
  {: id="20210330211656-obxre6r"}
{: id="20210330211656-9xa4wgm"}

图示：
{: id="20210330211656-lhwaki0"}

![Spring Bean 生命周期](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-9-17/48376272.jpg)
{: id="20210330211656-wfqlv7p"}

与之比较类似的中文版本:
{: id="20210330211656-vfhslc6"}

![Spring Bean 生命周期](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-9-17/5496407.jpg)
{: id="20210330211656-wibpmf7"}

## 6. Spring MVC
{: id="20210330211656-mn5bfpc"}

### 6.1 说说自己对于 Spring MVC 了解?
{: id="20210330211656-7novabb"}

谈到这个问题，我们不得不提提之前 Model1 和 Model2 这两个没有 Spring MVC 的时代。
{: id="20210330211656-n2kju0u"}

- {: id="20210330211656-z4ao3gw"}**Model1 时代** : 很多学 Java 后端比较晚的朋友可能并没有接触过  Model1 模式下的 JavaWeb 应用开发。在 Model1 模式下，整个 Web 应用几乎全部用 JSP 页面组成，只用少量的 JavaBean 来处理数据库连接、访问等操作。这个模式下 JSP 既是控制层又是表现层。显而易见，这种模式存在很多问题。比如①将控制逻辑和表现逻辑混杂在一起，导致代码重用率极低；②前端和后端相互依赖，难以进行测试并且开发效率极低；
  {: id="20210330211656-oaaiqwg"}
- {: id="20210330211656-ac8sy68"}**Model2 时代** ：学过 Servlet 并做过相关 Demo 的朋友应该了解“Java Bean(Model)+ JSP（View,）+Servlet（Controller）  ”这种开发模式,这就是早期的 JavaWeb MVC 开发模式。Model:系统涉及的数据，也就是 dao 和 bean。View：展示模型中的数据，只是用来展示。Controller：处理用户请求都发送给 ，返回数据给 JSP 并展示给用户。
  {: id="20210330211656-312ku20"}
{: id="20210330211656-3rs8d02"}

Model2 模式下还存在很多问题，Model2的抽象和封装程度还远远不够，使用Model2进行开发时不可避免地会重复造轮子，这就大大降低了程序的可维护性和复用性。于是很多JavaWeb开发相关的 MVC 框架应运而生比如Struts2，但是 Struts2 比较笨重。随着 Spring 轻量级开发框架的流行，Spring 生态圈出现了 Spring MVC 框架， Spring MVC 是当前最优秀的 MVC 框架。相比于 Struts2 ， Spring MVC 使用更加简单和方便，开发效率更高，并且 Spring MVC 运行速度更快。
{: id="20210330211656-xzduin1"}

MVC 是一种设计模式,Spring MVC 是一款很优秀的 MVC 框架。Spring MVC 可以帮助我们进行更简洁的Web层的开发，并且它天生与 Spring 框架集成。Spring MVC 下我们一般把后端项目分为 Service层（处理业务）、Dao层（数据库操作）、Entity层（实体类）、Controller层(控制层，返回数据给前台页面)。
{: id="20210330211656-7bd7mb1"}

**Spring MVC 的简单原理图如下：**
{: id="20210330211656-qmq11ex"}

![](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-10-11/60679444.jpg)
{: id="20210330211656-9jm4mqo"}

### 6.2 SpringMVC 工作原理了解吗?
{: id="20210330211656-96lxgy4"}

**原理如下图所示：**
![SpringMVC运行原理](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-10-11/49790288.jpg)
{: id="20210330211656-w61wucr"}

上图的一个笔误的小问题：Spring MVC 的入口函数也就是前端控制器 `DispatcherServlet` 的作用是接收请求，响应结果。
{: id="20210330211656-51dxhgj"}

**流程说明（重要）：**
{: id="20210330211656-a9o7eh5"}

1. {: id="20210330211656-ambang0"}客户端（浏览器）发送请求，直接请求到 `DispatcherServlet`。
   {: id="20210330211656-c4liinh"}
2. {: id="20210330211656-pt77paa"}`DispatcherServlet` 根据请求信息调用 `HandlerMapping`，解析请求对应的 `Handler`。
   {: id="20210330211656-4gncev8"}
3. {: id="20210330211656-05shcnx"}解析到对应的 `Handler`（也就是我们平常说的 `Controller` 控制器）后，开始由 `HandlerAdapter` 适配器处理。
   {: id="20210330211656-z7m4fa4"}
4. {: id="20210330211656-st86tal"}`HandlerAdapter` 会根据 `Handler `来调用真正的处理器来处理请求，并处理相应的业务逻辑。
   {: id="20210330211656-2jaro18"}
5. {: id="20210330211656-jky9v2n"}处理器处理完业务后，会返回一个 `ModelAndView` 对象，`Model` 是返回的数据对象，`View` 是个逻辑上的 `View`。
   {: id="20210330211656-w0r9rey"}
6. {: id="20210330211656-0q2hp8t"}`ViewResolver` 会根据逻辑 `View` 查找实际的 `View`。
   {: id="20210330211656-8c7k7jp"}
7. {: id="20210330211656-32lnswk"}`DispaterServlet` 把返回的 `Model` 传给 `View`（视图渲染）。
   {: id="20210330211656-4c00cjy"}
8. {: id="20210330211656-0sbsg71"}把 `View` 返回给请求者（浏览器）
   {: id="20210330211656-vxjav2n"}
{: id="20210330211656-mm3wq2v"}

## 7. Spring 框架中用到了哪些设计模式？
{: id="20210330211656-cj9882c"}

关于下面一些设计模式的详细介绍，可以看笔主前段时间的原创文章[《面试官:“谈谈Spring中都用到了那些设计模式?”。》](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247485303&idx=1&sn=9e4626a1e3f001f9b0d84a6fa0cff04a&chksm=cea248bcf9d5c1aaf48b67cc52bac74eb29d6037848d6cf213b0e5466f2d1fda970db700ba41&token=255050878&lang=zh_CN#rd) 。
{: id="20210330211656-jgw92bw"}

- {: id="20210330211656-8sjx6uh"}**工厂设计模式** : Spring使用工厂模式通过 `BeanFactory`、`ApplicationContext` 创建 bean 对象。
  {: id="20210330211656-hhj9ceb"}
- {: id="20210330211656-zu8ot09"}**代理设计模式** : Spring AOP 功能的实现。
  {: id="20210330211656-p72mdam"}
- {: id="20210330211656-wm7csa6"}**单例设计模式** : Spring 中的 Bean 默认都是单例的。
  {: id="20210330211656-4x7ub5r"}
- {: id="20210330211656-ng3gw5f"}**模板方法模式** : Spring 中 `jdbcTemplate`、`hibernateTemplate` 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。
  {: id="20210330211656-lm37bkz"}
- {: id="20210330211656-q172h8p"}**包装器设计模式** : 我们的项目需要连接多个数据库，而且不同的客户在每次访问中根据需要会去访问不同的数据库。这种模式让我们可以根据客户的需求能够动态切换不同的数据源。
  {: id="20210330211656-iwesck1"}
- {: id="20210330211656-do4yygx"}**观察者模式:** Spring 事件驱动模型就是观察者模式很经典的一个应用。
  {: id="20210330211656-wexu804"}
- {: id="20210330211656-ulenuwk"}**适配器模式** :Spring AOP 的增强或通知(Advice)使用到了适配器模式、spring MVC 中也是用到了适配器模式适配`Controller`。
  {: id="20210330211656-1mowdy6"}
- {: id="20210330211656-if68o8q"}......
  {: id="20210330211656-f0kttax"}
{: id="20210330211656-iah2jvo"}

## 8. Spring 事务
{: id="20210330211656-85xh77x"}

### 8.1 Spring 管理事务的方式有几种？
{: id="20210330211656-vu33ugn"}

1. {: id="20210330211656-gimfeuv"}编程式事务，在代码中硬编码。(不推荐使用)
   {: id="20210330211656-p858wr8"}
2. {: id="20210330211656-w36x0a3"}声明式事务，在配置文件中配置（推荐使用）
   {: id="20210330211656-jiopfmd"}
{: id="20210330211656-p5bsril"}

**声明式事务又分为两种：**
{: id="20210330211656-cl6pbd7"}

1. {: id="20210330211656-hs86wlk"}基于XML的声明式事务
   {: id="20210330211656-y2afbfn"}
2. {: id="20210330211656-ho4mscc"}基于注解的声明式事务
   {: id="20210330211656-4p7f91q"}
{: id="20210330211656-ejkm2l2"}

### 8.2 Spring 事务中的隔离级别有哪几种?
{: id="20210330211656-l9kudim"}

**TransactionDefinition 接口中定义了五个表示隔离级别的常量：**
{: id="20210330211656-pwhp6dx"}

- {: id="20210330211656-hzbaojv"}**TransactionDefinition.ISOLATION_DEFAULT:**  使用后端数据库默认的隔离级别，Mysql 默认采用的 REPEATABLE_READ隔离级别 Oracle 默认采用的 READ_COMMITTED隔离级别.
  {: id="20210330211656-8dx3inp"}
- {: id="20210330211656-ddjvsqp"}**TransactionDefinition.ISOLATION_READ_UNCOMMITTED:** 最低的隔离级别，允许读取尚未提交的数据变更，**可能会导致脏读、幻读或不可重复读**
  {: id="20210330211656-ajvqlw8"}
- {: id="20210330211656-rylmp5t"}**TransactionDefinition.ISOLATION_READ_COMMITTED:**   允许读取并发事务已经提交的数据，**可以阻止脏读，但是幻读或不可重复读仍有可能发生**
  {: id="20210330211656-kjrscgj"}
- {: id="20210330211656-6pad98n"}**TransactionDefinition.ISOLATION_REPEATABLE_READ:**  对同一字段的多次读取结果都是一致的，除非数据是被本身事务自己所修改，**可以阻止脏读和不可重复读，但幻读仍有可能发生。**
  {: id="20210330211656-lm1rack"}
- {: id="20210330211656-chgd41l"}**TransactionDefinition.ISOLATION_SERIALIZABLE:**   最高的隔离级别，完全服从ACID的隔离级别。所有的事务依次逐个执行，这样事务之间就完全不可能产生干扰，也就是说，**该级别可以防止脏读、不可重复读以及幻读**。但是这将严重影响程序的性能。通常情况下也不会用到该级别。
  {: id="20210330211656-8vvjoao"}
{: id="20210330211656-cq9y38i"}

### 8.3 Spring 事务中哪几种事务传播行为?
{: id="20210330211656-5t6jnw1"}

**支持当前事务的情况：**
{: id="20210330211656-s4sl6iu"}

- {: id="20210330211656-5jmwyr9"}**TransactionDefinition.PROPAGATION_REQUIRED：** 如果当前存在事务，则加入该事务；如果当前没有事务，则创建一个新的事务。
  {: id="20210330211656-qubh4xd"}
- {: id="20210330211656-uzqas9l"}**TransactionDefinition.PROPAGATION_SUPPORTS：** 如果当前存在事务，则加入该事务；如果当前没有事务，则以非事务的方式继续运行。
  {: id="20210330211656-fp8pgsr"}
- {: id="20210330211656-q461nm8"}**TransactionDefinition.PROPAGATION_MANDATORY：** 如果当前存在事务，则加入该事务；如果当前没有事务，则抛出异常。（mandatory：强制性）
  {: id="20210330211656-cy5bbm2"}
{: id="20210330211656-dx0wq0m"}

**不支持当前事务的情况：**
{: id="20210330211656-yskv9xx"}

- {: id="20210330211656-firkj6k"}**TransactionDefinition.PROPAGATION_REQUIRES_NEW：** 创建一个新的事务，如果当前存在事务，则把当前事务挂起。
  {: id="20210330211656-h5wdfeg"}
- {: id="20210330211656-3b0q8p5"}**TransactionDefinition.PROPAGATION_NOT_SUPPORTED：** 以非事务方式运行，如果当前存在事务，则把当前事务挂起。
  {: id="20210330211656-vlxoa7j"}
- {: id="20210330211656-2ei9vdf"}**TransactionDefinition.PROPAGATION_NEVER：** 以非事务方式运行，如果当前存在事务，则抛出异常。
  {: id="20210330211656-34p6blt"}
{: id="20210330211656-7qyeet8"}

**其他情况：**
{: id="20210330211656-xjvvnsb"}

- {: id="20210330211656-y5eehih"}**TransactionDefinition.PROPAGATION_NESTED：** 如果当前存在事务，则创建一个事务作为当前事务的嵌套事务来运行；如果当前没有事务，则该取值等价于TransactionDefinition.PROPAGATION_REQUIRED。
  {: id="20210330211656-38ctl53"}
{: id="20210330211656-zbo8bih"}

### 8.4 @Transactional(rollbackFor = Exception.class)注解了解吗？
{: id="20210330211656-u44w7wq"}

我们知道：Exception分为运行时异常RuntimeException和非运行时异常。事务管理对于企业应用来说是至关重要的，即使出现异常情况，它也可以保证数据的一致性。
{: id="20210330211656-445owcg"}

当`@Transactional`注解作用于类上时，该类的所有 public 方法将都具有该类型的事务属性，同时，我们也可以在方法级别使用该标注来覆盖类级别的定义。如果类或者方法加了这个注解，那么这个类里面的方法抛出异常，就会回滚，数据库里面的数据也会回滚。
{: id="20210330211656-byvbuv5"}

在`@Transactional`注解中如果不配置`rollbackFor`属性,那么事务只会在遇到`RuntimeException`的时候才会回滚,加上`rollbackFor=Exception.class`,可以让事务在遇到非运行时异常时也回滚。
{: id="20210330211656-bx4n0l0"}

关于 `@Transactional ` 注解推荐阅读的文章：
{: id="20210330211656-yw3ylko"}

- {: id="20210330211656-whmv23s"}[透彻的掌握 Spring 中@transactional 的使用](https://www.ibm.com/developerworks/cn/java/j-master-spring-transactional-use/index.html)
  {: id="20210330211656-dmlymgg"}
{: id="20210330211656-do01l5u"}

## 9. JPA
{: id="20210330211656-oh0qh89"}

### 9.1 如何使用JPA在数据库中非持久化一个字段？
{: id="20210330211656-0cj3m99"}

假如我们有有下面一个类：
{: id="20210330211656-exb365h"}

```java
Entity(name="USER")
public class User {
    
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    @Column(name = "ID")
    private Long id;
    
    @Column(name="USER_NAME")
    private String userName;
    
    @Column(name="PASSWORD")
    private String password;
  
    private String secrect;
  
}
```
{: id="20210330211656-ah29c9n"}

如果我们想让`secrect` 这个字段不被持久化，也就是不被数据库存储怎么办？我们可以采用下面几种方法：
{: id="20210330211656-twe75tg"}

```java
static String transient1; // not persistent because of static
final String transient2 = “Satish”; // not persistent because of final
transient String transient3; // not persistent because of transient
@Transient
String transient4; // not persistent because of @Transient
```
{: id="20210330211656-u54nr8y"}

一般使用后面两种方式比较多，我个人使用注解的方式比较多。
{: id="20210330211656-n9ts1se"}

## 参考
{: id="20210330211656-78f3men"}

- {: id="20210330211656-9m4jib6"}《Spring 技术内幕》
  {: id="20210330211656-859s7g7"}
- {: id="20210330211656-os1ic5u"}[http://www.cnblogs.com/wmyskxz/p/8820371.html](http://www.cnblogs.com/wmyskxz/p/8820371.html)
  {: id="20210330211656-9r4qaa9"}
- {: id="20210330211656-h5rkzta"}[https://www.journaldev.com/2696/spring-interview-questions-and-answers](https://www.journaldev.com/2696/spring-interview-questions-and-answers)
  {: id="20210330211656-bc8ewfi"}
- {: id="20210330211656-xny3by1"}[https://www.edureka.co/blog/interview-questions/spring-interview-questions/](https://www.edureka.co/blog/interview-questions/spring-interview-questions/)
  {: id="20210330211656-s2ucia3"}
- {: id="20210330211656-mj3tfn8"}https://www.cnblogs.com/clwydjgs/p/9317849.html
  {: id="20210330211656-gv95v9e"}
- {: id="20210330211656-dfp7w0l"}[https://howtodoinjava.com/interview-questions/top-spring-interview-questions-with-answers/](https://howtodoinjava.com/interview-questions/top-spring-interview-questions-with-answers/)
  {: id="20210330211656-czobi9m"}
- {: id="20210330211656-y3hhwzt"}[http://www.tomaszezula.com/2014/02/09/spring-series-part-5-component-vs-bean/](http://www.tomaszezula.com/2014/02/09/spring-series-part-5-component-vs-bean/)
  {: id="20210330211656-g1covtc"}
- {: id="20210330211656-uqtdvsy"}[https://stackoverflow.com/questions/34172888/difference-between-bean-and-autowired](https://stackoverflow.com/questions/34172888/difference-between-bean-and-autowired)
  {: id="20210330211656-fn19r6s"}
- {: id="20210330211656-d4l337p"}[https://www.interviewbit.com/spring-interview-questions/](https://www.interviewbit.com/spring-interview-questions/)
  {: id="20210330211656-jlw9p4m"}
{: id="20210330211656-4ss1wtw"}

## 公众号
{: id="20210330211656-4r99wb2"}

如果大家想要实时关注我更新的文章以及分享的干货的话，可以关注我的公众号。
{: id="20210330211656-td8ocr2"}

**《Java面试突击》:** 由本文档衍生的专为面试而生的《Java面试突击》V2.0 PDF 版本[公众号](#公众号)后台回复 **"Java面试突击"** 即可免费领取！
{: id="20210330211656-580pg4r"}

**Java工程师必备学习资源:** 一些Java工程师常用学习资源公众号后台回复关键字 **“1”** 即可免费无套路获取。
{: id="20210330211656-tukubav"}

![公众号](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-7/javaguide1.jpg)
{: id="20210330211656-ynk6o94"}


{: id="20210330211656-g3lxayb" type="doc"}
