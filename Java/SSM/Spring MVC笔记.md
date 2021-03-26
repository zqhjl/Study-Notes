### Spring MVC
{: id="20210326221302-vktd5w7"}

Spring MVC 是目前主流的实现 MVC 设计模式的企业级开发框架，Spring 框架的一个子模块，无需整合，开发起来更加便捷。
{: id="20210326221302-2wnge58"}

#### 什么是 MVC 设计模式？
{: id="20210326221302-0t7r756"}

将应用程序分为 Controller、Model、View 三层，Controller 接收客户端请求，调用 Model 生成业务数据，传递给 View。
{: id="20210326221302-lozad3n"}

Spring MVC 就是对这套流程的封装，屏蔽了很多底层代码，开放出接口，让开发者可以更加轻松、便捷地完成基于 MVC 模式的 Web 开发。
{: id="20210326221302-hm1lmjg"}

#### Spring MVC 的核心组件
{: id="20210326221302-nz8vp4n"}

- {: id="20210326221302-cr77l5g"}DispatcherServlet：前置控制器，是整个流程控制的核心，控制其他组件的执行，进行统一调度，降低组件之间的耦合性，相当于总指挥。
  {: id="20210326221302-ofy5ze0"}
- {: id="20210326221302-x1gwa78"}Handler：处理器，完成具体的业务逻辑，相当于 Servlet 或 Action。
  {: id="20210326221302-xin9lk7"}
- {: id="20210326221302-lvwdfo0"}HandlerMapping：DispatcherServlet 接收到请求之后，通过 HandlerMapping 将不同的请求映射到不同的 Handler。
  {: id="20210326221302-m64t95s"}
- {: id="20210326221302-5of0fgo"}HandlerInterceptor：处理器拦截器，是一个接口，如果需要完成一些拦截处理，可以实现该接口。
  {: id="20210326221302-s2johve"}
- {: id="20210326221302-5wqkeyo"}HandlerExecutionChain：处理器执行链，包括两部分内容：Handler 和 HandlerInterceptor（系统会有一个默认的 HandlerInterceptor，如果需要额外设置拦截，可以添加拦截器）。
  {: id="20210326221302-9vwozg2"}
- {: id="20210326221302-ldp4347"}HandlerAdapter：处理器适配器，Handler 执行业务方法之前，需要进行一系列的操作，包括表单数据的验证、数据类型的转换、将表单数据封装到 JavaBean 等，这些操作都是由 HandlerApater 来完成，开发者只需将注意力集中业务逻辑的处理上，DispatcherServlet 通过 HandlerAdapter 执行不同的 Handler。
  {: id="20210326221302-js2slsg"}
- {: id="20210326221302-e5ffaed"}ModelAndView：装载了模型数据和视图信息，作为 Handler 的处理结果，返回给 DispatcherServlet。
  {: id="20210326221302-6wkoyoh"}
- {: id="20210326221302-6cmmzkx"}ViewResolver：视图解析器，DispatcheServlet 通过它将逻辑视图解析为物理视图，最终将渲染结果响应给客户端。
  {: id="20210326221302-85w3n1z"}
{: id="20210326221302-459qc8i"}

#### Spring MVC 的工作流程
{: id="20210326221302-1b8oy3s"}

- {: id="20210326221302-qdkmdp2"}客户端请求被 DisptacherServlet 接收。
  {: id="20210326221302-vxmt99j"}
- {: id="20210326221302-vema1x4"}根据 HandlerMapping 映射到 Handler。
  {: id="20210326221302-edm9qjb"}
- {: id="20210326221302-uk57qhn"}生成 Handler 和 HandlerInterceptor。
  {: id="20210326221302-6ws4jhf"}
- {: id="20210326221302-982aan2"}Handler 和 HandlerInterceptor 以 HandlerExecutionChain 的形式一并返回给 DisptacherServlet。
  {: id="20210326221302-jmm2el0"}
- {: id="20210326221302-xs9j7mb"}DispatcherServlet 通过 HandlerAdapter 调用 Handler 的方法完成业务逻辑处理。
  {: id="20210326221302-337o8jz"}
- {: id="20210326221302-40890dp"}Handler 返回一个 ModelAndView 给 DispatcherServlet。
  {: id="20210326221302-a8rnmkr"}
- {: id="20210326221302-tw6vyqq"}DispatcherServlet 将获取的 ModelAndView 对象传给 ViewResolver 视图解析器，将逻辑视图解析为物理视图 View。
  {: id="20210326221302-brb582s"}
- {: id="20210326221302-0thy19a"}ViewResovler 返回一个 View 给 DispatcherServlet。
  {: id="20210326221302-gr3ayxn"}
- {: id="20210326221302-3krmzx1"}DispatcherServlet 根据 View 进行视图渲染（将模型数据 Model 填充到视图 View 中）。
  {: id="20210326221302-19phpj7"}
- {: id="20210326221302-wckj6dz"}DispatcherServlet 将渲染后的结果响应给客户端。
  {: id="20210326221302-og5bvfg"}
{: id="20210326221302-2fdavq6"}

![image-20190313111136254](/Users/southwind/Library/Application Support/typora-user-images/image-20190313111136254.png)
{: id="20210326221302-2yt6r5j"}

Spring MVC 流程非常复杂，实际开发中很简单，因为大部分的组件不需要开发者创建、管理，只需要通过配置文件的方式完成配置即可，真正需要开发者进行处理的只有 Handler 、View。
{: id="20210326221302-inhl1hk"}

#### 如何使用？
{: id="20210326221302-u37ulv8"}

- {: id="20210326221302-noh3yvj"}创建 Maven 工程，pom.xml
  {: id="20210326221302-d6czvic"}
{: id="20210326221302-wi51wf7"}

```xml
<dependencies>

    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.0.11.RELEASE</version>
    </dependency>

</dependencies>
```
{: id="20210326221302-vjyaf4l"}

- {: id="20210326221302-k0h7ruu"}在 web.xml 中配置 DispatcherServlet。
  {: id="20210326221302-dj32ej6"}
{: id="20210326221302-kej1gul"}

```xml
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
  <display-name>Archetype Created Web Application</display-name>
  
  <servlet>
    <servlet-name>dispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:springmvc.xml</param-value>
    </init-param>
  </servlet>
  
  <servlet-mapping>
    <servlet-name>dispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
  
</web-app>
```
{: id="20210326221302-saj8agz"}

- {: id="20210326221302-lm2h3vn"}springmvc.xml
  {: id="20210326221302-leq8ny6"}
{: id="20210326221302-w6fenng"}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/mvc
       http://www.springframework.org/schema/mvc/spring-mvc-3.2.xsd">

    <!-- 自动扫描 -->
    <context:component-scan base-package="com.southwind"></context:component-scan>

    <!-- 配置视图解析器 -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/"></property>
        <property name="suffix" value=".jsp"></property>
    </bean>

</beans>
```
{: id="20210326221302-pz8x6qu"}

- {: id="20210326221302-jd4ieie"}创建 Handler
  {: id="20210326221302-a6pgeks"}
{: id="20210326221302-b2fk9sl"}

```java
package com.southwind.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class HelloHandler {

    @RequestMapping("/index")
    public String index(){
        System.out.println("执行了index...");
        return "index";
    }
}
```
{: id="20210326221302-sqs4qv4"}

### Spring MVC 注解
{: id="20210326221302-qywaxa4"}

- {: id="20210326221302-tsdply4"}@RequestMapping
  {: id="20210326221302-azxber3"}
{: id="20210326221302-uhkf82w"}

Spring MVC 通过 @RequestMapping 注解将 URL 请求与业务方法进行映射，在 Handler 的类定义处以及方法定义处都可以添加 @RequestMapping ，在类定义处添加，相当于客户端多了一层访问路径。
{: id="20210326221302-dw3dmwu"}

- {: id="20210326221302-i2aobm3"}@Controller
  {: id="20210326221302-sn125xd"}
{: id="20210326221302-iai8m32"}

@Controller 在类定义处添加，将该类交个 IoC 容器来管理（结合 springmvc.xml 的自动扫描配置使用），同时使其成为一个控制器，可以接收客户端请求。
{: id="20210326221302-mozuo7z"}

```java
package com.southwind.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/hello")
public class HelloHandler {

