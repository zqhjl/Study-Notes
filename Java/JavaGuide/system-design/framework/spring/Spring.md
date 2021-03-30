## Spring相关教程/资料
{: id="20210330211656-2hfhgeb"}

### 官网相关
{: id="20210330211656-slppugy"}

- {: id="20210330211656-a3jzs08"}[Spring官网](https://spring.io/)、[Spring系列主要项目](https://spring.io/projects)、[Spring官网指南](https://spring.io/guides)、[官方文档](https://spring.io/docs/reference)
  {: id="20210330211656-ipydkl6"}
- {: id="20210330211656-90f2hd2"}[spring-framework-reference](https://docs.spring.io/spring/docs/5.0.14.RELEASE/spring-framework-reference/index.html)
  {: id="20210330211656-cki73ab"}
- {: id="20210330211656-6u02lzi"}[Spring Framework 4.3.17.RELEASE API](https://docs.spring.io/spring/docs/4.3.17.RELEASE/javadoc-api/)
  {: id="20210330211656-566mbfz"}
{: id="20210330211656-naka0y0"}

## 系统学习教程
{: id="20210330211656-abnxwx6"}

### 文档
{: id="20210330211656-r3ri358"}

- {: id="20210330211656-bohibj4"}[极客学院Spring Wiki](http://wiki.jikexueyuan.com/project/spring/transaction-management.html)
  {: id="20210330211656-jbg9ape"}
- {: id="20210330211656-vvyfrjk"}[Spring W3Cschool教程 ](https://www.w3cschool.cn/wkspring/f6pk1ic8.html)
  {: id="20210330211656-0zpzvqc"}
{: id="20210330211656-9oi593g"}

### 视频
{: id="20210330211656-hsc0qox"}

- {: id="20210330211656-h7a5nlh"}[网易云课堂——58集精通java教程Spring框架开发](http://study.163.com/course/courseMain.htm?courseId=1004475015#/courseDetail?tab=1&35)
  {: id="20210330211656-4bebtv3"}
- {: id="20210330211656-5mjavxa"}[慕课网相关视频](https://www.imooc.com/)
  {: id="20210330211656-spgjngw"}
- {: id="20210330211656-jx1pjfb"}**黑马视频和尚硅谷视频（非常推荐）：** 微信公众号：“**JavaGuide**”后台回复关键字 “**1**” 免费领取。
  {: id="20210330211656-ipptfv4"}
{: id="20210330211656-sgkglc7"}

## 面试必备知识点
{: id="20210330211656-51cowfq"}

### SpringAOP,IOC实现原理
{: id="20210330211656-nl7m5sn"}

AOP实现原理、动态代理和静态代理、Spring IOC的初始化过程、IOC原理、自己实现怎么实现一个IOC容器？这些东西都是经常会被问到的。
{: id="20210330211656-huejtdj"}

推荐阅读：
{: id="20210330211656-a8lskrx"}

- {: id="20210330211656-1d25xcn"}[自己动手实现的 Spring IOC 和 AOP - 上篇](http://www.coolblog.xyz/2018/01/18/自己动手实现的-Spring-IOC-和-AOP-上篇/)
  {: id="20210330211656-p0v5rzz"}
- {: id="20210330211656-u5m2sao"}[自己动手实现的 Spring IOC 和 AOP - 下篇](http://www.coolblog.xyz/2018/01/18/自己动手实现的-Spring-IOC-和-AOP-下篇/)
  {: id="20210330211656-et52pby"}
{: id="20210330211656-esmugvy"}

### AOP
{: id="20210330211656-rh6b9j3"}

AOP思想的实现一般都是基于 **代理模式** ，在JAVA中一般采用JDK动态代理模式，但是我们都知道，**JDK动态代理模式只能代理接口而不能代理类**。因此，Spring AOP 会这样子来进行切换，因为Spring AOP 同时支持 CGLIB、ASPECTJ、JDK动态代理。
{: id="20210330211656-hjakx6j"}

- {: id="20210330211656-im30839"}如果目标对象的实现类实现了接口，Spring AOP 将会采用 JDK 动态代理来生成 AOP 代理类；
  {: id="20210330211656-xshyu6w"}
- {: id="20210330211656-8g0pox0"}如果目标对象的实现类没有实现接口，Spring AOP 将会采用 CGLIB 来生成 AOP 代理类——不过这个选择过程对开发者完全透明、开发者也无需关心。
  {: id="20210330211656-4icvcwt"}
{: id="20210330211656-7ffbjn7"}

推荐阅读：
{: id="20210330211656-fyyo1b2"}

- {: id="20210330211656-85dy0iq"}[静态代理、JDK动态代理、CGLIB动态代理讲解](http://www.cnblogs.com/puyangsky/p/6218925.html) ：我们知道AOP思想的实现一般都是基于 **代理模式** ，所以在看下面的文章之前建议先了解一下静态代理以及JDK动态代理、CGLIB动态代理的实现方式。
  {: id="20210330211656-iehkxb2"}
- {: id="20210330211656-3sbm80y"}[Spring AOP 入门](https://juejin.im/post/5aa7818af265da23844040c6) ：带你入门的一篇文章。这篇文章主要介绍了AOP中的基本概念：5种类型的通知（Before，After，After-returning，After-throwing，Around）；Spring中对AOP的支持：AOP思想的实现一般都是基于代理模式，在Java中一般采用JDK动态代理模式，Spring AOP 同时支持 CGLIB、ASPECTJ、JDK动态代理，
  {: id="20210330211656-it7mwtq"}
- {: id="20210330211656-f9ifvb7"}[Spring AOP 基于AspectJ注解如何实现AOP](https://juejin.im/post/5a55af9e518825734d14813f) ： **AspectJ是一个AOP框架，它能够对java代码进行AOP编译（一般在编译期进行），让java代码具有AspectJ的AOP功能（当然需要特殊的编译器）**，可以这样说AspectJ是目前实现AOP框架中最成熟，功能最丰富的语言，更幸运的是，AspectJ与java程序完全兼容，几乎是无缝关联，因此对于有java编程基础的工程师，上手和使用都非常容易。Spring注意到AspectJ在AOP的实现方式上依赖于特殊编译器(ajc编译器)，因此Spring很机智回避了这点，转向采用动态代理技术的实现原理来构建Spring AOP的内部机制（动态织入），这是与AspectJ（静态织入）最根本的区别。**Spring 只是使用了与 AspectJ 5 一样的注解，但仍然没有使用 AspectJ 的编译器，底层依是动态代理技术的实现，因此并不依赖于 AspectJ 的编译器**。 Spring AOP虽然是使用了那一套注解，其实实现AOP的底层是使用了动态代理(JDK或者CGLib)来动态植入。至于AspectJ的静态植入，不是本文重点，所以只提一提。
  {: id="20210330211656-e19cyzf"}
- {: id="20210330211656-vgndtk0"}[探秘Spring AOP（慕课网视频，很不错）](https://www.imooc.com/learn/869):慕课网视频，讲解的很不错，详细且深入
  {: id="20210330211656-93ohh4e"}
- {: id="20210330211656-faqceks"}[spring源码剖析（六）AOP实现原理剖析](https://blog.csdn.net/fighterandknight/article/details/51209822) :通过源码分析Spring AOP的原理
  {: id="20210330211656-705515y"}
{: id="20210330211656-7b0gnim"}

### IOC
{: id="20210330211656-7epnqy1"}

- {: id="20210330211656-ak6ouyb"}[[Spring框架]Spring IOC的原理及详解。](https://www.cnblogs.com/wang-meng/p/5597490.html)
  {: id="20210330211656-cfw97b4"}
- {: id="20210330211656-0yh50cj"}[Spring IOC核心源码学习](https://yikun.github.io/2015/05/29/Spring-IOC核心源码学习/) :比较简短，推荐阅读。
  {: id="20210330211656-oqwojky"}
- {: id="20210330211656-qaycyob"}[Spring IOC 容器源码分析](https://javadoop.com/post/spring-ioc) :强烈推荐，内容详尽，而且便于阅读。
  {: id="20210330211656-x9t3av4"}
- {: id="20210330211656-o6akdp9"}[Bean初始化过程](https://www.qzztf.com/2019/08/21/Bean%E5%88%9D%E5%A7%8B%E5%8C%96/#Bean-%E5%AE%9E%E4%BE%8B%E5%8C%96)
  {: id="20210330211656-lsxno48"}
{: id="20210330211656-j12dwa8"}

## Spring事务管理
{: id="20210330211656-oiug7lj"}

- {: id="20210330211656-s6w5tez"}[可能是最漂亮的Spring事务管理详解](https://juejin.im/post/5b00c52ef265da0b95276091)
  {: id="20210330211656-c8qswad"}
- {: id="20210330211656-ed7qraz"}[Spring编程式和声明式事务实例讲解](https://juejin.im/post/5b010f27518825426539ba38)
  {: id="20210330211656-tj7vd7l"}
{: id="20210330211656-zxwtpxr"}

### Spring单例与线程安全
{: id="20210330211656-xkh4fk0"}

- {: id="20210330211656-6do2pi7"}[Spring框架中的单例模式（源码解读）](http://www.cnblogs.com/chengxuyuanzhilu/p/6404991.html):单例模式是一种常用的软件设计模式。通过单例模式可以保证系统中一个类只有一个实例。spring依赖注入时，使用了 多重判断加锁 的单例模式。
  {: id="20210330211656-id2na0l"}
{: id="20210330211656-6us4irx"}

### Spring源码阅读
{: id="20210330211656-li5f4q6"}

阅读源码不仅可以加深我们对Spring设计思想的理解，提高自己的编码水平，还可以让自己在面试中如鱼得水。下面的是Github上的一个开源的Spring源码阅读，大家有时间可以看一下，当然你如果有时间也可以自己慢慢研究源码。
{: id="20210330211656-65cszpq"}

- {: id="20210330211656-ss8r3m1"}[spring-core](https://github.com/seaswalker/Spring/blob/master/note/Spring.md)
  {: id="20210330211656-zcy35ng"}
- {: id="20210330211656-3clq7ct"}[spring-aop](https://github.com/seaswalker/Spring/blob/master/note/spring-aop.md)
  {: id="20210330211656-m22g1ep"}
- {: id="20210330211656-5klexve"}[spring-context](https://github.com/seaswalker/Spring/blob/master/note/spring-context.md)
  {: id="20210330211656-zxc23nl"}
- {: id="20210330211656-3rs7odi"}[spring-task](https://github.com/seaswalker/Spring/blob/master/note/spring-task.md)
  {: id="20210330211656-kxwk8cx"}
- {: id="20210330211656-wem7dx5"}[spring-transaction](https://github.com/seaswalker/Spring/blob/master/note/spring-transaction.md)
  {: id="20210330211656-v7ufveg"}
- {: id="20210330211656-7mw229p"}[spring-mvc](https://github.com/seaswalker/Spring/blob/master/note/spring-mvc.md)
  {: id="20210330211656-8uu5eo8"}
- {: id="20210330211656-i6gw60r"}[guava-cache](https://github.com/seaswalker/Spring/blob/master/note/guava-cache.md)
  {: id="20210330211656-8mpoifd"}
{: id="20210330211656-nkz0j49"}


{: id="20210330211656-fkljnfi" type="doc"}
