### 文章目录
{: id="20210330211656-tsv92kj"}

<!-- TOC -->

- {: id="20210330211656-m0cz42r"}[文章目录](#%e6%96%87%e7%ab%a0%e7%9b%ae%e5%bd%95)
  {: id="20210330211656-5fp3z6q"}
- {: id="20210330211656-x1p59sp"}[0.前言](#0%e5%89%8d%e8%a8%80)
  {: id="20210330211656-k0yqio7"}
- {: id="20210330211656-ow8vi6q"}[1. `@SpringBootApplication`](#1-springbootapplication)
  {: id="20210330211656-j1du5n1"}
- {: id="20210330211656-vgvhi9l"}[2. Spring Bean 相关](#2-spring-bean-%e7%9b%b8%e5%85%b3)
  {: id="20210330211656-z8w5c9z"}
  - {: id="20210330211656-hwniecy"}[2.1. `@Autowired`](#21-autowired)
    {: id="20210330211656-n1cww38"}
  - {: id="20210330211656-jy34qib"}[2.2. `@Component`,`@Repository`,`@Service`, `@Controller`](#22-componentrepositoryservice-controller)
    {: id="20210330211656-u6np9jd"}
  - {: id="20210330211656-pw8gzbr"}[2.3. `@RestController`](#23-restcontroller)
    {: id="20210330211656-kajt977"}
  - {: id="20210330211656-o9q66k2"}[2.4. `@Scope`](#24-scope)
    {: id="20210330211656-zkw7791"}
  - {: id="20210330211656-jwvhrqm"}[2.5. `@Configuration`](#25-configuration)
    {: id="20210330211656-tvfywbp"}
  {: id="20210330211656-x547clc"}
- {: id="20210330211656-cad7to3"}[3. 处理常见的 HTTP 请求类型](#3-%e5%a4%84%e7%90%86%e5%b8%b8%e8%a7%81%e7%9a%84-http-%e8%af%b7%e6%b1%82%e7%b1%bb%e5%9e%8b)
  {: id="20210330211656-6j5mlj6"}
  - {: id="20210330211656-qexmq7f"}[3.1. GET 请求](#31-get-%e8%af%b7%e6%b1%82)
    {: id="20210330211656-l0qjpj0"}
  - {: id="20210330211656-j7ybdvk"}[3.2. POST 请求](#32-post-%e8%af%b7%e6%b1%82)
    {: id="20210330211656-kwkbfcw"}
  - {: id="20210330211656-rjv8t52"}[3.3. PUT 请求](#33-put-%e8%af%b7%e6%b1%82)
    {: id="20210330211656-lg69aqw"}
  - {: id="20210330211656-aeqyja4"}[3.4. **DELETE 请求**](#34-delete-%e8%af%b7%e6%b1%82)
    {: id="20210330211656-71ddk34"}
  - {: id="20210330211656-i2pxik1"}[3.5. **PATCH 请求**](#35-patch-%e8%af%b7%e6%b1%82)
    {: id="20210330211656-vxj3jej"}
  {: id="20210330211656-je9jk0y"}
- {: id="20210330211656-dlzo49r"}[4. 前后端传值](#4-%e5%89%8d%e5%90%8e%e7%ab%af%e4%bc%a0%e5%80%bc)
  {: id="20210330211656-0g4ff9h"}
  - {: id="20210330211656-o3e6r4l"}[4.1. `@PathVariable` 和 `@RequestParam`](#41-pathvariable-%e5%92%8c-requestparam)
    {: id="20210330211656-61dv8gg"}
  - {: id="20210330211656-60j2vdp"}[4.2. `@RequestBody`](#42-requestbody)
    {: id="20210330211656-hknwxaf"}
  {: id="20210330211656-3j8lqli"}
- {: id="20210330211656-dfob9ta"}[5. 读取配置信息](#5-%e8%af%bb%e5%8f%96%e9%85%8d%e7%bd%ae%e4%bf%a1%e6%81%af)
  {: id="20210330211656-r93c9mo"}
  - {: id="20210330211656-bw6d3yq"}[5.1. `@value`(常用)](#51-value%e5%b8%b8%e7%94%a8)
    {: id="20210330211656-ogdfov1"}
  - {: id="20210330211656-u4engfq"}[5.2. `@ConfigurationProperties`(常用)](#52-configurationproperties%e5%b8%b8%e7%94%a8)
    {: id="20210330211656-iqp2bgg"}
  - {: id="20210330211656-lxo6yb3"}[5.3. `PropertySource`（不常用）](#53-propertysource%e4%b8%8d%e5%b8%b8%e7%94%a8)
    {: id="20210330211656-mqos943"}
  {: id="20210330211656-r3zob4u"}
- {: id="20210330211656-hquzlep"}[6. 参数校验](#6-%e5%8f%82%e6%95%b0%e6%a0%a1%e9%aa%8c)
  {: id="20210330211656-jwkozy8"}
  - {: id="20210330211656-fvwob1y"}[6.1. 一些常用的字段验证的注解](#61-%e4%b8%80%e4%ba%9b%e5%b8%b8%e7%94%a8%e7%9a%84%e5%ad%97%e6%ae%b5%e9%aa%8c%e8%af%81%e7%9a%84%e6%b3%a8%e8%a7%a3)
    {: id="20210330211656-rs2bz9x"}
  - {: id="20210330211656-bxei7se"}[6.2. 验证请求体(RequestBody)](#62-%e9%aa%8c%e8%af%81%e8%af%b7%e6%b1%82%e4%bd%93requestbody)
    {: id="20210330211656-yir668p"}
  - {: id="20210330211656-kblsbtk"}[6.3. 验证请求参数(Path Variables 和 Request Parameters)](#63-%e9%aa%8c%e8%af%81%e8%af%b7%e6%b1%82%e5%8f%82%e6%95%b0path-variables-%e5%92%8c-request-parameters)
    {: id="20210330211656-hph1hac"}
  {: id="20210330211656-3l5cmq6"}
- {: id="20210330211656-vm632lj"}[7. 全局处理 Controller 层异常](#7-%e5%85%a8%e5%b1%80%e5%a4%84%e7%90%86-controller-%e5%b1%82%e5%bc%82%e5%b8%b8)
  {: id="20210330211656-9v2r0t8"}
- {: id="20210330211656-d2pyx0x"}[8. JPA 相关](#8-jpa-%e7%9b%b8%e5%85%b3)
  {: id="20210330211656-oc7ylge"}
  - {: id="20210330211656-zqgdwgo"}[8.1. 创建表](#81-%e5%88%9b%e5%bb%ba%e8%a1%a8)
    {: id="20210330211656-14l6lkm"}
  - {: id="20210330211656-l6eo8h2"}[8.2. 创建主键](#82-%e5%88%9b%e5%bb%ba%e4%b8%bb%e9%94%ae)
    {: id="20210330211656-v7s4ic5"}
  - {: id="20210330211656-riorodn"}[8.3. 设置字段类型](#83-%e8%ae%be%e7%bd%ae%e5%ad%97%e6%ae%b5%e7%b1%bb%e5%9e%8b)
    {: id="20210330211656-zzoe9ht"}
  - {: id="20210330211656-jaqgwdr"}[8.4. 指定不持久化特定字段](#84-%e6%8c%87%e5%ae%9a%e4%b8%8d%e6%8c%81%e4%b9%85%e5%8c%96%e7%89%b9%e5%ae%9a%e5%ad%97%e6%ae%b5)
    {: id="20210330211656-smfvbw3"}
  - {: id="20210330211656-0y7iqgu"}[8.5. 声明大字段](#85-%e5%a3%b0%e6%98%8e%e5%a4%a7%e5%ad%97%e6%ae%b5)
    {: id="20210330211656-euj96qe"}
  - {: id="20210330211656-r1ju9q9"}[8.6. 创建枚举类型的字段](#86-%e5%88%9b%e5%bb%ba%e6%9e%9a%e4%b8%be%e7%b1%bb%e5%9e%8b%e7%9a%84%e5%ad%97%e6%ae%b5)
    {: id="20210330211656-c29i10r"}
  - {: id="20210330211656-vm5vkxy"}[8.7. 增加审计功能](#87-%e5%a2%9e%e5%8a%a0%e5%ae%a1%e8%ae%a1%e5%8a%9f%e8%83%bd)
    {: id="20210330211656-xybac9l"}
  - {: id="20210330211656-6haz9kx"}[8.8. 删除/修改数据](#88-%e5%88%a0%e9%99%a4%e4%bf%ae%e6%94%b9%e6%95%b0%e6%8d%ae)
    {: id="20210330211656-ztwbe8s"}
  - {: id="20210330211656-jcqjbsw"}[8.9. 关联关系](#89-%e5%85%b3%e8%81%94%e5%85%b3%e7%b3%bb)
    {: id="20210330211656-4sn03gt"}
  {: id="20210330211656-jxm3e53"}
- {: id="20210330211656-1o0je0x"}[9. 事务 `@Transactional`](#9-%e4%ba%8b%e5%8a%a1-transactional)
  {: id="20210330211656-83qgvje"}
- {: id="20210330211656-f2ziw59"}[10. json 数据处理](#10-json-%e6%95%b0%e6%8d%ae%e5%a4%84%e7%90%86)
  {: id="20210330211656-uy3lbgj"}
  - {: id="20210330211656-dhpu0x7"}[10.1. 过滤 json 数据](#101-%e8%bf%87%e6%bb%a4-json-%e6%95%b0%e6%8d%ae)
    {: id="20210330211656-otfnyjl"}
  - {: id="20210330211656-t3wtzs8"}[10.2. 格式化 json 数据](#102-%e6%a0%bc%e5%bc%8f%e5%8c%96-json-%e6%95%b0%e6%8d%ae)
    {: id="20210330211656-1dam6g4"}
  - {: id="20210330211656-76rj6pi"}[10.3. 扁平化对象](#103-%e6%89%81%e5%b9%b3%e5%8c%96%e5%af%b9%e8%b1%a1)
    {: id="20210330211656-4nvtjgi"}
  {: id="20210330211656-mbmbdgp"}
- {: id="20210330211656-9bqszih"}[11. 测试相关](#11-%e6%b5%8b%e8%af%95%e7%9b%b8%e5%85%b3)
  {: id="20210330211656-r54zec9"}
{: id="20210330211656-p08gtym"}

<!-- /TOC -->

### 0.前言
{: id="20210330211656-ezbozbt"}

_大家好，我是 Guide 哥！这是我的 221 篇优质原创文章。如需转载，请在文首注明地址，蟹蟹！_
{: id="20210330211656-zl1j5hj"}

本文已经收录进我的 75K Star 的 Java 开源项目 JavaGuide：[https://github.com/Snailclimb/JavaGuide](https://github.com/Snailclimb/JavaGuide)。
{: id="20210330211656-yyr68hv"}

可以毫不夸张地说，这篇文章介绍的 Spring/SpringBoot 常用注解基本已经涵盖你工作中遇到的大部分常用的场景。对于每一个注解我都说了具体用法，掌握搞懂，使用 SpringBoot 来开发项目基本没啥大问题了！
{: id="20210330211656-mft16ep"}

**为什么要写这篇文章？**
{: id="20210330211656-qrf1u8r"}

最近看到网上有一篇关于 SpringBoot 常用注解的文章被转载的比较多，我看了文章内容之后属实觉得质量有点低，并且有点会误导没有太多实际使用经验的人（这些人又占据了大多数）。所以，自己索性花了大概 两天时间简单总结一下了。
{: id="20210330211656-xb2ptqy"}

**因为我个人的能力和精力有限，如果有任何不对或者需要完善的地方，请帮忙指出！Guide 哥感激不尽！**
{: id="20210330211656-xbo9l65"}

### 1. `@SpringBootApplication`
{: id="20210330211656-6v6ljdk"}

这里先单独拎出`@SpringBootApplication` 注解说一下，虽然我们一般不会主动去使用它。
{: id="20210330211656-3u0u3ym"}

_Guide 哥：这个注解是 Spring Boot 项目的基石，创建 SpringBoot 项目之后会默认在主类加上。_
{: id="20210330211656-fa3epf1"}

```java
@SpringBootApplication
public class SpringSecurityJwtGuideApplication {
      public static void main(java.lang.String[] args) {
        SpringApplication.run(SpringSecurityJwtGuideApplication.class, args);
    }
}
```
{: id="20210330211656-ks4t38c"}

我们可以把 `@SpringBootApplication`看作是 `@Configuration`、`@EnableAutoConfiguration`、`@ComponentScan` 注解的集合。
{: id="20210330211656-nddap00"}

```java
package org.springframework.boot.autoconfigure;
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = {
		@Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {
   ......
}

package org.springframework.boot;
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Configuration
public @interface SpringBootConfiguration {

}
```
{: id="20210330211656-6c16bvm"}

根据 SpringBoot 官网，这三个注解的作用分别是：
{: id="20210330211656-fqyp04v"}

- {: id="20210330211656-5m93dfi"}`@EnableAutoConfiguration`：启用 SpringBoot 的自动配置机制
  {: id="20210330211656-t5rjawd"}
- {: id="20210330211656-mdjok3m"}`@ComponentScan`： 扫描被`@Component` (`@Service`,`@Controller`)注解的 bean，注解默认会扫描该类所在的包下所有的类。
  {: id="20210330211656-r9yrnl8"}
- {: id="20210330211656-220wtob"}`@Configuration`：允许在 Spring 上下文中注册额外的 bean 或导入其他配置类
  {: id="20210330211656-vjdt21j"}
{: id="20210330211656-zdegrko"}

### 2. Spring Bean 相关
{: id="20210330211656-9mr3na5"}

#### 2.1. `@Autowired`
{: id="20210330211656-0oja16m"}

自动导入对象到类中，被注入进的类同样要被 Spring 容器管理比如：Service 类注入到 Controller 类中。
{: id="20210330211656-9r5n5q5"}

```java
@Service
public class UserService {
  ......
}

@RestController
@RequestMapping("/users")
public class UserController {
   @Autowired
   private UserService userService;
   ......
}
```
{: id="20210330211656-f3c76mp"}

#### 2.2. `@Component`,`@Repository`,`@Service`, `@Controller`
{: id="20210330211656-4xqmtl4"}

我们一般使用 `@Autowired` 注解让 Spring 容器帮我们自动装配 bean。要想把类标识成可用于 `@Autowired` 注解自动装配的 bean 的类,可以采用以下注解实现：
{: id="20210330211656-go52rfo"}

- {: id="20210330211656-ov7r7t3"}`@Component` ：通用的注解，可标注任意类为 `Spring` 组件。如果一个 Bean 不知道属于哪个层，可以使用`@Component` 注解标注。
  {: id="20210330211656-n19s4we"}
- {: id="20210330211656-fnq1sqj"}`@Repository` : 对应持久层即 Dao 层，主要用于数据库相关操作。
  {: id="20210330211656-29b7obd"}
- {: id="20210330211656-ukfulpk"}`@Service` : 对应服务层，主要涉及一些复杂的逻辑，需要用到 Dao 层。
  {: id="20210330211656-27y4vkc"}
- {: id="20210330211656-14k7vjs"}`@Controller` : 对应 Spring MVC 控制层，主要用于接受用户请求并调用 Service 层返回数据给前端页面。
  {: id="20210330211656-k9fbnfo"}
{: id="20210330211656-xp18qkt"}

#### 2.3. `@RestController`
{: id="20210330211656-za38irt"}

`@RestController`注解是`@Controller和`@`ResponseBody`的合集,表示这是个控制器 bean,并且是将函数的返回值直 接填入 HTTP 响应体中,是 REST 风格的控制器。
{: id="20210330211656-46yfr2r"}

_Guide 哥：现在都是前后端分离，说实话我已经很久没有用过`@Controller`。如果你的项目太老了的话，就当我没说。_
{: id="20210330211656-ub44hxf"}

单独使用 `@Controller` 不加 `@ResponseBody`的话一般使用在要返回一个视图的情况，这种情况属于比较传统的 Spring MVC 的应用，对应于前后端不分离的情况。`@Controller` +`@ResponseBody` 返回 JSON 或 XML 形式数据
{: id="20210330211656-f9ulffn"}

关于`@RestController` 和 `@Controller`的对比，请看这篇文章：[@RestController vs @Controller](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247485544&idx=1&sn=3cc95b88979e28fe3bfe539eb421c6d8&chksm=cea247a3f9d5ceb5e324ff4b8697adc3e828ecf71a3468445e70221cce768d1e722085359907&token=1725092312&lang=zh_CN#rd)。
{: id="20210330211656-qxro6qr"}

#### 2.4. `@Scope`
{: id="20210330211656-q6d80fn"}

声明 Spring Bean 的作用域，使用方法:
{: id="20210330211656-q97xoer"}

```java
@Bean
@Scope("singleton")
public Person personSingleton() {
    return new Person();
}
```
{: id="20210330211656-00taic9"}

**四种常见的 Spring Bean 的作用域：**
{: id="20210330211656-kglpfrp"}

- {: id="20210330211656-rv0r0ip"}singleton : 唯一 bean 实例，Spring 中的 bean 默认都是单例的。
  {: id="20210330211656-yk7270s"}
- {: id="20210330211656-n42esge"}prototype : 每次请求都会创建一个新的 bean 实例。
  {: id="20210330211656-1w4ya5v"}
- {: id="20210330211656-75ecpnz"}request : 每一次 HTTP 请求都会产生一个新的 bean，该 bean 仅在当前 HTTP request 内有效。
  {: id="20210330211656-twuyba3"}
- {: id="20210330211656-l7b2898"}session : 每一次 HTTP 请求都会产生一个新的 bean，该 bean 仅在当前 HTTP session 内有效。
  {: id="20210330211656-pivalem"}
{: id="20210330211656-vlddclg"}

#### 2.5. `@Configuration`
{: id="20210330211656-kmvbdjs"}

一般用来声明配置类，可以使用 `@Component`注解替代，不过使用`@Configuration`注解声明配置类更加语义化。
{: id="20210330211656-mv1mrg8"}

```java
@Configuration
public class AppConfig {
    @Bean
    public TransferService transferService() {
        return new TransferServiceImpl();
    }

}
```
{: id="20210330211656-zolps5r"}

### 3. 处理常见的 HTTP 请求类型
{: id="20210330211656-sz93fqt"}

**5 种常见的请求类型:**
{: id="20210330211656-e7b408q"}

- {: id="20210330211656-0xl19pg"}**GET** ：请求从服务器获取特定资源。举个例子：`GET /users`（获取所有学生）
  {: id="20210330211656-ghk2aze"}
- {: id="20210330211656-zmef9nn"}**POST** ：在服务器上创建一个新的资源。举个例子：`POST /users`（创建学生）
  {: id="20210330211656-efzssbm"}
- {: id="20210330211656-mc4ubz8"}**PUT** ：更新服务器上的资源（客户端提供更新后的整个资源）。举个例子：`PUT /users/12`（更新编号为 12 的学生）
  {: id="20210330211656-ir1nxst"}
- {: id="20210330211656-45nv5up"}**DELETE** ：从服务器删除特定的资源。举个例子：`DELETE /users/12`（删除编号为 12 的学生）
  {: id="20210330211656-i9pzb6i"}
- {: id="20210330211656-st7w1pm"}**PATCH** ：更新服务器上的资源（客户端提供更改的属性，可以看做作是部分更新），使用的比较少，这里就不举例子了。
  {: id="20210330211656-pm3l0au"}
{: id="20210330211656-fkukd7s"}

#### 3.1. GET 请求
{: id="20210330211656-3qdziq2"}

`@GetMapping("users")` 等价于`@RequestMapping(value="/users",method=RequestMethod.GET)`
{: id="20210330211656-plf3whf"}

```java
@GetMapping("/users")
public ResponseEntity<List<User>> getAllUsers() {
 return userRepository.findAll();
}
```
{: id="20210330211656-f5b09pa"}

#### 3.2. POST 请求
{: id="20210330211656-2pejt7l"}

`@PostMapping("users")` 等价于`@RequestMapping(value="/users",method=RequestMethod.POST)`
{: id="20210330211656-uqj2wog"}

关于`@RequestBody`注解的使用，在下面的“前后端传值”这块会讲到。
{: id="20210330211656-zl6xp4c"}

```java
@PostMapping("/users")
public ResponseEntity<User> createUser(@Valid @RequestBody UserCreateRequest userCreateRequest) {
 return userRespository.save(user);
}
```
{: id="20210330211656-zp7sxal"}

#### 3.3. PUT 请求
{: id="20210330211656-zq7tfy1"}

`@PutMapping("/users/{userId}")` 等价于`@RequestMapping(value="/users/{userId}",method=RequestMethod.PUT)`
{: id="20210330211656-b74w04b"}

```java
@PutMapping("/users/{userId}")
public ResponseEntity<User> updateUser(@PathVariable(value = "userId") Long userId,
  @Valid @RequestBody UserUpdateRequest userUpdateRequest) {
  ......
}
```
{: id="20210330211656-nk7d5e5"}

#### 3.4. **DELETE 请求**
{: id="20210330211656-zkl81ud"}

`@DeleteMapping("/users/{userId}")`等价于`@RequestMapping(value="/users/{userId}",method=RequestMethod.DELETE)`
{: id="20210330211656-vbg7bzl"}

```java
@DeleteMapping("/users/{userId}")
public ResponseEntity deleteUser(@PathVariable(value = "userId") Long userId){
  ......
}
```
{: id="20210330211656-jkair7s"}

#### 3.5. **PATCH 请求**
{: id="20210330211656-rhms6vq"}

一般实际项目中，我们都是 PUT 不够用了之后才用 PATCH 请求去更新数据。
{: id="20210330211656-87u7h5w"}

```java
  @PatchMapping("/profile")
  public ResponseEntity updateStudent(@RequestBody StudentUpdateRequest studentUpdateRequest) {
        studentRepository.updateDetail(studentUpdateRequest);
        return ResponseEntity.ok().build();
    }
```
{: id="20210330211656-huamvbf"}

### 4. 前后端传值
{: id="20210330211656-6lo0q59"}

**掌握前后端传值的正确姿势，是你开始 CRUD 的第一步！**
{: id="20210330211656-6mlws10"}

#### 4.1. `@PathVariable` 和 `@RequestParam`
{: id="20210330211656-o8fr2wg"}

`@PathVariable`用于获取路径参数，`@RequestParam`用于获取查询参数。
{: id="20210330211656-4bcvkyg"}

举个简单的例子：
{: id="20210330211656-bupzhjs"}

```java
@GetMapping("/klasses/{klassId}/teachers")
public List<Teacher> getKlassRelatedTeachers(
         @PathVariable("klassId") Long klassId,
         @RequestParam(value = "type", required = false) String type ) {
...
}
```
{: id="20210330211656-qf57nuh"}

如果我们请求的 url 是：`/klasses/{123456}/teachers?type=web`
{: id="20210330211656-z4cgdfd"}

那么我们服务获取到的数据就是：`klassId=123456,type=web`。
{: id="20210330211656-x2vtnb0"}

#### 4.2. `@RequestBody`
{: id="20210330211656-01rgpvq"}

用于读取 Request 请求（可能是 POST,PUT,DELETE,GET 请求）的 body 部分并且**Content-Type 为 application/json** 格式的数据，接收到数据之后会自动将数据绑定到 Java 对象上去。系统会使用`HttpMessageConverter`或者自定义的`HttpMessageConverter`将请求的 body 中的 json 字符串转换为 java 对象。
{: id="20210330211656-vnxktjp"}

我用一个简单的例子来给演示一下基本使用！
{: id="20210330211656-pivowus"}

我们有一个注册的接口：
{: id="20210330211656-yudxb63"}

```java
@PostMapping("/sign-up")
public ResponseEntity signUp(@RequestBody @Valid UserRegisterRequest userRegisterRequest) {
  userService.save(userRegisterRequest);
  return ResponseEntity.ok().build();
}
```
{: id="20210330211656-w4extxs"}

`UserRegisterRequest`对象：
{: id="20210330211656-ro6bi7s"}

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class UserRegisterRequest {
    @NotBlank
    private String userName;
    @NotBlank
    private String password;
    @NotBlank
    private String fullName;
}
```
{: id="20210330211656-z0yc30k"}

我们发送 post 请求到这个接口，并且 body 携带 JSON 数据：
{: id="20210330211656-djia37o"}

```json
{"userName":"coder","fullName":"shuangkou","password":"123456"}
```
{: id="20210330211656-pwg6ftw"}

这样我们的后端就可以直接把 json 格式的数据映射到我们的 `UserRegisterRequest` 类上。
{: id="20210330211656-gejmddj"}

![](images/spring-annotations/@RequestBody.png)
{: id="20210330211656-8qvakoj"}

👉 需要注意的是：**一个请求方法只可以有一个`@RequestBody`，但是可以有多个`@RequestParam`和`@PathVariable`**。 如果你的方法必须要用两个 `@RequestBody`来接受数据的话，大概率是你的数据库设计或者系统设计出问题了！
{: id="20210330211656-vrx0uos"}

### 5. 读取配置信息
{: id="20210330211656-1ye7tpq"}

**很多时候我们需要将一些常用的配置信息比如阿里云 oss、发送短信、微信认证的相关配置信息等等放到配置文件中。**
{: id="20210330211656-41aytu0"}

**下面我们来看一下 Spring 为我们提供了哪些方式帮助我们从配置文件中读取这些配置信息。**
{: id="20210330211656-i1n1oeb"}

我们的数据源`application.yml`内容如下：：
{: id="20210330211656-h6owt3o"}

```yaml
wuhan2020: 2020年初武汉爆发了新型冠状病毒，疫情严重，但是，我相信一切都会过去！武汉加油！中国加油！

my-profile:
  name: Guide哥
  email: koushuangbwcx@163.com

library:
  location: 湖北武汉加油中国加油
  books:
    - name: 天才基本法
      description: 二十二岁的林朝夕在父亲确诊阿尔茨海默病这天，得知自己暗恋多年的校园男神裴之即将出国深造的消息——对方考取的学校，恰是父亲当年为她放弃的那所。
    - name: 时间的秩序
      description: 为什么我们记得过去，而非未来？时间“流逝”意味着什么？是我们存在于时间之内，还是时间存在于我们之中？卡洛·罗韦利用诗意的文字，邀请我们思考这一亘古难题——时间的本质。
    - name: 了不起的我
      description: 如何养成一个新习惯？如何让心智变得更成熟？如何拥有高质量的关系？ 如何走出人生的艰难时刻？
```
{: id="20210330211656-mx4nmr0"}

#### 5.1. `@value`(常用)
{: id="20210330211656-55552ua"}

使用 `@Value("${property}")` 读取比较简单的配置信息：
{: id="20210330211656-v9a5ki3"}

```java
@Value("${wuhan2020}")
String wuhan2020;
```
{: id="20210330211656-o9d1ehz"}

#### 5.2. `@ConfigurationProperties`(常用)
{: id="20210330211656-il2owhv"}

通过`@ConfigurationProperties`读取配置信息并与 bean 绑定。
{: id="20210330211656-q18upfi"}

```java
@Component
@ConfigurationProperties(prefix = "library")
class LibraryProperties {
    @NotEmpty
    private String location;
    private List<Book> books;

    @Setter
    @Getter
    @ToString
    static class Book {
        String name;
        String description;
    }
  省略getter/setter
  ......
}
```
{: id="20210330211656-omy4134"}

你可以像使用普通的 Spring bean 一样，将其注入到类中使用。
{: id="20210330211656-vulnfnm"}

#### 5.3. `PropertySource`（不常用）
{: id="20210330211656-kt8z8v4"}

`@PropertySource`读取指定 properties 文件
{: id="20210330211656-nizkgfn"}

```java
@Component
@PropertySource("classpath:website.properties")

class WebSite {
    @Value("${url}")
    private String url;

  省略getter/setter
  ......
}
```
{: id="20210330211656-ea9f1fe"}

更多内容请查看我的这篇文章：《[10 分钟搞定 SpringBoot 如何优雅读取配置文件？](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247486181&idx=2&sn=10db0ae64ef501f96a5b0dbc4bd78786&chksm=cea2452ef9d5cc384678e456427328600971180a77e40c13936b19369672ca3e342c26e92b50&token=816772476&lang=zh_CN#rd)》 。
{: id="20210330211656-1tojmym"}

### 6. 参数校验
{: id="20210330211656-1huoiun"}

**数据的校验的重要性就不用说了，即使在前端对数据进行校验的情况下，我们还是要对传入后端的数据再进行一遍校验，避免用户绕过浏览器直接通过一些 HTTP 工具直接向后端请求一些违法数据。**
{: id="20210330211656-31pocq5"}

**JSR(Java Specification Requests）** 是一套 JavaBean 参数校验的标准，它定义了很多常用的校验注解，我们可以直接将这些注解加在我们 JavaBean 的属性上面，这样就可以在需要校验的时候进行校验了，非常方便！
{: id="20210330211656-k7meq63"}

校验的时候我们实际用的是 **Hibernate Validator** 框架。Hibernate Validator 是 Hibernate 团队最初的数据校验框架，Hibernate Validator 4.x 是 Bean Validation 1.0（JSR 303）的参考实现，Hibernate Validator 5.x 是 Bean Validation 1.1（JSR 349）的参考实现，目前最新版的 Hibernate Validator 6.x 是 Bean Validation 2.0（JSR 380）的参考实现。
{: id="20210330211656-3y7slc4"}

SpringBoot 项目的 spring-boot-starter-web 依赖中已经有 hibernate-validator 包，不需要引用相关依赖。如下图所示（通过 idea 插件—Maven Helper 生成）：
{: id="20210330211656-1eihm4f"}

![](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/2021/03/c7bacd12-1c1a-4e41-aaaf-4cad840fc073.png)
{: id="20210330211656-w6cimpo"}

非 SpringBoot 项目需要自行引入相关依赖包，这里不多做讲解，具体可以查看我的这篇文章：《[如何在 Spring/Spring Boot 中做参数校验？你需要了解的都在这里！](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247485783&idx=1&sn=a407f3b75efa17c643407daa7fb2acd6&chksm=cea2469cf9d5cf8afbcd0a8a1c9cc4294d6805b8e01bee6f76bb2884c5bc15478e91459def49&token=292197051&lang=zh_CN#rd)》。
{: id="20210330211656-jt7i47f"}

👉 需要注意的是： **所有的注解，推荐使用 JSR 注解，即`javax.validation.constraints`，而不是`org.hibernate.validator.constraints`**
{: id="20210330211656-cs31kbq"}

#### 6.1. 一些常用的字段验证的注解
{: id="20210330211656-uarx54h"}

- {: id="20210330211656-e9bthl6"}`@NotEmpty` 被注释的字符串的不能为 null 也不能为空
  {: id="20210330211656-7g4anlc"}
- {: id="20210330211656-x2t0cij"}`@NotBlank` 被注释的字符串非 null，并且必须包含一个非空白字符
  {: id="20210330211656-p6p9nvs"}
- {: id="20210330211656-zhwncf3"}`@Null` 被注释的元素必须为 null
  {: id="20210330211656-5i58e54"}
- {: id="20210330211656-5875e4z"}`@NotNull` 被注释的元素必须不为 null
  {: id="20210330211656-pahtpaf"}
- {: id="20210330211656-qhd68a2"}`@AssertTrue` 被注释的元素必须为 true
  {: id="20210330211656-gp9esm0"}
- {: id="20210330211656-mb7nhto"}`@AssertFalse` 被注释的元素必须为 false
  {: id="20210330211656-fi536tr"}
- {: id="20210330211656-rfsjab2"}`@Pattern(regex=,flag=)`被注释的元素必须符合指定的正则表达式
  {: id="20210330211656-5rkg0ei"}
- {: id="20210330211656-zwncbr3"}`@Email` 被注释的元素必须是 Email 格式。
  {: id="20210330211656-jh6uir7"}
- {: id="20210330211656-gh54nvo"}`@Min(value)`被注释的元素必须是一个数字，其值必须大于等于指定的最小值
  {: id="20210330211656-oy48itg"}
- {: id="20210330211656-6zr5h0g"}`@Max(value)`被注释的元素必须是一个数字，其值必须小于等于指定的最大值
  {: id="20210330211656-9gyxmhm"}
- {: id="20210330211656-aur93xz"}`@DecimalMin(value)`被注释的元素必须是一个数字，其值必须大于等于指定的最小值
  {: id="20210330211656-tmxdwlm"}
- {: id="20210330211656-x8ngjxc"}`@DecimalMax(value)` 被注释的元素必须是一个数字，其值必须小于等于指定的最大值
  {: id="20210330211656-3evlln5"}
- {: id="20210330211656-af4i0o5"}`@Size(max=, min=)`被注释的元素的大小必须在指定的范围内
  {: id="20210330211656-wgf1nkh"}
- {: id="20210330211656-ryhi29v"}`@Digits (integer, fraction)`被注释的元素必须是一个数字，其值必须在可接受的范围内
  {: id="20210330211656-3z6b50j"}
- {: id="20210330211656-pcxl4rd"}`@Past`被注释的元素必须是一个过去的日期
  {: id="20210330211656-pit7r61"}
- {: id="20210330211656-1vleu6r"}`@Future` 被注释的元素必须是一个将来的日期
  {: id="20210330211656-aek733q"}
- {: id="20210330211656-wpd8w2u"}......
  {: id="20210330211656-92mrrle"}
{: id="20210330211656-5m617ld"}

#### 6.2. 验证请求体(RequestBody)
{: id="20210330211656-l7q36vx"}

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Person {

    @NotNull(message = "classId 不能为空")
    private String classId;

    @Size(max = 33)
    @NotNull(message = "name 不能为空")
    private String name;

    @Pattern(regexp = "((^Man$|^Woman$|^UGM$))", message = "sex 值不在可选范围")
    @NotNull(message = "sex 不能为空")
    private String sex;

    @Email(message = "email 格式不正确")
    @NotNull(message = "email 不能为空")
    private String email;

}
```
{: id="20210330211656-70bjz00"}

我们在需要验证的参数上加上了`@Valid`注解，如果验证失败，它将抛出`MethodArgumentNotValidException`。
{: id="20210330211656-fku3jpq"}

```java
@RestController
@RequestMapping("/api")
public class PersonController {

    @PostMapping("/person")
    public ResponseEntity<Person> getPerson(@RequestBody @Valid Person person) {
        return ResponseEntity.ok().body(person);
    }
}
```
{: id="20210330211656-fid7j25"}

#### 6.3. 验证请求参数(Path Variables 和 Request Parameters)
{: id="20210330211656-o4kq9pc"}

**一定一定不要忘记在类上加上 `Validated` 注解了，这个参数可以告诉 Spring 去校验方法参数。**
{: id="20210330211656-yvct83i"}

```java
@RestController
@RequestMapping("/api")
@Validated
public class PersonController {

    @GetMapping("/person/{id}")
    public ResponseEntity<Integer> getPersonByID(@Valid @PathVariable("id") @Max(value = 5,message = "超过 id 的范围了") Integer id) {
        return ResponseEntity.ok().body(id);
    }
}
```
{: id="20210330211656-kbg0qjx"}

更多关于如何在 Spring 项目中进行参数校验的内容，请看《[如何在 Spring/Spring Boot 中做参数校验？你需要了解的都在这里！](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247485783&idx=1&sn=a407f3b75efa17c643407daa7fb2acd6&chksm=cea2469cf9d5cf8afbcd0a8a1c9cc4294d6805b8e01bee6f76bb2884c5bc15478e91459def49&token=292197051&lang=zh_CN#rd)》这篇文章。
{: id="20210330211656-p5rnfwj"}

### 7. 全局处理 Controller 层异常
{: id="20210330211656-ojwf0rw"}

介绍一下我们 Spring 项目必备的全局处理 Controller 层异常。
{: id="20210330211656-8r281ky"}

**相关注解：**
{: id="20210330211656-ghoa179"}

1. {: id="20210330211656-p4apcqy"}`@ControllerAdvice` :注解定义全局异常处理类
   {: id="20210330211656-bqx340z"}
2. {: id="20210330211656-6r10fiu"}`@ExceptionHandler` :注解声明异常处理方法
   {: id="20210330211656-gplzvg0"}
{: id="20210330211656-m3nhdi3"}

如何使用呢？拿我们在第 5 节参数校验这块来举例子。如果方法参数不对的话就会抛出`MethodArgumentNotValidException`，我们来处理这个异常。
{: id="20210330211656-x69uib0"}

```java
@ControllerAdvice
@ResponseBody
public class GlobalExceptionHandler {

    /**
     * 请求参数异常处理
     */
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<?> handleMethodArgumentNotValidException(MethodArgumentNotValidException ex, HttpServletRequest request) {
       ......
    }
}
```
{: id="20210330211656-1xdwduh"}

更多关于 Spring Boot 异常处理的内容，请看我的这两篇文章：
{: id="20210330211656-bhpr3ip"}

1. {: id="20210330211656-fluuedo"}[SpringBoot 处理异常的几种常见姿势](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247485568&idx=2&sn=c5ba880fd0c5d82e39531fa42cb036ac&chksm=cea2474bf9d5ce5dcbc6a5f6580198fdce4bc92ef577579183a729cb5d1430e4994720d59b34&token=2133161636&lang=zh_CN#rd)
   {: id="20210330211656-b8e288x"}
2. {: id="20210330211656-qv9tdpg"}[使用枚举简单封装一个优雅的 Spring Boot 全局异常处理！](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247486379&idx=2&sn=48c29ae65b3ed874749f0803f0e4d90e&chksm=cea24460f9d5cd769ed53ad7e17c97a7963a89f5350e370be633db0ae8d783c3a3dbd58c70f8&token=1054498516&lang=zh_CN#rd)
   {: id="20210330211656-i6lqcl0"}
{: id="20210330211656-tp72xee"}

### 8. JPA 相关
{: id="20210330211656-uy8v4m5"}

#### 8.1. 创建表
{: id="20210330211656-y42mnjr"}

`@Entity`声明一个类对应一个数据库实体。
{: id="20210330211656-7erlpsd"}

`@Table` 设置表名
{: id="20210330211656-5yqb88j"}

```java
@Entity
@Table(name = "role")
public class Role {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String description;
    省略getter/setter......
}
```
{: id="20210330211656-jo23e2h"}

#### 8.2. 创建主键
{: id="20210330211656-hdf1fpd"}

`@Id` ：声明一个字段为主键。
{: id="20210330211656-162hfx1"}

使用`@Id`声明之后，我们还需要定义主键的生成策略。我们可以使用 `@GeneratedValue` 指定主键生成策略。
{: id="20210330211656-i4g8dus"}

**1.通过 `@GeneratedValue`直接使用 JPA 内置提供的四种主键生成策略来指定主键生成策略。**
{: id="20210330211656-lh7qjao"}

```java
@Id
@GeneratedValue(strategy = GenerationType.IDENTITY)
private Long id;
```
{: id="20210330211656-vezfqgi"}

JPA 使用枚举定义了 4 中常见的主键生成策略，如下：
{: id="20210330211656-7k7u2wp"}

_Guide 哥：枚举替代常量的一种用法_
{: id="20210330211656-vfses8d"}

```java
public enum GenerationType {

    /**
     * 使用一个特定的数据库表格来保存主键
     * 持久化引擎通过关系数据库的一张特定的表格来生成主键,
     */
    TABLE,

    /**
     *在某些数据库中,不支持主键自增长,比如Oracle、PostgreSQL其提供了一种叫做"序列(sequence)"的机制生成主键
     */
    SEQUENCE,

    /**
     * 主键自增长
     */
    IDENTITY,

    /**
     *把主键生成策略交给持久化引擎(persistence engine),
     *持久化引擎会根据数据库在以上三种主键生成 策略中选择其中一种
     */
    AUTO
}

```
{: id="20210330211656-btses6z"}

`@GeneratedValue`注解默认使用的策略是`GenerationType.AUTO`
{: id="20210330211656-7pvb0ju"}

```java
public @interface GeneratedValue {

    GenerationType strategy() default AUTO;
    String generator() default "";
}
```
{: id="20210330211656-xuhm591"}

一般使用 MySQL 数据库的话，使用`GenerationType.IDENTITY`策略比较普遍一点（分布式系统的话需要另外考虑使用分布式 ID）。
{: id="20210330211656-6n8oz2e"}

**2.通过 `@GenericGenerator`声明一个主键策略，然后 `@GeneratedValue`使用这个策略**
{: id="20210330211656-a6caaof"}

```java
@Id
@GeneratedValue(generator = "IdentityIdGenerator")
@GenericGenerator(name = "IdentityIdGenerator", strategy = "identity")
private Long id;
```
{: id="20210330211656-6wtlmtg"}

等价于：
{: id="20210330211656-x5fy2o3"}

```java
@Id
@GeneratedValue(strategy = GenerationType.IDENTITY)
private Long id;
```
{: id="20210330211656-a8k01bz"}

jpa 提供的主键生成策略有如下几种：
{: id="20210330211656-tcw3ln5"}

```java
public class DefaultIdentifierGeneratorFactory
		implements MutableIdentifierGeneratorFactory, Serializable, ServiceRegistryAwareService {

	@SuppressWarnings("deprecation")
	public DefaultIdentifierGeneratorFactory() {
		register( "uuid2", UUIDGenerator.class );
		register( "guid", GUIDGenerator.class );			// can be done with UUIDGenerator + strategy
		register( "uuid", UUIDHexGenerator.class );			// "deprecated" for new use
		register( "uuid.hex", UUIDHexGenerator.class ); 	// uuid.hex is deprecated
		register( "assigned", Assigned.class );
		register( "identity", IdentityGenerator.class );
		register( "select", SelectGenerator.class );
		register( "sequence", SequenceStyleGenerator.class );
		register( "seqhilo", SequenceHiLoGenerator.class );
		register( "increment", IncrementGenerator.class );
		register( "foreign", ForeignGenerator.class );
		register( "sequence-identity", SequenceIdentityGenerator.class );
		register( "enhanced-sequence", SequenceStyleGenerator.class );
		register( "enhanced-table", TableGenerator.class );
	}

	public void register(String strategy, Class generatorClass) {
		LOG.debugf( "Registering IdentifierGenerator strategy [%s] -> [%s]", strategy, generatorClass.getName() );
		final Class previous = generatorStrategyToClassNameMap.put( strategy, generatorClass );
		if ( previous != null ) {
			LOG.debugf( "    - overriding [%s]", previous.getName() );
		}
	}

}
```
{: id="20210330211656-5wxm937"}

#### 8.3. 设置字段类型
{: id="20210330211656-0z3lso2"}

`@Column` 声明字段。
{: id="20210330211656-bb4l7x1"}

**示例：**
{: id="20210330211656-3tv8pep"}

设置属性 userName 对应的数据库字段名为 user_name，长度为 32，非空
{: id="20210330211656-0zz0w7o"}

```java
@Column(name = "user_name", nullable = false, length=32)
private String userName;
```
{: id="20210330211656-jx68h4g"}

设置字段类型并且加默认值，这个还是挺常用的。
{: id="20210330211656-ilg8v30"}

```java
Column(columnDefinition = "tinyint(1) default 1")
private Boolean enabled;
```
{: id="20210330211656-34fprgu"}

#### 8.4. 指定不持久化特定字段
{: id="20210330211656-rcwvht8"}

`@Transient` ：声明不需要与数据库映射的字段，在保存的时候不需要保存进数据库 。
{: id="20210330211656-mfe5mdj"}

如果我们想让`secrect` 这个字段不被持久化，可以使用 `@Transient`关键字声明。
{: id="20210330211656-uy1rupr"}

```java
Entity(name="USER")
public class User {

    ......
    @Transient
    private String secrect; // not persistent because of @Transient

}
```
{: id="20210330211656-8476gcs"}

除了 `@Transient`关键字声明， 还可以采用下面几种方法：
{: id="20210330211656-v6pgq6c"}

```java
static String secrect; // not persistent because of static
final String secrect = “Satish”; // not persistent because of final
transient String secrect; // not persistent because of transient
```
{: id="20210330211656-68kqof1"}

一般使用注解的方式比较多。
{: id="20210330211656-nualgt9"}

#### 8.5. 声明大字段
{: id="20210330211656-7fm48sm"}

`@Lob`:声明某个字段为大字段。
{: id="20210330211656-gj071cy"}

```java
@Lob
private String content;
```
{: id="20210330211656-yrccwsj"}

更详细的声明：
{: id="20210330211656-o71zgut"}

```java
@Lob
//指定 Lob 类型数据的获取策略， FetchType.EAGER 表示非延迟 加载，而 FetchType. LAZY 表示延迟加载 ；
@Basic(fetch = FetchType.EAGER)
//columnDefinition 属性指定数据表对应的 Lob 字段类型
@Column(name = "content", columnDefinition = "LONGTEXT NOT NULL")
private String content;
```
{: id="20210330211656-ijqnhtj"}

#### 8.6. 创建枚举类型的字段
{: id="20210330211656-3su2kia"}

可以使用枚举类型的字段，不过枚举字段要用`@Enumerated`注解修饰。
{: id="20210330211656-i37ni18"}

```java
public enum Gender {
    MALE("男性"),
    FEMALE("女性");

    private String value;
    Gender(String str){
        value=str;
    }
}
```
{: id="20210330211656-h6em8u1"}

```java
@Entity
@Table(name = "role")
public class Role {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String description;
    @Enumerated(EnumType.STRING)
    private Gender gender;
    省略getter/setter......
}
```
{: id="20210330211656-5ksvlcq"}

数据库里面对应存储的是 MAIL/FEMAIL。
{: id="20210330211656-4vuwt6l"}

#### 8.7. 增加审计功能
{: id="20210330211656-vcr5zda"}

只要继承了 `AbstractAuditBase`的类都会默认加上下面四个字段。
{: id="20210330211656-v8y7za4"}

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
@MappedSuperclass
@EntityListeners(value = AuditingEntityListener.class)
public abstract class AbstractAuditBase {

    @CreatedDate
    @Column(updatable = false)
    @JsonIgnore
    private Instant createdAt;

    @LastModifiedDate
    @JsonIgnore
    private Instant updatedAt;

    @CreatedBy
    @Column(updatable = false)
    @JsonIgnore
    private String createdBy;

    @LastModifiedBy
    @JsonIgnore
    private String updatedBy;
}

```
{: id="20210330211656-t2v9esu"}

我们对应的审计功能对应地配置类可能是下面这样的（Spring Security 项目）:
{: id="20210330211656-js4lmtv"}

```java

@Configuration
@EnableJpaAuditing
public class AuditSecurityConfiguration {
    @Bean
    AuditorAware<String> auditorAware() {
        return () -> Optional.ofNullable(SecurityContextHolder.getContext())
                .map(SecurityContext::getAuthentication)
                .filter(Authentication::isAuthenticated)
                .map(Authentication::getName);
    }
}
```
{: id="20210330211656-pw5pu3q"}

简单介绍一下上面设计到的一些注解：
{: id="20210330211656-6s60r2o"}

1. {: id="20210330211656-4bbcix2"}`@CreatedDate`: 表示该字段为创建时间时间字段，在这个实体被 insert 的时候，会设置值
   {: id="20210330211656-5uw2qvg"}
2. {: id="20210330211656-1xxcuo5"}`@CreatedBy` :表示该字段为创建人，在这个实体被 insert 的时候，会设置值
   {: id="20210330211656-67r058m"}
   `@LastModifiedDate`、`@LastModifiedBy`同理。
   {: id="20210330211656-6zpurkw"}
{: id="20210330211656-2407vfv"}

`@EnableJpaAuditing`：开启 JPA 审计功能。
{: id="20210330211656-w2j6ai3"}

#### 8.8. 删除/修改数据
{: id="20210330211656-upoffj8"}

`@Modifying` 注解提示 JPA 该操作是修改操作,注意还要配合`@Transactional`注解使用。
{: id="20210330211656-4m9zoqm"}

```java
@Repository
public interface UserRepository extends JpaRepository<User, Integer> {

    @Modifying
    @Transactional(rollbackFor = Exception.class)
    void deleteByUserName(String userName);
}
```
{: id="20210330211656-ifpqx7i"}

#### 8.9. 关联关系
{: id="20210330211656-sfzxldr"}

- {: id="20210330211656-8u3h566"}`@OneToOne` 声明一对一关系
  {: id="20210330211656-w2hvfr6"}
- {: id="20210330211656-94h68oj"}`@OneToMany` 声明一对多关系
  {: id="20210330211656-0a7fy9y"}
- {: id="20210330211656-n82h0nw"}`@ManyToOne`声明多对一关系
  {: id="20210330211656-kdhxn79"}
- {: id="20210330211656-p6bmlsg"}`MangToMang`声明多对多关系
  {: id="20210330211656-tbf1d48"}
{: id="20210330211656-2bfe4qp"}

更多关于 Spring Boot JPA 的文章请看我的这篇文章：[一文搞懂如何在 Spring Boot 正确中使用 JPA](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247485689&idx=1&sn=061b32c2222869932be5631fb0bb5260&chksm=cea24732f9d5ce24a356fb3675170e7843addbfcc79ee267cfdb45c83fc7e90babf0f20d22e1&token=292197051&lang=zh_CN#rd) 。
{: id="20210330211656-u3yk0fx"}

### 9. 事务 `@Transactional`
{: id="20210330211656-jyravt0"}

在要开启事务的方法上使用`@Transactional`注解即可!
{: id="20210330211656-81l18ez"}

```java
@Transactional(rollbackFor = Exception.class)
public void save() {
  ......
}

```
{: id="20210330211656-68n03y7"}

我们知道 Exception 分为运行时异常 RuntimeException 和非运行时异常。在`@Transactional`注解中如果不配置`rollbackFor`属性,那么事物只会在遇到`RuntimeException`的时候才会回滚,加上`rollbackFor=Exception.class`,可以让事物在遇到非运行时异常时也回滚。
{: id="20210330211656-evqj532"}

`@Transactional` 注解一般用在可以作用在`类`或者`方法`上。
{: id="20210330211656-i0m2j1d"}

- {: id="20210330211656-b2e6wd6"}**作用于类**：当把`@Transactional 注解放在类上时，表示所有该类的`public 方法都配置相同的事务属性信息。
  {: id="20210330211656-cyhfcvx"}
- {: id="20210330211656-otzdqeo"}**作用于方法**：当类配置了`@Transactional`，方法也配置了`@Transactional`，方法的事务会覆盖类的事务配置信息。
  {: id="20210330211656-4og85ni"}
{: id="20210330211656-dpnaygu"}

更多关于关于 Spring 事务的内容请查看：
{: id="20210330211656-u0dmu64"}

1. {: id="20210330211656-bf1gxee"}[可能是最漂亮的 Spring 事务管理详解](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247484943&idx=1&sn=46b9082af4ec223137df7d1c8303ca24&chksm=cea249c4f9d5c0d2b8212a17252cbfb74e5fbe5488b76d829827421c53332326d1ec360f5d63&token=1082669959&lang=zh_CN#rd)
   {: id="20210330211656-srj9bkt"}
2. {: id="20210330211656-5i58ido"}[一口气说出 6 种 @Transactional 注解失效场景](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247486483&idx=2&sn=77be488e206186803531ea5d7164ec53&chksm=cea243d8f9d5cacecaa5c5daae4cde4c697b9b5b21f96dfc6cce428cfcb62b88b3970c26b9c2&token=816772476&lang=zh_CN#rd)
   {: id="20210330211656-1uk7pb9"}
{: id="20210330211656-px8ypjl"}

### 10. json 数据处理
{: id="20210330211656-ls1d70e"}

#### 10.1. 过滤 json 数据
{: id="20210330211656-fxgob6n"}

**`@JsonIgnoreProperties` 作用在类上用于过滤掉特定字段不返回或者不解析。**
{: id="20210330211656-ynfo88c"}

```java
//生成json时将userRoles属性过滤
@JsonIgnoreProperties({"userRoles"})
public class User {

    private String userName;
    private String fullName;
    private String password;
    @JsonIgnore
    private List<UserRole> userRoles = new ArrayList<>();
}
```
{: id="20210330211656-09i6gwo"}

**`@JsonIgnore`一般用于类的属性上，作用和上面的`@JsonIgnoreProperties` 一样。**
{: id="20210330211656-k2mjgb5"}

```java

public class User {

    private String userName;
    private String fullName;
    private String password;
   //生成json时将userRoles属性过滤
    @JsonIgnore
    private List<UserRole> userRoles = new ArrayList<>();
}
```
{: id="20210330211656-hox1yoj"}

#### 10.2. 格式化 json 数据
{: id="20210330211656-gkp3m2m"}

`@JsonFormat`一般用来格式化 json 数据。：
{: id="20210330211656-m5gz5v9"}

比如：
{: id="20210330211656-73529gp"}

```java
@JsonFormat(shape=JsonFormat.Shape.STRING, pattern="yyyy-MM-dd'T'HH:mm:ss.SSS'Z'", timezone="GMT")
private Date date;
```
{: id="20210330211656-c5yb3r0"}

#### 10.3. 扁平化对象
{: id="20210330211656-78loxfe"}

```java
@Getter
@Setter
@ToString
public class Account {
    @JsonUnwrapped
    private Location location;
    @JsonUnwrapped
    private PersonInfo personInfo;

  @Getter
  @Setter
  @ToString
  public static class Location {
     private String provinceName;
     private String countyName;
  }
  @Getter
  @Setter
  @ToString
  public static class PersonInfo {
    private String userName;
    private String fullName;
  }
}

```
{: id="20210330211656-nu4y1si"}

未扁平化之前：
{: id="20210330211656-uylzimy"}

```json
{
    "location": {
        "provinceName":"湖北",
        "countyName":"武汉"
    },
    "personInfo": {
        "userName": "coder1234",
        "fullName": "shaungkou"
    }
}
```
{: id="20210330211656-alhyant"}

使用`@JsonUnwrapped` 扁平对象之后：
{: id="20210330211656-fewowwx"}

```java
@Getter
@Setter
@ToString
public class Account {
    @JsonUnwrapped
    private Location location;
    @JsonUnwrapped
    private PersonInfo personInfo;
    ......
}
```
{: id="20210330211656-sx9v9c4"}

```json
{
  "provinceName":"湖北",
  "countyName":"武汉",
  "userName": "coder1234",
  "fullName": "shaungkou"
}
```
{: id="20210330211656-ay86548"}

### 11. 测试相关
{: id="20210330211656-0a52ogi"}

**`@ActiveProfiles`一般作用于测试类上， 用于声明生效的 Spring 配置文件。**
{: id="20210330211656-171m3bs"}

```java
@SpringBootTest(webEnvironment = RANDOM_PORT)
@ActiveProfiles("test")
@Slf4j
public abstract class TestBase {
  ......
}
```
{: id="20210330211656-0k74gpi"}

**`@Test`声明一个方法为测试方法**
{: id="20210330211656-bkyuran"}

**`@Transactional`被声明的测试方法的数据会回滚，避免污染测试数据。**
{: id="20210330211656-3cln4up"}

**`@WithMockUser` Spring Security 提供的，用来模拟一个真实用户，并且可以赋予权限。**
{: id="20210330211656-3usun3j"}

```java
    @Test
    @Transactional
    @WithMockUser(username = "user-id-18163138155", authorities = "ROLE_TEACHER")
    void should_import_student_success() throws Exception {
        ......
    }
```
{: id="20210330211656-ypc72av"}

_暂时总结到这里吧！虽然花了挺长时间才写完，不过可能还是会一些常用的注解的被漏掉，所以，我将文章也同步到了 Github 上去，Github 地址： 欢迎完善！_
{: id="20210330211656-ndhs9kv"}

本文已经收录进我的 75K Star 的 Java 开源项目 JavaGuide：[https://github.com/Snailclimb/JavaGuide](https://github.com/Snailclimb/JavaGuide)。
{: id="20210330211656-sm71k8j"}


{: id="20210330211656-jhypl6h" type="doc"}