    @RequestMapping("/index")
    public String index(){
        System.out.println("执行了index...");
        return "index";
    }
}
```
{: id="20210326221302-r6xx54a"}

- {: id="20210326221302-lxgejbo"}@RequestMapping 相关参数
  {: id="20210326221302-zwf08xt"}
{: id="20210326221302-2wf7qgz"}

1、value：指定 URL 请求的实际地址，是 @RequestMapping 的默认值。
{: id="20210326221302-1fyfn48"}

```java
@RequestMapping("/index")
public String index(){
    System.out.println("执行了index...");
    return "index";
}
```
{: id="20210326221302-vv6q9p8"}

等于
{: id="20210326221302-fdcvlge"}

```java
@RequestMapping(value="/index")
public String index(){
    System.out.println("执行了index...");
    return "index";
}
```
{: id="20210326221302-lxr378o"}

2、method：指定请求的 method 类型，GET、POST、PUT、DELET。
{: id="20210326221302-3qj84l5"}

```java
@RequestMapping(value = "/index",method = RequestMethod.GET)
public String index(){
    System.out.println("执行了index...");
    return "index";
}
```
{: id="20210326221302-4p7slmp"}

上述代码表示 index 方法只能接收 GET 请求。
{: id="20210326221302-lfi19av"}

3、params：指定请求中必须包含某些参数，否则无法调用该方法。
{: id="20210326221302-5wrw4i6"}

```java
@RequestMapping(value = "/index",method = RequestMethod.GET,params = {"name","id=10"})
public String index(){
    System.out.println("执行了index...");
    return "index";
}
```
{: id="20210326221302-6wuqa69"}

上述代码表示请求中必须包含 name 和 id 两个参数，同时 id 的值必须是 10。
{: id="20210326221302-h7nho6m"}

关于参数绑定，在形参列表中通过添加 @RequestParam 注解完成 HTTP 请求参数与业务方法形参的映射。
{: id="20210326221302-6xur7xf"}

```java
@RequestMapping(value = "/index",method = RequestMethod.GET,params = {"name","id=10"})
public String index(@RequestParam("name") String str,@RequestParam("id") int age){
    System.out.println(str);
    System.out.println(age);
    System.out.println("执行了index...");
    return "index";
}
```
{: id="20210326221302-yxf5iwt"}

上述代码表示将请求的参数 name 和 id 分别赋给了形参 str 和 age ，同时自动完成了数据类型转换，将 “10” 转为了 int 类型的 10，再赋给 age，这些工作都是由 HandlerAdapter 来完成的。
{: id="20210326221302-5wxu3q1"}

Spring MVC 也支持 RESTful 风格的 URL。
{: id="20210326221302-272ge1k"}

传统类型：http://localhost:8080/hello/index?name=zhangsan&id=10
{: id="20210326221302-4ueg74z"}

REST：http://localhost:8080/hello/index/zhangsan/10
{: id="20210326221302-s1alni8"}

```java
@RequestMapping("/rest/{name}/{id}")
public String rest(@PathVariable("name") String name,@PathVariable("id") int id){
    System.out.println(name);
    System.out.println(id);
    return "index";
}
```
{: id="20210326221302-fxbc17p"}

通过 @PathVariable 注解完成请求参数与形参的映射。
{: id="20210326221302-49wojpc"}

- {: id="20210326221302-0yaqlhy"}映射 Cookie
  {: id="20210326221302-8tnrq3l"}
{: id="20210326221302-zhzvfc1"}

Spring MVC 通过映射可以直接在业务方法中获取 Cookie 的值。
{: id="20210326221302-wuothud"}

```java
@RequestMapping("/cookie")
public String cookie(@CookieValue(value = "JSESSIONID") String sessionId){
    System.out.println(sessionId);
    return "index";
}
```
{: id="20210326221302-z54jsj4"}

- {: id="20210326221302-rbusd1i"}使用 JavaBean 绑定参数
  {: id="20210326221302-3fi24cg"}
{: id="20210326221302-jn0ui4t"}

Spring MVC 会根据请求参数名和 JavaBean 属性名进行自动匹配，自动为对象填充属性值，同时支持及联属性。
{: id="20210326221302-re54asw"}

```java
package com.southwind.entity;

import lombok.Data;

@Data
public class Address {
    private String value;
}
```
{: id="20210326221302-eio80dm"}

```java
package com.southwind.entity;

import lombok.Data;

@Data
public class User {
    private long id;
    private String name;
    private Address address;
}
```
{: id="20210326221302-fmd8lcf"}

```jsp
<%--
  Created by IntelliJ IDEA.
  User: southwind
  Date: 2019-03-13
  Time: 15:33
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <form action="/hello/save" method="post">
        用户id：<input type="text" name="id"/><br/>
        用户名：<input type="text" name="name"/><br/>
        用户地址：<input type="text" name="address.value"/><br/>
        <input type="submit" value="注册"/>
    </form>
</body>
</html>
```
{: id="20210326221302-a3izzpu"}

```java
@RequestMapping(value = "/save",method = RequestMethod.POST)
public String save(User user){
    System.out.println(user);
    return "index";
}
```
{: id="20210326221302-ifvvibb"}

如果出现中文乱码问题，只需在 web.xml 添加 Spring MVC 自带的过滤器即可。
{: id="20210326221302-i8hg1y4"}

```xml
<filter>
    <filter-name>encodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
</filter>

<filter-mapping>
    <filter-name>encodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```
{: id="20210326221302-skon9sg"}

- {: id="20210326221302-z7bh8lc"}JSP 页面的转发和重定向：
  {: id="20210326221302-tg2h386"}
{: id="20210326221302-ph9vi3e"}

Spring MVC 默认是以转发的形式响应 JSP。
{: id="20210326221302-ooiwnvy"}

1、转发
{: id="20210326221302-n6rfmjo"}

```java
@RequestMapping("/forward")
public String forward(){
    return "forward:/index.jsp";
    //        return "index";
}
```
{: id="20210326221302-67bwlzm"}

2、重定向
{: id="20210326221302-ld293ut"}

```java
@RequestMapping("/redirect")
public String redirect(){
    return "redirect:/index.jsp";
}
```
{: id="20210326221302-gdc328u"}

### Spring MVC 数据绑定
{: id="20210326221302-oxjtmll"}

数据绑定：在后端的业务方法中直接获取客户端 HTTP 请求中的参数，将请求参数映射到业务方法的形参中，Spring MVC 中数据绑定的工作是由 HandlerAdapter 来完成的。
{: id="20210326221302-87q59yd"}

- {: id="20210326221302-dt47brv"}基本数据类型
  {: id="20210326221302-u9v99v0"}
{: id="20210326221302-ah1lmzj"}

```java
@RequestMapping("/baseType")
@ResponseBody
public String baseType(int id){
    return id+"";
}
```
{: id="20210326221302-a8hoywc"}

@ResponseBody 表示 Spring MVC 会直接将业务方法的返回值响应给客户端，如果不加 @ResponseBody 注解，Spring MVC 会将业务方法的放回值传递给 DispatcherServlet，再由 DisptacherServlet 调用 ViewResolver 对返回值进行解析，映射到一个 JSP 资源。
{: id="20210326221302-g6viix1"}

- {: id="20210326221302-ohqk5za"}包装类
  {: id="20210326221302-a9q3dph"}
{: id="20210326221302-z86344h"}

```java
@RequestMapping("/packageType")
@ResponseBody
public String packageType(@RequestParam(value = "num",required = false,defaultValue = "0") Integer id){
    return id+"";
}
```
{: id="20210326221302-7rhjcs4"}

包装类可以接收 null，当 HTTP 请求没有参数时，使用包装类定义形参的数据类型，程序不会抛出异常。
{: id="20210326221302-yfl9xic"}

@RequestParam
{: id="20210326221302-s1rwc4i"}

value = "num"：将 HTTP 请求中名为 num 的参数赋给形参 id。
{: id="20210326221302-t68id4g"}

requried：设置 num 是否为必填项，true 表示必填，false 表示非必填，可省略。
{: id="20210326221302-xc3z1oz"}

defaultValue = “0”：如果 HTTP 请求中没有 num 参数，默认值为0.
{: id="20210326221302-pdyrzs4"}

- {: id="20210326221302-cm3q4ay"}数组
  {: id="20210326221302-h9bpo01"}
{: id="20210326221302-v7iw3mo"}

```java
@RestController
@RequestMapping("/data")
public class DataBindHandler {
    @RequestMapping("/array")
    public String array(String[] name){
        String str = Arrays.toString(name);
        return str;
    }
}
```
{: id="20210326221302-qb0ttr0"}

@RestController 表示该控制器会直接将业务方法的返回值响应给客户端，不进行视图解析。
{: id="20210326221302-rqvn7gj"}

@Controller 表示该控制器的每一个业务方法的返回值都会交给视图解析器进行解析，如果只需要将数据响应给客户端，而不需要进行视图解析，则需要在对应的业务方法定义处添加 @ResponseBody。
{: id="20210326221302-1ovep6b"}

```java
@RestController
@RequestMapping("/data")
public class DataBindHandler {
    @RequestMapping("/array")
    public String array(String[] name){
        String str = Arrays.toString(name);
        return str;
    }
}
```
{: id="20210326221302-gbcldej"}

等同于
{: id="20210326221302-q4l0oa2"}

```java
@Controller
@RequestMapping("/data")
public class DataBindHandler {
    @RequestMapping("/array")
    @ResponseBody
    public String array(String[] name){
        String str = Arrays.toString(name);
        return str;
    }
}
```
{: id="20210326221302-6bcxb2d"}

- {: id="20210326221302-wwkgyun"}List
  {: id="20210326221302-u5l0ody"}
{: id="20210326221302-vd0tqxb"}

Spring MVC 不支持 List 类型的直接转换，需要对 List 集合进行包装。
{: id="20210326221302-nsfddlu"}

集合封装类
{: id="20210326221302-fqcb0s6"}

```java
package com.southwind.entity;

import lombok.Data;

import java.util.List;

@Data
public class UserList {
    private List<User> users;
}
```
{: id="20210326221302-riftz0b"}

JSP
{: id="20210326221302-bdgdyfs"}

```jsp
<%--
  Created by IntelliJ IDEA.
  User: southwind
  Date: 2019-03-14
  Time: 09:12
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <form action="/data/list" method="post">
        用户1编号：<input type="text" name="users[0].id"/><br/>
        用户1名称：<input type="text" name="users[0].name"/><br/>
        用户2编号：<input type="text" name="users[1].id"/><br/>
        用户2名称：<input type="text" name="users[1].name"/><br/>
        用户3编号：<input type="text" name="users[2].id"/><br/>
        用户3名称：<input type="text" name="users[2].name"/><br/>
        <input type="submit" value="提交"/>
    </form>
</body>
</html>
```
{: id="20210326221302-tsk81rk"}

业务方法
{: id="20210326221302-6fgqamf"}

```java
@RequestMapping("/list")
public String list(UserList userList){
    StringBuffer str = new StringBuffer();
    for(User user:userList.getUsers()){
        str.append(user);
    }
    return str.toString();
}
```
{: id="20210326221302-8gn1siu"}

处理 @ResponseBody 中文乱码，在 springmvc.xml 中配置消息转换器。
{: id="20210326221302-2ttd5ah"}

```xml
<mvc:annotation-driven>
    <!-- 消息转换器 -->
    <mvc:message-converters register-defaults="true">
        <bean class="org.springframework.http.converter.StringHttpMessageConverter">
            <property name="supportedMediaTypes" value="text/html;charset=UTF-8"></property>
        </bean>
    </mvc:message-converters>
</mvc:annotation-driven>
```
{: id="20210326221302-zfa17qr"}

- {: id="20210326221302-jf92lum"}Map
  {: id="20210326221302-k2b0kro"}
{: id="20210326221302-e1fvajb"}

自定义封装类
{: id="20210326221302-luncnkw"}

```java
package com.southwind.entity;

import lombok.Data;

import java.util.Map;

@Data
public class UserMap {
    private Map<String,User> users;
}
```
{: id="20210326221302-riqfdfi"}

业务方法
{: id="20210326221302-gjnkmca"}

```java
@RequestMapping("/map")
public String map(UserMap userMap){
    StringBuffer str = new StringBuffer();
    for(String key:userMap.getUsers().keySet()){
        User user = userMap.getUsers().get(key);
        str.append(user);
    }
    return str.toString();
}
```
{: id="20210326221302-eot4doz"}

JSP
{: id="20210326221302-qd6aw6t"}

```jsp
<%--
  Created by IntelliJ IDEA.
  User: southwind
  Date: 2019-03-14
  Time: 09:12
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <form action="/data/map" method="post">
        用户1编号：<input type="text" name="users['a'].id"/><br/>
        用户1名称：<input type="text" name="users['a'].name"/><br/>
        用户2编号：<input type="text" name="users['b'].id"/><br/>
        用户2名称：<input type="text" name="users['b'].name"/><br/>
        用户3编号：<input type="text" name="users['c'].id"/><br/>
        用户3名称：<input type="text" name="users['c'].name"/><br/>
        <input type="submit" value="提交"/>
    </form>
</body>
</html>
```
{: id="20210326221302-ytpyby3"}

- {: id="20210326221302-alxnde0"}JSON
  {: id="20210326221302-4docu30"}
{: id="20210326221302-yy6jf36"}

客户端发生 JSON 格式的数据，直接通过 Spring MVC 绑定到业务方法的形参中。
{: id="20210326221302-j79h6ep"}

处理 Spring MVC 无法加载静态资源，在 web.xml 中添加配置即可。
{: id="20210326221302-oyrmmaw"}

```xml
<servlet-mapping>
    <servlet-name>default</servlet-name>
    <url-pattern>*.js</url-pattern>
</servlet-mapping>
```
{: id="20210326221302-58k0a2u"}

JSP
{: id="20210326221302-ydlduyj"}

```jsp
<%--
  Created by IntelliJ IDEA.
  User: southwind
  Date: 2019-03-14
  Time: 10:35
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
    <script type="text/javascript" src="js/jquery-3.3.1.min.js"></script>
    <script type="text/javascript">
        $(function(){
           var user = {
               "id":1,
               "name":"张三"
           };
           $.ajax({
               url:"/data/json",
               data:JSON.stringify(user),
               type:"POST",
               contentType:"application/json;charset=UTF-8",
               dataType:"JSON",
               success:function(data){
                   alter(data.id+"---"+data.name);
               }
           })
        });
    </script>
</head>
<body>

</body>
</html>
```
{: id="20210326221302-c4epihr"}

业务方法
{: id="20210326221302-4ljdxah"}

```java
@RequestMapping("/json")
public User json(@RequestBody User user){
    System.out.println(user);
    user.setId(6);
    user.setName("张六");
    return user;
}
```
{: id="20210326221302-wnl7qqj"}

Spring MVC 中的 JSON 和 JavaBean 的转换需要借助于 fastjson，pom.xml 引入相关依赖。
{: id="20210326221302-5n7xsaz"}

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.32</version>
</dependency>
```
{: id="20210326221302-gdv5lgm"}

springmvc.xml 添加 fastjson 配置。
{: id="20210326221302-77wqull"}

```xml
<mvc:annotation-driven>
    <!-- 消息转换器 -->
    <mvc:message-converters register-defaults="true">
        <bean class="org.springframework.http.converter.StringHttpMessageConverter">
            <property name="supportedMediaTypes" value="text/html;charset=UTF-8"></property>
        </bean>
        <!-- 配置fastjson -->
        <bean class="com.alibaba.fastjson.support.spring.FastJsonHttpMessageConverter4"></bean>
    </mvc:message-converters>
</mvc:annotation-driven>
```
{: id="20210326221302-55t7zh3"}

### Spring MVC 模型数据解析
{: id="20210326221302-e8m2kr7"}

JSP 四大作用域对应的内置对象：pageContext、request、session、application。
{: id="20210326221302-zjz9u23"}

模型数据的绑定是由 ViewResolver 来完成的，实际开发中，我们需要先添加模型数据，再交给 ViewResolver 来绑定。
{: id="20210326221302-pc5wkcl"}

Spring MVC 提供了以下几种方式添加模型数据：
{: id="20210326221302-25caoeo"}

- {: id="20210326221302-dd9sghx"}Map
  {: id="20210326221302-rmzote6"}
- {: id="20210326221302-qohjbta"}Model
  {: id="20210326221302-b7ljvyg"}
- {: id="20210326221302-9e1rf7d"}ModelAndView
  {: id="20210326221302-ietpi6p"}
- {: id="20210326221302-z8y3q9d"}@SessionAttribute
  {: id="20210326221302-nbq8e7i"}
- {: id="20210326221302-hqmptow"}@ModelAttribute
  {: id="20210326221302-7es8jj1"}
{: id="20210326221302-9zrhqqn"}

> 将模式数据绑定到 request 对象。
> {: id="20210326221302-8lm6fub"}
{: id="20210326221302-wi6zeet"}

1、Map
{: id="20210326221302-d8691l0"}

```java
@RequestMapping("/map")
public String map(Map<String,User> map){
    User user = new User();
    user.setId(1L);
    user.setName("张三");
    map.put("user",user);
    return "view";
}
```
{: id="20210326221302-iuqqt6j"}

JSP
{: id="20210326221302-0ddzlo0"}

```jsp
<%--
  Created by IntelliJ IDEA.
  User: southwind
  Date: 2019-03-14
  Time: 11:36
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ page isELIgnored="false" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    ${requestScope.user}
</body>
</html>
```
{: id="20210326221302-m0b2boq"}

2、Model
{: id="20210326221302-d2cngzb"}

```java
@RequestMapping("/model")
public String model(Model model){
    User user = new User();
    user.setId(1L);
    user.setName("张三");
    model.addAttribute("user",user);
    return "view";
}
```
{: id="20210326221302-pgzc7zc"}

3、ModelAndView
{: id="20210326221302-ntayghg"}

```java
@RequestMapping("/modelAndView")
public ModelAndView modelAndView(){
    User user = new User();
    user.setId(1L);
    user.setName("张三");
    ModelAndView modelAndView = new ModelAndView();
    modelAndView.addObject("user",user);
    modelAndView.setViewName("view");
    return modelAndView;
}

@RequestMapping("/modelAndView2")
public ModelAndView modelAndView2(){
    User user = new User();
    user.setId(1L);
    user.setName("张三");
    ModelAndView modelAndView = new ModelAndView();
    modelAndView.addObject("user",user);
    View view = new InternalResourceView("/view.jsp");
    modelAndView.setView(view);
    return modelAndView;
}

@RequestMapping("/modelAndView3")
public ModelAndView modelAndView3(){
    User user = new User();
    user.setId(1L);
    user.setName("张三");
    ModelAndView modelAndView = new ModelAndView("view");
    modelAndView.addObject("user",user);
    return modelAndView;
}

@RequestMapping("/modelAndView4")
public ModelAndView modelAndView4(){
    User user = new User();
    user.setId(1L);
    user.setName("张三");
    View view = new InternalResourceView("/view.jsp");
    ModelAndView modelAndView = new ModelAndView(view);
    modelAndView.addObject("user",user);
    return modelAndView;
}

@RequestMapping("/modelAndView5")
public ModelAndView modelAndView5(){
    User user = new User();
    user.setId(1L);
    user.setName("张三");
    Map<String,User> map = new HashMap<>();
    map.put("user",user);
    ModelAndView modelAndView = new ModelAndView("view",map);
    return modelAndView;
}

@RequestMapping("/modelAndView6")
public ModelAndView modelAndView6(){
    User user = new User();
    user.setId(1L);
    user.setName("张三");
    Map<String,User> map = new HashMap<>();
    map.put("user",user);
    View view = new InternalResourceView("/view.jsp");
    ModelAndView modelAndView = new ModelAndView(view,map);
    return modelAndView;
}

@RequestMapping("/modelAndView7")
public ModelAndView modelAndView7(){
    User user = new User();
    user.setId(1L);
    user.setName("张三");
    ModelAndView modelAndView = new ModelAndView("view","user",user);
    return modelAndView;
}

@RequestMapping("/modelAndView8")
public ModelAndView modelAndView8(){
    User user = new User();
    user.setId(1L);
    user.setName("张三");
    View view = new InternalResourceView("/view.jsp");
    ModelAndView modelAndView = new ModelAndView(view,"user",user);
    return modelAndView;
}
```
{: id="20210326221302-gcsjmvw"}

4、HttpServletRequest
{: id="20210326221302-f8uf06p"}

```java
@RequestMapping("/request")
public String request(HttpServletRequest request){
    User user = new User();
    user.setId(1L);
    user.setName("张三");
    request.setAttribute("user",user);
    return "view";
}
```
{: id="20210326221302-bg1xyws"}

5、@ModelAttribute
{: id="20210326221302-p9dfmkv"}

- {: id="20210326221302-tqhuiqz"}定义一个方法，该方法专门用来返回要填充到模型数据中的对象。
  {: id="20210326221302-ykdfq5k"}
{: id="20210326221302-0ai5ecy"}

```java
@ModelAttribute
public User getUser(){
    User user = new User();
    user.setId(1L);
    user.setName("张三");
    return user;
}
```
{: id="20210326221302-d7ogitq"}

```java
@ModelAttribute
public void getUser(Map<String,User> map){
    User user = new User();
    user.setId(1L);
    user.setName("张三");
    map.put("user",user);
}
```
{: id="20210326221302-ykus03s"}

```java
@ModelAttribute
public void getUser(Model model){
    User user = new User();
    user.setId(1L);
    user.setName("张三");
    model.addAttribute("user",user);
}
```
{: id="20210326221302-wkharxv"}

- {: id="20210326221302-xa21oh3"}业务方法中无需再处理模型数据，只需返回视图即可。
  {: id="20210326221302-5kjvgmu"}
{: id="20210326221302-7am3u72"}

```java
@RequestMapping("/modelAttribute")
public String modelAttribute(){
    return "view";
}
```
{: id="20210326221302-mvc6mud"}

> 将模型数据绑定到 session 对象
> {: id="20210326221302-ux6ojce"}
{: id="20210326221302-6cvxd43"}

1、直接使用原生的 Servlet API。
{: id="20210326221302-t5bp9ov"}

```java
@RequestMapping("/session")
public String session(HttpServletRequest request){
    HttpSession session = request.getSession();
    User user = new User();
    user.setId(1L);
    user.setName("张三");
    session.setAttribute("user",user);
    return "view";
}

@RequestMapping("/session2")
public String session2(HttpSession session){
    User user = new User();
    user.setId(1L);
    user.setName("张三");
    session.setAttribute("user",user);
    return "view";
}
```
{: id="20210326221302-djkbu7q"}

2、@SessionAttribute
{: id="20210326221302-we032bz"}

```java
@SessionAttributes(value = {"user","address"})
public class ViewHandler {
}
```
{: id="20210326221302-1tb6bx1"}

对于 ViewHandler 中的所有业务方法，只要向 request 中添加了 key = "user"、key = "address" 的对象时，Spring MVC 会自动将该数据添加到 session 中，保存 key 不变。
{: id="20210326221302-el0cc8x"}

```java
@SessionAttributes(types = {User.class,Address.class})
public class ViewHandler {
}
```
{: id="20210326221302-rt2uq7h"}

对于 ViewHandler 中的所有业务方法，只要向 request 中添加了数据类型是 User 、Address 的对象时，Spring MVC 会自动将该数据添加到 session 中，保存 key 不变。
{: id="20210326221302-q1xc8sm"}

> 将模型数据绑定到 application 对象
> {: id="20210326221302-wmouehr"}
{: id="20210326221302-vcj5hz0"}

```java
@RequestMapping("/application")
public String application(HttpServletRequest request){
    ServletContext application = request.getServletContext();
    User user = new User();
    user.setId(1L);
    user.setName("张三");
    application.setAttribute("user",user);
    return "view";
}
```
{: id="20210326221302-dlfz6dg"}

### Spring MVC 自定义数据转换器
{: id="20210326221302-rl9cy9z"}

数据转换器是指将客户端 HTTP 请求中的参数转换为业务方法中定义的形参，自定义表示开发者可以自主设计转换的方式，HandlerApdter 已经提供了通用的转换，String 转 int，String 转 double，表单数据的封装等，但是在特殊的业务场景下，HandlerAdapter 无法进行转换，就需要开发者自定义转换器。
{: id="20210326221302-pu2zfio"}

客户端输入 String 类型的数据 "2019-03-03"，自定义转换器将该数据转为 Date 类型的对象。
{: id="20210326221302-kcsektj"}

- {: id="20210326221302-y635dxw"}创建 DateConverter 转换器，实现 Conveter 接口。
  {: id="20210326221302-byzksei"}
{: id="20210326221302-7vz7csm"}

```java
package com.southwind.converter;

import org.springframework.core.convert.converter.Converter;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class DateConverter implements Converter<String, Date> {

    private String pattern;

    public DateConverter(String pattern){
        this.pattern = pattern;
    }

    @Override
    public Date convert(String s) {
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat(this.pattern);
        Date date = null;
        try {
            date = simpleDateFormat.parse(s);
        } catch (ParseException e) {
            e.printStackTrace();
        }
        return date;
    }
}
```
{: id="20210326221302-oanebg3"}

- {: id="20210326221302-iv4f82t"}springmvc.xml 配置转换器。
  {: id="20210326221302-uekcomp"}
{: id="20210326221302-mh5w5v9"}

```xml
<!-- 配置自定义转换器 -->
<bean id="conversionService" class="org.springframework.context.support.ConversionServiceFactoryBean">
    <property name="converters">
        <list>
            <bean class="com.southwind.converter.DateConverter">
                <constructor-arg type="java.lang.String" value="yyyy-MM-dd"></constructor-arg>
            </bean>
        </list>
    </property>
</bean>

<mvc:annotation-driven conversion-service="conversionService">
    <!-- 消息转换器 -->
    <mvc:message-converters register-defaults="true">
        <bean class="org.springframework.http.converter.StringHttpMessageConverter">
            <property name="supportedMediaTypes" value="text/html;charset=UTF-8"></property>
        </bean>
        <!-- 配置fastjson -->
        <bean class="com.alibaba.fastjson.support.spring.FastJsonHttpMessageConverter4"></bean>
    </mvc:message-converters>
</mvc:annotation-driven>
```
{: id="20210326221302-fcl52rh"}

- {: id="20210326221302-7fus4ap"}JSP
  {: id="20210326221302-bjrfu0i"}
{: id="20210326221302-l6taime"}

```jsp
<%--
  Created by IntelliJ IDEA.
  User: southwind
  Date: 2019-03-14
  Time: 14:47
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <form action="/converter/date" method="post">
        请输入日期:<input type="text" name="date"/>(yyyy-MM-dd)<br/>
        <input type="submit" value="提交"/>
    </form>
</body>
</html>
```
{: id="20210326221302-4nduf99"}

- {: id="20210326221302-c09y8jh"}Handler
  {: id="20210326221302-1mtfvtu"}
{: id="20210326221302-329qhk6"}

```java
package com.southwind.controller;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.Date;

@RestController
@RequestMapping("/converter")
public class ConverterHandler {

    @RequestMapping("/date")
    public String date(Date date){
        return date.toString();
    }
}
```
{: id="20210326221302-8cupgmc"}

String 转 Student
{: id="20210326221302-ztiijs5"}

StudentConverter
{: id="20210326221302-1rj617t"}

```java
package com.southwind.converter;

import com.southwind.entity.Student;
import org.springframework.core.convert.converter.Converter;

public class StudentConverter implements Converter<String, Student> {
    @Override
    public Student convert(String s) {
        String[] args = s.split("-");
        Student student = new Student();
        student.setId(Long.parseLong(args[0]));
        student.setName(args[1]);
        student.setAge(Integer.parseInt(args[2]));
        return student;
    }
}
```
{: id="20210326221302-y0qjhfr"}

springmvc.xml
{: id="20210326221302-znldwx0"}

```xml
<!-- 配置自定义转换器 -->
<bean id="conversionService" class="org.springframework.context.support.ConversionServiceFactoryBean">
    <property name="converters">
        <list>
            <bean class="com.southwind.converter.DateConverter">
                <constructor-arg type="java.lang.String" value="yyyy-MM-dd"></constructor-arg>
            </bean>
            <bean class="com.southwind.converter.StudentConverter"></bean>
        </list>
    </property>
</bean>

<mvc:annotation-driven conversion-service="conversionService">
    <!-- 消息转换器 -->
    <mvc:message-converters register-defaults="true">
        <bean class="org.springframework.http.converter.StringHttpMessageConverter">
            <property name="supportedMediaTypes" value="text/html;charset=UTF-8"></property>
        </bean>
        <!-- 配置fastjson -->
        <bean class="com.alibaba.fastjson.support.spring.FastJsonHttpMessageConverter4"></bean>
    </mvc:message-converters>
</mvc:annotation-driven>
```
{: id="20210326221302-n6ixzqk"}

JSP
{: id="20210326221302-rscnrxk"}

```jsp
<%--
  Created by IntelliJ IDEA.
  User: southwind
  Date: 2019-03-14
  Time: 15:23
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <form action="/converter/student" method="post">
        请输入学生信息：<input type="text" name="student"/>(id-name-age)<br/>
        <input type="submit" value="提交"/>
    </form>
</body>
</html>
```
{: id="20210326221302-xa0wqjb"}

Handler
{: id="20210326221302-fs88x8j"}

```java
@RequestMapping("/student")
public String student(Student student){
    return student.toString();
}
```
{: id="20210326221302-imi08o3"}

### Spring MVC REST
{: id="20210326221302-9gxk8z2"}

REST：Representational State Transfer，资源表现层状态转换，是目前比较主流的一种互联网软件架构，它结构清晰、标准规范、易于理解、便于扩展。
{: id="20210326221302-zmxmjj2"}

- {: id="20210326221302-2pnusc1"}资源（Resource）
  {: id="20210326221302-k2ngt9h"}
{: id="20210326221302-3hvsb13"}

网络上的一个实体，或者说网络中存在的一个具体信息，一段文本、一张图片、一首歌曲、一段视频等等，总之就是一个具体的存在。可以用一个 URI（统一资源定位符）指向它，每个资源都有对应的一个特定的 URI，要获取该资源时，只需要访问对应的 URI 即可。
{: id="20210326221302-urqi8ti"}

- {: id="20210326221302-ar9y6hh"}表现层（Representation）
  {: id="20210326221302-97mf3vf"}
{: id="20210326221302-55yl8de"}

资源具体呈现出来的形式，比如文本可以用 txt 格式表示，也可以用 HTML、XML、JSON等格式来表示。
{: id="20210326221302-8nldy52"}

- {: id="20210326221302-e74dn1y"}状态转换（State Transfer）
  {: id="20210326221302-d9wx8nl"}
{: id="20210326221302-gvvgi7f"}

客户端如果希望操作服务器中的某个资源，就需要通过某种方式让服务端发生状态转换，而这种转换是建立在表现层之上的，所有叫做"表现层状态转换"。
{: id="20210326221302-o6uadig"}

#### 特点
{: id="20210326221302-h8xlswq"}

- {: id="20210326221302-plxkjhf"}URL 更加简洁。
  {: id="20210326221302-0idhcri"}
- {: id="20210326221302-yi8cehw"}有利于不同系统之间的资源共享，只需要遵守一定的规范，不需要进行其他配置即可实现资源共享。
  {: id="20210326221302-3o2fu0a"}
{: id="20210326221302-mg3uriu"}

#### 如何使用
{: id="20210326221302-izqt8kt"}

REST 具体操作就是 HTTP 协议中四个表示操作方式的动词分别对应 CRUD 基本操作。
{: id="20210326221302-3y0z5o8"}

GET 用来表示获取资源。
{: id="20210326221302-m7kldqx"}

POST 用来表示新建资源。
{: id="20210326221302-uszz43i"}

PUT 用来表示修改资源。
{: id="20210326221302-vcor1yg"}

DELETE 用来表示删除资源。
{: id="20210326221302-12xwold"}

Handler
{: id="20210326221302-shqpeqs"}

```java
package com.southwind.controller;

import com.southwind.entity.Student;
import com.southwind.entity.User;
import com.southwind.repository.StudentRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Repository;
import org.springframework.web.bind.annotation.*;

import javax.servlet.http.HttpServletResponse;
import java.util.Collection;

@RestController
@RequestMapping("/rest")
public class RESTHandeler {

    @Autowired
    private StudentRepository studentRepository;

    @GetMapping("/findAll")
    public Collection<Student> findAll(HttpServletResponse response){
        response.setContentType("text/json;charset=UTF-8");
        return studentRepository.findAll();
    }

    @GetMapping("/findById/{id}")
    public Student findById(@PathVariable("id") long id){
        return studentRepository.findById(id);
    }

    @PostMapping("/save")
    public void save(@RequestBody Student student){
        studentRepository.saveOrUpdate(student);
    }

    @PutMapping("/update")
    public void update(@RequestBody Student student){
        studentRepository.saveOrUpdate(student);
    }

    @DeleteMapping("/deleteById/{id}")
    public void deleteById(@PathVariable("id") long id){
        studentRepository.deleteById(id);
    }

}
```
{: id="20210326221302-60uv0u0"}

StudentRepository
{: id="20210326221302-hsgqw76"}

```java
package com.southwind.repository;

import com.southwind.entity.Student;

import java.util.Collection;

public interface StudentRepository {
    public Collection<Student> findAll();
    public Student findById(long id);
    public void saveOrUpdate(Student student);
    public void deleteById(long id);
}
```
{: id="20210326221302-iearv3q"}

StudentRepositoryImpl
{: id="20210326221302-0xrkrif"}

```java
package com.southwind.repository.impl;

import com.southwind.entity.Student;
import com.southwind.repository.StudentRepository;
import org.springframework.stereotype.Repository;

import java.util.Collection;
import java.util.HashMap;
import java.util.Map;

@Repository
public class StudentRepositoryImpl implements StudentRepository {

    private static Map<Long,Student> studentMap;

    static{
        studentMap = new HashMap<>();
        studentMap.put(1L,new Student(1L,"张三",22));
        studentMap.put(2L,new Student(2L,"李四",23));
        studentMap.put(3L,new Student(3L,"王五",24));
    }

    @Override
    public Collection<Student> findAll() {
        return studentMap.values();
    }

    @Override
    public Student findById(long id) {
        return studentMap.get(id);
    }

    @Override
    public void saveOrUpdate(Student student) {
        studentMap.put(student.getId(),student);
    }

    @Override
    public void deleteById(long id) {
        studentMap.remove(id);
    }
}
```
{: id="20210326221302-vdey1iu"}

### Spring MVC 文件上传下载
{: id="20210326221302-mxxmddo"}

> 单文件上传
> {: id="20210326221302-ra3f8p1"}
{: id="20210326221302-xkytj6z"}

底层是使用 Apache fileupload 组件完成上传，Spring MVC 对这种方式进行了封装。
{: id="20210326221302-vjnmirw"}

- {: id="20210326221302-mvdr836"}pom.xml
  {: id="20210326221302-uziun4c"}
{: id="20210326221302-e3463br"}

```xml
<dependency>
    <groupId>commons-io</groupId>
    <artifactId>commons-io</artifactId>
    <version>2.5</version>
</dependency>

<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.3.3</version>
</dependency>
```
{: id="20210326221302-w4ka6nk"}

- {: id="20210326221302-crhnr85"}JSP
  {: id="20210326221302-tkehn0d"}
{: id="20210326221302-6wuc6iq"}

```jsp
<%--
  Created by IntelliJ IDEA.
  User: southwind
  Date: 2019-03-15
  Time: 09:09
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ page isELIgnored="false" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <form action="/file/upload" method="post" enctype="multipart/form-data">
        <input type="file" name="img"/>
        <input type="submit" value="上传"/>
    </form>
    <img src="${path}">
</body>
</html>
```
{: id="20210326221302-g37m7eh"}

1、input 的 type 设置为 file。
{: id="20210326221302-ku5e01j"}

2、form 的 method 设置为 post（get 请求只能将文件名传给服务器）
{: id="20210326221302-yq4ova6"}

3、from 的 enctype 设置为 multipart-form-data（如果不设置只能将文件名传给服务器）
{: id="20210326221302-r6qlbl0"}

- {: id="20210326221302-5gk5etp"}Handler
  {: id="20210326221302-ukkeugi"}
{: id="20210326221302-j83iylp"}

```java
package com.southwind.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.multipart.MultipartFile;

import javax.servlet.http.HttpServletRequest;
import java.io.File;
import java.io.IOException;

@Controller
@RequestMapping("/file")
public class FileHandler {

    @PostMapping("/upload")
    public String upload(MultipartFile img, HttpServletRequest request){
        if(img.getSize()>0){
            //获取保存上传文件的file路径
            String path = request.getServletContext().getRealPath("file");
            //获取上传的文件名
            String name = img.getOriginalFilename();
            File file = new File(path,name);
            try {
                img.transferTo(file);
                //保存上传之后的文件路径
                request.setAttribute("path","/file/"+name);
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        return "upload";
    }
}
```
{: id="20210326221302-3oz7egi"}

- {: id="20210326221302-x8ptkrj"}springmvc.xml
  {: id="20210326221302-pqvwjhc"}
{: id="20210326221302-23u0cx8"}

```xml
<!-- 配置上传组件 -->
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver"></bean>
```
{: id="20210326221302-4tbzz05"}

- {: id="20210326221302-3qwkf40"}web.xml 添加如下配置，否则客户端无法访问 png
  {: id="20210326221302-octj4kf"}
{: id="20210326221302-t6s6w8d"}

```xml
<servlet-mapping>
    <servlet-name>default</servlet-name>
    <url-pattern>*.png</url-pattern>
</servlet-mapping>
```
{: id="20210326221302-62hb0zb"}

> 多文件上传
> {: id="20210326221302-j5a5wt8"}
{: id="20210326221302-y7g3xvh"}

pom.xml
{: id="20210326221302-7kn5k3i"}

```xml
<dependency>
    <groupId>jstl</groupId>
    <artifactId>jstl</artifactId>
    <version>1.2</version>
</dependency>

<dependency>
    <groupId>taglibs</groupId>
    <artifactId>standard</artifactId>
    <version>1.1.2</version>
</dependency>
```
{: id="20210326221302-dcmkhbd"}

JSP
{: id="20210326221302-ljhufkj"}

```jsp
<%--
  Created by IntelliJ IDEA.
  User: southwind
  Date: 2019-03-15
  Time: 09:32
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ page isELIgnored="false" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <form action="/file/uploads" method="post" enctype="multipart/form-data">
        file1:<input type="file" name="imgs"/><br/>
        file2:<input type="file" name="imgs"/><br/>
        file3:<input type="file" name="imgs"><br/>
        <input type="submit" value="上传"/>
    </form>
    <c:forEach items="${files}" var="file" >
        <img src="${file}" width="300px">
    </c:forEach>
</body>
</html>
```
{: id="20210326221302-s0aq47y"}

Handler
{: id="20210326221302-9sshuvr"}

```java
@PostMapping("/uploads")
public String uploads(MultipartFile[] imgs,HttpServletRequest request){
    List<String> files = new ArrayList<>();
    for (MultipartFile img:imgs){
        if(img.getSize()>0){
            //获取保存上传文件的file路径
            String path = request.getServletContext().getRealPath("file");
            //获取上传的文件名
            String name = img.getOriginalFilename();
            File file = new File(path,name);
            try {
                img.transferTo(file);
                //保存上传之后的文件路径
                files.add("/file/"+name);
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
    request.setAttribute("files",files);
    return "uploads";
}
```
{: id="20210326221302-nkm94ao"}

> 下载
> {: id="20210326221302-nxl4pvo"}
{: id="20210326221302-1u2er02"}

- {: id="20210326221302-rgx2xcc"}JSP
  {: id="20210326221302-2syv4dk"}
{: id="20210326221302-okwu16w"}

```jsp
<%--
  Created by IntelliJ IDEA.
  User: southwind
  Date: 2019-03-15
  Time: 10:36
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <a href="/file/download/1">1.png</a>
    <a href="/file/download/2">2.png</a>
    <a href="/file/download/3">3.png</a>
</body>
</html>
```
{: id="20210326221302-k1f3yyb"}

- {: id="20210326221302-wjg85nw"}Handler
  {: id="20210326221302-ige7lzr"}
{: id="20210326221302-2hcuj4y"}

```java
@GetMapping("/download/{name}")
public void download(@PathVariable("name") String name, HttpServletRequest request, HttpServletResponse response){
    if(name != null){
        name += ".png";
        String path = request.getServletContext().getRealPath("file");
        File file = new File(path,name);
        OutputStream outputStream = null;
        if(file.exists()){
            response.setContentType("application/forc-download");
            response.setHeader("Content-Disposition","attachment;filename="+name);
            try {
                outputStream = response.getOutputStream();
                outputStream.write(FileUtils.readFileToByteArray(file));
                outputStream.flush();
            } catch (IOException e) {
                e.printStackTrace();
            } finally {
                if(outputStream != null){
                    try {
                        outputStream.close();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }
            }
        }
    }
}
```
{: id="20210326221302-92xslsh"}

### Spring MVC 表单标签库
{: id="20210326221302-uipirwf"}

- {: id="20210326221302-fooftg9"}Handler
  {: id="20210326221302-nuxd8lz"}
{: id="20210326221302-sugkpfs"}

```java
@GetMapping("/get")
public ModelAndView get(){
    ModelAndView modelAndView = new ModelAndView("tag");
    Student student = new Student(1L,"张三",22);
    modelAndView.addObject("student",student);
    return modelAndView;
}
```
{: id="20210326221302-4vl1218"}

- {: id="20210326221302-5xs05ou"}JSP
  {: id="20210326221302-omzyyga"}
{: id="20210326221302-r6znyr1"}

```jsp
<%--
  Created by IntelliJ IDEA.
  User: southwind
  Date: 2019-03-15
  Time: 10:53
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ page isELIgnored="false" %>
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <h1>学生信息</h1>
    <form:form modelAttribute="student">
        学生ID：<form:input path="id"/><br/>
        学生姓名：<form:input path="name"/><br/>
        学生年龄：<form:input path="age"/><br/>
        <input type="submit" value="提交"/>
    </form:form>
</body>
</html>
```
{: id="20210326221302-mbqsvf8"}

1、JSP 页面导入 Spring MVC 表单标签库，与导入 JSTL 标签库的语法非常相似，前缀 prefix 可以自定义，通常定义为 from。
{: id="20210326221302-gl9mq5t"}

```jsp
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>
```
{: id="20210326221302-42fjedk"}

2、将 form 表单与模型数据进行绑定，通过 modelAttribute 属性完成绑定，将 modelAttribute 的值设置为模型数据对应的 key 值。
{: id="20210326221302-clzhn9l"}

```java
Handeler:modelAndView.addObject("student",student);
JSP:<form:form modelAttribute="student">
```
{: id="20210326221302-vkvw3lu"}

3、form 表单完成绑定之后，将模型数据的值取出绑定到不同的标签中，通过设置标签的 path 属性完成，将 path 属性的值设置为模型数据对应的属性名即可。
{: id="20210326221302-kg7ykzl"}

```jsp
学生ID：<form:input path="id"/><br/>
学生姓名：<form:input path="name"/><br/>
学生年龄：<form:input path="age"/><br/>
```
{: id="20210326221302-imb0yzq"}

#### 常用的表单标签
{: id="20210326221302-gefkncx"}

- {: id="20210326221302-tzxx2n8"}from
  {: id="20210326221302-rurzbmv"}
{: id="20210326221302-9kbfxpg"}

```jsp
<form:from modelAttribute="student"/>
```
{: id="20210326221302-u82bl9u"}

渲染的是 HTML 中的`<form></from>`，通过 modelAttribute 属性绑定具体的模型数据。
{: id="20210326221302-qrkhnfr"}

- {: id="20210326221302-gn81rzt"}input
  {: id="20210326221302-uvro1ln"}
{: id="20210326221302-rkcj9kt"}

```jsp
<form:input path="name"/>
```
{: id="20210326221302-rlfkmh5"}

渲染的是 HTML 中的 `<input type="text"/>`，from 标签绑定的是模型数据，input 标签绑定的是模型数据中的属性值，通过 path 属性可以与模型数据中的属性名对应，并且支持及联操作。
{: id="20210326221302-ciryyk2"}

```jsp
<from:input path="address.name"/>
```
{: id="20210326221302-usv1s44"}

- {: id="20210326221302-fxw5ujp"}password
  {: id="20210326221302-k3bc5jh"}
{: id="20210326221302-1jpc6o4"}

```jsp
<form:password path="password"/>
```
{: id="20210326221302-06mk8nf"}

渲染的是 HTML 中的 `<input type="password"/>`，通过 path 属性与模型数据的属性值进行绑定，password 标签的值不会在页面显示。
{: id="20210326221302-t0lj5mp"}

- {: id="20210326221302-ta3n3aw"}checkbox
  {: id="20210326221302-l6krq6b"}
{: id="20210326221302-9bwxkjw"}

```jsp
<form:checkbox path="hobby" value="读书"/>
```
{: id="20210326221302-1wxd2is"}

```java
student.setFlag(false);
```
{: id="20210326221302-pqbmauo"}

```jsp
checkbox：<form:checkbox path="flag" value="flag"></form:checkbox><br/>
```
{: id="20210326221302-ny0riee"}

渲染的是 HTML 中的 `<input type="checkbox"/>`，通过 path 与模型数据的属性值进行绑定，可以绑定 boolean、数组和集合。
{: id="20210326221302-7e5tc2n"}

如果绑定 boolean 值，若该变量的值为 true，则表示该复选框选中，否则表示不选中。
{: id="20210326221302-ccfgxzi"}

如果绑定数组或者集合，数组/集合中的元素等于 checkbox 的 value 值，则选中。
{: id="20210326221302-cdf3pk9"}

```java
student.setHobby(Arrays.asList("读书","看电影","玩游戏"));
modelAndView.addObject("student",student);
```
{: id="20210326221302-49il676"}

```jsp
爱好：<form:checkbox path="hobby" value="摄影"></form:checkbox>摄影<br/>
<form:checkbox path="hobby" value="读书"></form:checkbox>读书<br/>
<form:checkbox path="hobby" value="听音乐"></form:checkbox>听音乐<br/>
<form:checkbox path="hobby" value="看电影"></form:checkbox>看电影<br/>
<form:checkbox path="hobby" value="旅游"></form:checkbox>旅游<br/>
<form:checkbox path="hobby" value="玩游戏"></form:checkbox>玩游戏<br/>
<input type="submit" value="提交"/>
```
{: id="20210326221302-bnxkjdn"}

- {: id="20210326221302-bxenecq"}checkboxes
  {: id="20210326221302-0ss6jlv"}
{: id="20210326221302-efsi49w"}

```jsp
<form:checkboxes items=${student.hobby} path="selecHobby"/>
```
{: id="20210326221302-599eewd"}

渲染的是 HTML 中的一组 `<input type="checkbox"/>`，是对 `<form:checkbox/>` 的一种简化，需要结合 items 和 path 属性来使用，items 绑定被遍历的集合或数组，path 绑定被选中的集合或数组，可以这样理解，items 为全部可选集合，path 为默认的选中集合。
{: id="20210326221302-h0que0u"}

```java
student.setHobby(Arrays.asList("摄影","读书","听音乐","看电影","旅游","玩游戏"));
student.setSelectHobby(Arrays.asList("摄影","读书","听音乐"));
modelAndView.addObject("student",student);
```
{: id="20210326221302-hs52ec7"}

```jsp
爱好：<form:checkboxes path="selectHobby" items="${student.hobby}"/><br/>
```
{: id="20210326221302-si0dl0v"}

需要注意的是 path 可以直接绑定模型数据的属性值，items 则需要通过 EL 表达式的形式从域对象中获取数据，不能直接写属性名。
{: id="20210326221302-8134h38"}

- {: id="20210326221302-lbhk1xg"}rabiobutton
  {: id="20210326221302-ssdp83c"}
{: id="20210326221302-p8pjp3t"}

```jsp
<from:radiobutton path="radioId" value="0"/>
```
{: id="20210326221302-w2uwncx"}

渲染的是 HTML 中的一个 `<input type="radio"/>`，绑定的数据与标签的 value 值相等则为选中，否则不选中。
{: id="20210326221302-lscrjfn"}

```java
student.setRadioId(1);
modelAndView.addObject("student",student);
```
{: id="20210326221302-har5728"}

```jsp
radiobutton:<form:radiobutton path="radioId" value="1"/>radiobutton<br/>
```
{: id="20210326221302-jdyfx8l"}

- {: id="20210326221302-kzvkg6d"}radiobuttons
  {: id="20210326221302-sr9fplz"}
{: id="20210326221302-8zhupw2"}

```jsp
<form:radiobuttons itmes="${student.grade}" path="selectGrade"/>
```
{: id="20210326221302-aqo1agr"}

渲染的是 HTML 中的一组 `<input type="radio"/>`，这里需要结合 items 和 path 两个属性来使用，items 绑定被遍历的集合或数组，path 绑定被选中的值，items 为全部的可选类型，path 为默认选中的选项，用法与 `<form:checkboxes/>` 一致。
{: id="20210326221302-4hkwval"}

```java
Map<Integer,String> gradeMap = new HashMap<>();
gradeMap.put(1,"一年级");
gradeMap.put(2,"二年级");
gradeMap.put(3,"三年级");
gradeMap.put(4,"四年级");
gradeMap.put(5,"五年级");
gradeMap.put(6,"六年级");
student.setGradeMap(gradeMap);
student.setSelectGrade(3);
modelAndView.addObject("student",student);
```
{: id="20210326221302-ff5ue86"}

```jsp
学生年级：<form:radiobuttons items="${student.gradeMap}" path="selectGrade"/><br/>
```
{: id="20210326221302-l8e5c6x"}

- {: id="20210326221302-nim3ibl"}select
  {: id="20210326221302-wspqcq3"}
{: id="20210326221302-bawq3eh"}

```jsp
<form:select items="${student.citys}" path="selectCity"/>
```
{: id="20210326221302-so4tpc8"}

渲染的是 HTML 中的一个 `<select/>` 标签，需要结合 items 和 path 两个属性来使用，items 绑定被遍历的集合或数组，path 绑定被选中的值，用法与 `<from:radiobuttons/>`一致。
{: id="20210326221302-3q5bb5m"}

```java
Map<Integer,String> cityMap = new HashMap<>();
cityMap.put(1,"北京");
cityMap.put(2,"上海");
cityMap.put(3,"广州");
cityMap.put(4,"深圳");
student.setCityMap(cityMap);
student.setSelectCity(3);
modelAndView.addObject("student",student);
```
{: id="20210326221302-6wdyaiy"}

```jsp
所在城市：<form:select items="${student.cityMap}" path="selectCity"></form:select><br/>
```
{: id="20210326221302-q4dciu3"}

- {: id="20210326221302-tulqymb"}options
  {: id="20210326221302-v8bzedb"}
{: id="20210326221302-v8u42pf"}

`form:select` 结合 `form:options` 的使用，`from:select` 只定义 path 属性，在 `form:select` 标签内部添加一个子标签 `form:options` ，设置 items 属性，获取被遍历的集合。
{: id="20210326221302-q477wv9"}

```jsp
所在城市：<form:select path="selectCity">
  				<form:options items="${student.cityMap}"></form:options>
				</form:select><br/>
```
{: id="20210326221302-uro6426"}

- {: id="20210326221302-tmgfvao"}option
  {: id="20210326221302-mwayl5o"}

  `form:select` 结合 `form:option` 的使用，`from:select` 定义 path 属性，给每一个 `form:option` 设置 value 值，path 的值与哪个 value 值相等，该项默认选中。
  {: id="20210326221302-j8kbmwu"}
{: id="20210326221302-bxl42dv"}

```jsp
所在城市：<form:select path="selectCity">
            <form:option value="1">杭州</form:option>
            <form:option value="2">成都</form:option>
            <form:option value="3">西安</form:option>
        </form:select><br/>
```
{: id="20210326221302-8z5xvrw"}

- {: id="20210326221302-tskmawh"}textarea
  {: id="20210326221302-un9ezby"}
{: id="20210326221302-b0qw0ib"}

渲染的是 HTML 中的一个 `<textarea/>` ，path 绑定模型数据的属性值，作为文本输入域的默认值。
{: id="20210326221302-soi0cds"}

```java
student.setIntroduce("你好，我是...");
modelAndView.addObject("student",student);
```
{: id="20210326221302-586cdnb"}

```jsp
信息：<form:textarea path="introduce"/><br/>
```
{: id="20210326221302-hj52qjg"}

- {: id="20210326221302-y3hixhr"}errors
  {: id="20210326221302-vc3f88f"}
{: id="20210326221302-i73u8cu"}

处理错误信息，一般用在数据校验，该标签需要结合 Spring MVC 的验证器结合起来使用。
{: id="20210326221302-zfs81f5"}

### Spring MVC 数据校验
{: id="20210326221302-xpke9ne"}

Spring MVC 提供了两种数据校验的方式：1、基于 Validator 接口。2、使用 Annotation JSR - 303 标准进行校验。
{: id="20210326221302-947lmty"}

基于 Validator 接口的方式需要自定义 Validator 验证器，每一条数据的验证规则需要开发者手动完成，使用 Annotation JSR - 303 标准则不需要自定义验证器，通过注解的方式可以直接在实体类中添加每个属性的验证规则，这种方式更加方便，实际开发中推荐使用。
{: id="20210326221302-t20n97y"}

> 基于 Validator 接口
> {: id="20210326221302-wmy77u0"}
{: id="20210326221302-f3rq78e"}

- {: id="20210326221302-itgt8ph"}实体类 Account
  {: id="20210326221302-bs2kwrz"}
{: id="20210326221302-vitn7v1"}

```java
package com.southwind.entity;

import lombok.Data;

@Data
public class Account {
    private String name;
    private String password;
}
```
{: id="20210326221302-h0mm4cq"}

- {: id="20210326221302-ozisq43"}自定义验证器 AccountValidator，实现 Validator 接口。
  {: id="20210326221302-di8stk9"}
{: id="20210326221302-9boq6zb"}

```java
package com.southwind.validator;

import com.southwind.entity.Account;
import org.springframework.validation.Errors;
import org.springframework.validation.ValidationUtils;
import org.springframework.validation.Validator;

public class AccountValidator implements Validator {
    @Override
    public boolean supports(Class<?> aClass) {
        return Account.class.equals(aClass);
    }

    @Override
    public void validate(Object o, Errors errors) {
        ValidationUtils.rejectIfEmpty(errors,"name",null,"姓名不能为空");
        ValidationUtils.rejectIfEmpty(errors,"password",null,"密码不能为空");
    }
}
```
{: id="20210326221302-54ukw26"}

- {: id="20210326221302-gmdd8h6"}控制器
  {: id="20210326221302-3iin43b"}
{: id="20210326221302-b3f5vro"}

```java
package com.southwind.controller;

import com.southwind.entity.Account;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.validation.BindingResult;
import org.springframework.validation.annotation.Validated;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/validator")
public class ValidatorHandler {

    @GetMapping("/login")
    public String login(Model model){
        model.addAttribute("account",new Account());
        return "login";
    }

    @PostMapping("/login")
    public String login(@Validated Account account, BindingResult bindingResult){
        if(bindingResult.hasErrors()){
            return "login";
        }
        return "index";
    }
}
```
{: id="20210326221302-04cyhv4"}

- {: id="20210326221302-do97nce"}springmvc.xml 配置验证器。
  {: id="20210326221302-wx7fsux"}
{: id="20210326221302-tm9iw22"}

```xml
<bean id="accountValidator" class="com.southwind.validator.AccountValidator"></bean>
<mvc:annotation-driven validator="accountValidator"></mvc:annotation-driven>
```
{: id="20210326221302-k1v0b15"}

- {: id="20210326221302-ebjic02"}JSP
  {: id="20210326221302-1fj63st"}
{: id="20210326221302-wk0tdxs"}

```jsp
<%--
  Created by IntelliJ IDEA.
  User: southwind
  Date: 2019-03-18
  Time: 10:31
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ page isELIgnored="false" %>
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>
<%@ taglib prefix="from" uri="http://www.springframework.org/tags/form" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <form:form modelAttribute="account" action="/validator/login" method="post">
        姓名：<form:input path="name"/><from:errors path="name"></from:errors><br/>
        密码：<form:input path="password"/><from:errors path="password"></from:errors><br/>
        <input type="submit" value="登录"/>
    </form:form>
</body>
</html>
```
{: id="20210326221302-dqy5ame"}

> Annotation JSR - 303 标准
> {: id="20210326221302-83hoq52"}
{: id="20210326221302-hewhnuy"}

使用 Annotation JSR - 303 标准进行验证，需要导入支持这种标准的依赖 jar 文件，这里我们使用 Hibernate Validator。
{: id="20210326221302-ve6e6tu"}

- {: id="20210326221302-a02ke0d"}pom.xml
  {: id="20210326221302-tydcge9"}
{: id="20210326221302-cthkon0"}

```xml
<!-- JSR-303 -->
<dependency>
  <groupId>org.hibernate</groupId>
  <artifactId>hibernate-validator</artifactId>
  <version>5.3.6.Final</version>
</dependency>

<dependency>
  <groupId>javax.validation</groupId>
  <artifactId>validation-api</artifactId>
  <version>2.0.1.Final</version>
</dependency>

<dependency>
  <groupId>org.jboss.logging</groupId>
  <artifactId>jboss-logging</artifactId>
  <version>3.3.2.Final</version>
</dependency>
```
{: id="20210326221302-zlz7hc7"}

- {: id="20210326221302-x97dy1u"}通过注解的方式直接在实体类中添加相关的验证规则。
  {: id="20210326221302-tnlu1yx"}
{: id="20210326221302-kzhr10g"}

```java
package com.southwind.entity;

import lombok.Data;
import org.hibernate.validator.constraints.Email;
import org.hibernate.validator.constraints.NotEmpty;
import javax.validation.constraints.Pattern;
import javax.validation.constraints.Size;

@Data
public class Person {
    @NotEmpty(message = "用户名不能为空")
    private String username;
    @Size(min = 6,max = 12,message = "密码6-12位")
    private String password;
    @Email(regexp = "^[a-zA-Z0-9_.-]+@[a-zA-Z0-9-]+(\\\\.[a-zA-Z0-9-]+)*\\\\.[a-zA-Z0-9]{2,6}$",message = "请输入正确的邮箱格式")
    private String email;
    @Pattern(regexp = "^((13[0-9])|(14[5|7])|(15([0-3]|[5-9]))|(18[0,5-9]))\\\\\\\\d{8}$",message = "请输入正确的电话")
    private String phone;
}
```
{: id="20210326221302-jrh9z3g"}

- {: id="20210326221302-ze9r6dd"}ValidatorHandler
  {: id="20210326221302-639oorf"}
{: id="20210326221302-5jczhe3"}

```java
@GetMapping("/register")
public String register(Model model){
    model.addAttribute("person",new Person());
    return "register";
}

@PostMapping("/register")
public String register(@Valid Person person, BindingResult bindingResult){
    if(bindingResult.hasErrors()){
        return "register";
    }
    return "index";
}
```
{: id="20210326221302-d7orvq1"}

- {: id="20210326221302-5kqutya"}springmvc.xml
  {: id="20210326221302-ard9j4p"}
{: id="20210326221302-aq59u2r"}

```xml
<mvc:annotation-driven />
```
{: id="20210326221302-iz56zn2"}

- {: id="20210326221302-56fnaxv"}JSP
  {: id="20210326221302-laujunr"}
{: id="20210326221302-880vmzx"}

```jsp
<%--
  Created by IntelliJ IDEA.
  User: southwind
  Date: 2019-03-18
  Time: 11:29
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ page isELIgnored="false" %>
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <form:form modelAttribute="person" action="/validator/register2" method="post">
        用户名：<form:input path="username"></form:input><form:errors path="username"/><br/>
        密码：<form:password path="password"></form:password><form:errors path="password"/><br/>
        邮箱：<form:input path="email"></form:input><form:errors path="email"/><br/>
        电话：<form:input path="phone"></form:input><form:errors path="phone"/><br/>
        <input type="submit" value="提交"/>
    </form:form>
</body>
</html>
```
{: id="20210326221302-5ujrq0h"}

校验规则详解：
{: id="20210326221302-mjlgjv1"}

@Null					被注解的元素必须为null
{: id="20210326221302-yikf313"}

@NotNull				  被注解的元素不能为null
{: id="20210326221302-z1w5q7i"}

@Min(value)			     被注解的元素必须是一个数字，其值必须大于等于指定的最小值
{: id="20210326221302-5l3wmq0"}

@Max(value)			    被注解的元素必须是一个数字，其值必须小于于等于指定的最大值
{: id="20210326221302-0qvfgbx"}

@Email				     被注解的元素必须是电子邮箱地址
{: id="20210326221302-igti6oz"}

@Pattern				  被注解的元素必须符合对应的正则表达式
{: id="20210326221302-j9614xu"}

@Length				   被注解的元素的大小必须在指定的范围内
{: id="20210326221302-y2b3qw5"}

@NotEmpty			      被注解的字符串的值必须非空
{: id="20210326221302-fox1rip"}

Null 和 Empty 是不同的结果，String str = null，str 是 null，String str = ""，str 不是 null，其值为空。
{: id="20210326221302-7oy2rub"}


{: id="20210326221302-26odznr" type="doc"}
