这篇文章是我根据官方文档以及自己平时的使用情况，对 Dubbo 所做的一个总结。欢迎补充！
{: id="20210330211656-pxt9qjw"}

## RPC基础
{: id="20210330211656-j493nll"}

### 何为 RPC?
{: id="20210330211656-1pshdb5"}

**RPC（Remote Procedure Call）** 即远程过程调用，通过名字我们就能看出 RPC 关注的是远程调用而非本地调用。
{: id="20210330211656-fqxj8da"}

**为什么要 RPC  ？** 因为，两个不同的服务器上的服务提供的方法不在一个内存空间，所以，需要通过网络编程才能传递方法调用所需要的参数。并且，方法调用的结果也需要通过网络编程来接收。但是，如果我们自己手动网络编程来实现这个调用过程的话工作量是非常大的，因为，我们需要考虑底层传输方式（TCP还是UDP）、序列化方式等等方面。
{: id="20210330211656-hobhg8x"}

**RPC 能帮助我们做什么呢？ ** 简单来说，通过 RPC 可以帮助我们调用远程计算机上某个服务的方法，这个过程就像调用本地方法一样简单。并且！我们不需要了解底层网络编程的具体细节。
{: id="20210330211656-5k8bbbj"}

举个例子：两个不同的服务 A、B 部署在两台不同的机器上，服务 A 如果想要调用服务 B 中的某个方法的话就可以通过 RPC 来做。
{: id="20210330211656-4k93hf5"}

一言蔽之：**RPC 的出现就是为了让你调用远程方法像调用本地方法一样简单。**
{: id="20210330211656-6wsqpcs"}

### RPC 的原理是什么?
{: id="20210330211656-gb7sipx"}

为了能够帮助小伙伴们理解 RPC 原理，我们可以将整个 RPC的 核心功能看作是下面👇 6 个部分实现的：
{: id="20210330211656-0i0cgtg"}

1. {: id="20210330211656-br1rcd9"}**客户端（服务消费端）** ：调用远程方法的一端。
   {: id="20210330211656-ngdasng"}
2. {: id="20210330211656-2h9d8mw"}**客户端 Stub（桩）** ： 这其实就是一代理类。代理类主要做的事情很简单，就是把你调用方法、类、方法参数等信息传递到服务端。
   {: id="20210330211656-qmpxrpn"}
3. {: id="20210330211656-547c2zw"}**网络传输** ： 网络传输就是你要把你调用的方法的信息比如说参数啊这些东西传输到服务端，然后服务端执行完之后再把返回结果通过网络传输给你传输回来。网络传输的实现方式有很多种比如最近基本的 Socket或者性能以及封装更加优秀的 Netty（推荐）。
   {: id="20210330211656-tzghwpa"}
4. {: id="20210330211656-rmqhrch"}**服务端 Stub（桩）** ：这个桩就不是代理类了。我觉得理解为桩实际不太好，大家注意一下就好。这里的服务端 Stub 实际指的就是接收到客户端执行方法的请求后，去指定对应的方法然后返回结果给客户端的类。
   {: id="20210330211656-w3jf3u2"}
5. {: id="20210330211656-otiehu9"}**服务端（服务提供端）** ：提供远程方法的一端。
   {: id="20210330211656-t2wuzhq"}
{: id="20210330211656-r1ugybd"}

具体原理图如下，后面我会串起来将整个RPC的过程给大家说一下。
{: id="20210330211656-0vvppfg"}

![RPC原理图](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-12-6/37345851.jpg)
{: id="20210330211656-k677io2"}

1. {: id="20210330211656-cl3wrzj"}服务消费端（client）以本地调用的方式调用远程服务；
   {: id="20210330211656-bjnoode"}
2. {: id="20210330211656-v3rudqd"}客户端 Stub（client stub） 接收到调用后负责将方法、参数等组装成能够进行网络传输的消息体（序列化）：`RpcRequest`；
   {: id="20210330211656-rhp7bus"}
3. {: id="20210330211656-7tp8xd8"}客户端 Stub（client stub） 找到远程服务的地址，并将消息发送到服务提供端；
   {: id="20210330211656-mj3fz2y"}
4. {: id="20210330211656-ajvonx6"}服务端 Stub（桩）收到消息将消息反序列化为Java对象: `RpcRequest`；
   {: id="20210330211656-8rmr4ba"}
5. {: id="20210330211656-mhrq1tk"}服务端 Stub（桩）根据`RpcRequest`中的类、方法、方法参数等信息调用本地的方法；
   {: id="20210330211656-kjgu9es"}
6. {: id="20210330211656-rfma6h4"}服务端 Stub（桩）得到方法执行结果并将组装成能够进行网络传输的消息体：`RpcResponse`（序列化）发送至消费方；
   {: id="20210330211656-yr36t4g"}
7. {: id="20210330211656-gib4750"}客户端 Stub（client stub）接收到消息并将消息反序列化为Java对象:`RpcResponse` ，这样也就得到了最终结果。over!
   {: id="20210330211656-au7bap6"}
{: id="20210330211656-clgfjsj"}

相信小伙伴们看完上面的讲解之后，已经了解了 RPC 的原理。
{: id="20210330211656-4f39paq"}

虽然篇幅不多，但是基本把 RPC 框架的核心原理讲清楚了！另外，对于上面的技术细节，我会在后面的章节介绍到。
{: id="20210330211656-qeejyya"}

**最后，对于 RPC 的原理，希望小伙伴不单单要理解，还要能够自己画出来并且能够给别人讲出来。因为，在面试中这个问题在面试官问到 RPC 相关内容的时候基本都会碰到。**
{: id="20210330211656-3y6p4kp"}

## Dubbo基础
{: id="20210330211656-1vj5jb3"}

### 什么是 Dubbo?
{: id="20210330211656-xru08qd"}

![](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2020-8/427f2168-1930-4c14-8760-415fac8db1d0-20200802184737978.png)
{: id="20210330211656-yxm9wli"}

[Apache Dubbo](https://github.com/apache/incubator-dubbo) (incubating) |ˈdʌbəʊ|  是一款高性能、轻量级的开源 Java RPC 框架。
{: id="20210330211656-spopodk"}

根据 [Dubbo 官方文档](https://dubbo.apache.org/zh/)的介绍，Dubbo 提供了六大核心能力
{: id="20210330211656-ewyhxmu"}

1. {: id="20210330211656-jiqc9zi"}面向接口代理的高性能RPC调用。
   {: id="20210330211656-905qiev"}
2. {: id="20210330211656-s55xoot"}智能容错和负载均衡。
   {: id="20210330211656-ivhhkp4"}
3. {: id="20210330211656-hvx8bd2"}服务自动注册和发现。
   {: id="20210330211656-eiizec4"}
4. {: id="20210330211656-2hy030e"}高度可扩展能力。
   {: id="20210330211656-2knguo6"}
5. {: id="20210330211656-q77pz8a"}运行期流量调度。
   {: id="20210330211656-fr0rchq"}
6. {: id="20210330211656-gjdc0xd"}可视化的服务治理与运维。
   {: id="20210330211656-m5p33xi"}
{: id="20210330211656-mzaw2js"}

![Dubbo提供的六大核心能力](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/%E6%BA%90%E7%A0%81/dubbo/dubbo%E6%8F%90%E4%BE%9B%E7%9A%84%E5%85%AD%E5%A4%A7%E6%A0%B8%E5%BF%83%E8%83%BD%E5%8A%9B.png)
{: id="20210330211656-pq4jy3i"}

简单来说就是： **Dubbo 不光可以帮助我们调用远程服务，还提供了一些其他开箱即用的功能比如智能负载均衡。**
{: id="20210330211656-jkywtay"}

Dubbo 目前已经有接近 34.4 k 的 Star  。
{: id="20210330211656-fijp5sh"}

在 **2020 年度 OSC 中国开源项目** 评选活动中，Dubbo 位列开发框架和基础组件类项目的第7名。想比几年前来说，热度和排名有所下降。
{: id="20210330211656-6v7vs7e"}

![](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/%E6%BA%90%E7%A0%81/dubbo/image-20210107153159545.png)
{: id="20210330211656-fwwt6h3"}

Dubbo 是由阿里开源，后来加入了 Apache 。正式由于 Dubbo 的出现，才使得越来越多的公司开始使用以及接受分布式架构。
{: id="20210330211656-edvaolg"}

### 为什么要用 Dubbo?
{: id="20210330211656-vfl4517"}

随着互联网的发展，网站的规模越来越大，用户数量越来越多。单一应用架构 、垂直应用架构无法满足我们的需求，这个时候分布式服务架构就诞生了。
{: id="20210330211656-el9ija8"}

分布式服务架构下，系统被拆分成不同的服务比如短信服务、安全服务，每个服务独立提供系统的某个核心服务。
{: id="20210330211656-opsy6qx"}

我们可以使用 Java RMI（Java Remote Method Invocation）、Hessian这种支持远程调用的框架来简单地暴露和引用远程服务。但是！当服务越来越多之后，服务调用关系越来越复杂。当应用访问压力越来越大后，负载均衡以及服务监控的需求也迫在眉睫。我们可以用 F5 这类硬件来做负载均衡，但这样增加了成本，并且存在单点故障的风险。
{: id="20210330211656-cl1u7p8"}

不过，Dubbo 的出现让上述问题得到了解决。**Dubbo 帮助我们解决了什么问题呢？**
{: id="20210330211656-zp7ngrw"}

1. {: id="20210330211656-6zmkq99"}**负载均衡** ： 同一个服务部署在不同的机器时该调用那一台机器上的服务。
   {: id="20210330211656-shmjivc"}
2. {: id="20210330211656-7y6vwty"}**服务调用链路生成**  ： 随着系统的发展，服务越来越多，服务间依赖关系变得错踪复杂，甚至分不清哪个应用要在哪个应用之前启动，架构师都不能完整的描述应用的架构关系。Dubbo 可以为我们解决服务之间互相是如何调用的。
   {: id="20210330211656-exaxc9y"}
3. {: id="20210330211656-yt4re70"}**服务访问压力以及时长统计、资源调度和治理** ：基于访问压力实时管理集群容量，提高集群利用率。
   {: id="20210330211656-yc29gcl"}
4. {: id="20210330211656-tcvmz9l"}......
   {: id="20210330211656-xm3esub"}
{: id="20210330211656-qzzxz2a"}

![](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-9-26/43050183.jpg)
{: id="20210330211656-ewta91r"}

另外，Dubbo 除了能够应用在分布式系统中，也可以应用在现在比较火的微服务系统中。不过，由于 Spring Cloud 在微服务中应用更加广泛，所以，我觉得一般我们提 Dubbo 的话，大部分是分布式系统的情况。
{: id="20210330211656-82mucva"}

**我们刚刚提到了分布式这个概念，下面再给大家介绍一下什么是分布式？为什么要分布式？**
{: id="20210330211656-nlkmbid"}

## 分布式基础
{: id="20210330211656-qhki7bl"}

### 什么是分布式?
{: id="20210330211656-wxvips8"}

分布式或者说 SOA 分布式重要的就是面向服务，说简单的分布式就是我们把整个系统拆分成不同的服务然后将这些服务放在不同的服务器上减轻单体服务的压力提高并发量和性能。比如电商系统可以简单地拆分成订单系统、商品系统、登录系统等等，拆分之后的每个服务可以部署在不同的机器上，如果某一个服务的访问量比较大的话也可以将这个服务同时部署在多台机器上。
{: id="20210330211656-yfms9li"}

![分布式事务示意图](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/java-guide-blog/%E5%88%86%E5%B8%83%E5%BC%8F%E4%BA%8B%E5%8A%A1%E7%A4%BA%E6%84%8F%E5%9B%BE.png)
{: id="20210330211656-ht9uwgm"}

### 为什么要分布式?
{: id="20210330211656-n4oqpnb"}

从开发角度来讲单体应用的代码都集中在一起，而分布式系统的代码根据业务被拆分。所以，每个团队可以负责一个服务的开发，这样提升了开发效率。另外，代码根据业务拆分之后更加便于维护和扩展。
{: id="20210330211656-1h5sdfa"}

另外，我觉得将系统拆分成分布式之后不光便于系统扩展和维护，更能提高整个系统的性能。你想一想嘛？把整个系统拆分成不同的服务/系统，然后每个服务/系统 单独部署在一台服务器上，是不是很大程度上提高了系统性能呢？
{: id="20210330211656-1vix5is"}

## Dubbo 架构
{: id="20210330211656-4ac4wor"}

### Dubbo 架构中的核心角色有哪些？
{: id="20210330211656-ajirzjf"}

[官方文档中的框架设计章节](https://dubbo.apache.org/zh/docs/v2.7/dev/design/) 已经介绍的非常详细了，我这里把一些比较重要的点再提一下。
{: id="20210330211656-4kdd0be"}

![dubbo-relation](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/%E6%BA%90%E7%A0%81/dubbo/dubbo-relation.jpg)
{: id="20210330211656-nyvbaqw"}

上述节点简单介绍以及他们之间的关系：
{: id="20210330211656-44mxaza"}

- {: id="20210330211656-yw2y9f9"}**Container：** 服务运行容器，负责加载、运行服务提供者。必须。
  {: id="20210330211656-sgl1fxz"}
- {: id="20210330211656-ilh3smm"}**Provider：** 暴露服务的服务提供方，会向注册中心注册自己提供的服务。必须。
  {: id="20210330211656-w94lwla"}
- {: id="20210330211656-vvybjbn"}**Consumer：** 调用远程服务的服务消费方，会向注册中心订阅自己所需的服务。必须。
  {: id="20210330211656-vganv55"}
- {: id="20210330211656-y869rhg"}**Registry：** 服务注册与发现的注册中心。注册中心会返回服务提供者地址列表给消费者。非必须。
  {: id="20210330211656-f0j53ls"}
- {: id="20210330211656-fz06zt7"}**Monitor：** 统计服务的调用次数和调用时间的监控中心。服务消费者和提供者会定时发送统计数据到监控中心。 非必须。
  {: id="20210330211656-cfls4k6"}
{: id="20210330211656-k9ngbvj"}

### Dubbo 中的 Invoker 概念了解么？
{: id="20210330211656-6obmf5i"}

`Invoker` 是 Dubbo 领域模型中非常重要的一个概念，你如果阅读过 Dubbo 源码的话，你会无数次看到这玩意。就比如下面我要说的负载均衡这块的源码中就有大量 `Invoker` 的身影。
{: id="20210330211656-gjl89m1"}

简单来说，`Invoker` 就是 Dubbo 对远程调用的抽象。
{: id="20210330211656-me4mz0c"}

![dubbo_rpc_invoke.jpg](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/java-guide-blog/dubbo_rpc_invoke.jpg)
{: id="20210330211656-o3qpmvn"}

按照 Dubbo 官方的话来说，`Invoker`  分为
{: id="20210330211656-tpgwtzp"}

- {: id="20210330211656-iyfb5fn"}服务提供 `Invoker`
  {: id="20210330211656-gzmhjb5"}
- {: id="20210330211656-71h3sp8"}服务消费 `Invoker`
  {: id="20210330211656-ch2o2r2"}
{: id="20210330211656-1c53gwr"}

假如我们需要调用一个远程方法，我们需要动态代理来屏蔽远程调用的细节吧！我们屏蔽掉的这些细节就依赖对应的 `Invoker`  实现， `Invoker` 实现了真正的远程服务调用。
{: id="20210330211656-ialjkhu"}

### Dubbo 的工作原理了解么？
{: id="20210330211656-d0prm03"}

下图是 Dubbo 的整体设计，从下至上分为十层，各层均为单向依赖。
{: id="20210330211656-nj6qyys"}

> 左边淡蓝背景的为服务消费方使用的接口，右边淡绿色背景的为服务提供方使用的接口，位于中轴线上的为双方都用到的接口。
> {: id="20210330211656-nel7geb"}
{: id="20210330211656-u8kc3vo"}

![dubbo-framework](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/source-code/dubbo/dubbo-framework.jpg)
{: id="20210330211656-s76cnek"}

- {: id="20210330211656-0p7vnzk"}**config 配置层**：Dubbo相关的配置。支持代码配置，同时也支持基于 Spring  来做配置，以 `ServiceConfig`, `ReferenceConfig` 为中心
  {: id="20210330211656-uqy2nm0"}
- {: id="20210330211656-qvuru0i"}**proxy 服务代理层**：调用远程方法像调用本地的方法一样简单的一个关键，真实调用过程依赖代理类，以 `ServiceProxy` 为中心。
  {: id="20210330211656-hshceyn"}
- {: id="20210330211656-3xjoslj"}**registry 注册中心层**：封装服务地址的注册与发现。
  {: id="20210330211656-a5cav1z"}
- {: id="20210330211656-5917kpx"}**cluster 路由层**：封装多个提供者的路由及负载均衡，并桥接注册中心，以 `Invoker` 为中心。
  {: id="20210330211656-lzzavzz"}
- {: id="20210330211656-i238pfg"}**monitor 监控层**：RPC 调用次数和调用时间监控，以 `Statistics` 为中心。
  {: id="20210330211656-torwg9g"}
- {: id="20210330211656-yc6yaxu"}**protocol 远程调用层**：封装 RPC 调用，以 `Invocation`, `Result` 为中心。
  {: id="20210330211656-ql2zye6"}
- {: id="20210330211656-73ft232"}**exchange 信息交换层**：封装请求响应模式，同步转异步，以 `Request`, `Response` 为中心。
  {: id="20210330211656-5lhelua"}
- {: id="20210330211656-ejng7gy"}**transport 网络传输层**：抽象 mina 和 netty 为统一接口，以 `Message` 为中心。
  {: id="20210330211656-j4hdqvh"}
- {: id="20210330211656-gh4a72x"}**serialize 数据序列化层** ：对需要在网络传输的数据进行序列化。
  {: id="20210330211656-7kgcikr"}
{: id="20210330211656-qzo17pn"}

### Dubbo 的 SPI 机制了解么？ 如何扩展 Dubbo 中的默认实现？
{: id="20210330211656-4tzhdn8"}

SPI（Service Provider Interface） 机制被大量用在开源项目中，它可以帮助我们动态寻找服务/功能（比如负载均衡策略）的实现。
{: id="20210330211656-804cvdn"}

SPI 的具体原理是这样的：我们将接口的实现类放在配置文件中，我们在程序运行过程中读取配置文件，通过反射加载实现类。这样，我们可以在运行的时候，动态替换接口的实现类。和 IoC 的解耦思想是类似的。
{: id="20210330211656-eet7my2"}

Java 本身就提供了 SPI 机制的实现。不过，Dubbo 没有直接用，而是对 Java原生的 SPI机制进行了增强，以便更好满足自己的需求。
{: id="20210330211656-7h8wez2"}

**那我们如何扩展 Dubbo 中的默认实现呢？**
{: id="20210330211656-ipr816y"}

比如说我们想要实现自己的负载均衡策略，我们创建对应的实现类 `XxxLoadBalance` 实现 `LoadBalance` 接口或者 `AbstractLoadBalance` 类。
{: id="20210330211656-pg0sivo"}

```java
package com.xxx;
 
import org.apache.dubbo.rpc.cluster.LoadBalance;
import org.apache.dubbo.rpc.Invoker;
import org.apache.dubbo.rpc.Invocation;
import org.apache.dubbo.rpc.RpcException; 
 
public class XxxLoadBalance implements LoadBalance {
    public <T> Invoker<T> select(List<Invoker<T>> invokers, Invocation invocation) throws RpcException {
        // ...
    }
}
```
{: id="20210330211656-dq2l4ac"}

我们将这个是实现类的路径写入到`resources` 目录下的 `META-INF/dubbo/org.apache.dubbo.rpc.cluster.LoadBalance`文件中即可。
{: id="20210330211656-fgqda05"}

```java
src
 |-main
    |-java
        |-com
            |-xxx
                |-XxxLoadBalance.java (实现LoadBalance接口)
    |-resources
        |-META-INF
            |-dubbo
                |-org.apache.dubbo.rpc.cluster.LoadBalance (纯文本文件，内容为：xxx=com.xxx.XxxLoadBalance)
```
{: id="20210330211656-bol1tn7"}

`org.apache.dubbo.rpc.cluster.LoadBalance`
{: id="20210330211656-e67rivj"}

```
xxx=com.xxx.XxxLoadBalance
```
{: id="20210330211656-px2gsr5"}

其他还有很多可供扩展的选择，你可以在[官方文档@SPI扩展实现](https://dubbo.apache.org/zh/docs/v2.7/dev/impls/)这里找到。
{: id="20210330211656-q9j2diu"}

![](https://img-blog.csdnimg.cn/20210328091015555.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0MzM3Mjcy,size_16,color_FFFFFF,t_70)
{: id="20210330211656-06fcbeu"}

### Dubbo 的微内核架构了解吗？
{: id="20210330211656-svuwidt"}

Dubbo 采用 微内核（Microkernel） + 插件（Plugin） 模式，简单来说就是微内核架构。微内核只负责组装插件。
{: id="20210330211656-1rvtdno"}

**何为微内核架构呢？** 《软件架构模式》 这本书是这样介绍的：
{: id="20210330211656-rvp2za6"}

> 微内核架构模式（有时被称为插件架构模式）是实现基于产品应用程序的一种自然模式。基于产品的应用程序是已经打包好并且拥有不同版本，可作为第三方插件下载的。然后，很多公司也在开发、发布自己内部商业应用像有版本号、说明及可加载插件式的应用软件（这也是这种模式的特征）。微内核系统可让用户添加额外的应用如插件，到核心应用，继而提供了可扩展性和功能分离的用法。
> {: id="20210330211656-guyq9ly"}
{: id="20210330211656-sj70hkw"}

微内核架构包含两类组件：**核心系统（core system）** 和 **插件模块（plug-in modules）**。
{: id="20210330211656-cruhnos"}

![](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/source-code/dubbo/%E5%BE%AE%E5%86%85%E6%A0%B8%E6%9E%B6%E6%9E%84%E7%A4%BA%E6%84%8F%E5%9B%BE.png)
{: id="20210330211656-9b8lsev"}

核心系统提供系统所需核心能力，插件模块可以扩展系统的功能。因此， 基于微内核架构的系统，非常易于扩展功能。
{: id="20210330211656-xstoikc"}

我们常见的一些IDE，都可以看作是基于微内核架构设计的。绝大多数 IDE比如IDEA、VSCode都提供了插件来丰富自己的功能。
{: id="20210330211656-37cwtve"}

正是因为Dubbo基于微内核架构，才使得我们可以随心所欲替换Dubbo的功能点。比如你觉得Dubbo 的序列化模块实现的不满足自己要求，没关系啊！你自己实现一个序列化模块就好了啊！
{: id="20210330211656-1mnqwkt"}

通常情况下，微核心都会采用 Factory、IoC、OSGi 等方式管理插件生命周期。Dubbo 不想依赖 Spring 等 IoC 容器，也不想自已造一个小的 IoC 容器（过度设计），因此采用了一种最简单的 Factory 方式管理插件 ：**JDK 标准的 SPI 扩展机制** （`java.util.ServiceLoader`）。
{: id="20210330211656-whmeh2s"}

### 关于Dubbo架构的一些自测小问题
{: id="20210330211656-4y8e2ce"}

#### 注册中心的作用了解么？
{: id="20210330211656-iczemdo"}

注册中心负责服务地址的注册与查找，相当于目录服务，服务提供者和消费者只在启动时与注册中心交互。
{: id="20210330211656-4y85r4z"}

#### 服务提供者宕机后，注册中心会做什么？
{: id="20210330211656-b05nk0j"}

注册中心会立即推送事件通知消费者。
{: id="20210330211656-hm1vbbm"}

#### 监控中心的作用呢？
{: id="20210330211656-oknycbp"}

监控中心负责统计各服务调用次数，调用时间等。
{: id="20210330211656-wqupg63"}

#### 注册中心和监控中心都宕机的话，服务都会挂掉吗？
{: id="20210330211656-28col08"}

不会。两者都宕机也不影响已运行的提供者和消费者，消费者在本地缓存了提供者列表。注册中心和监控中心都是可选的，服务消费者可以直连服务提供者。
{: id="20210330211656-lzn1tlq"}

## Dubbo 的负载均衡策略
{: id="20210330211656-k79qaee"}

### 什么是负载均衡？
{: id="20210330211656-bd4tjb8"}

先来看一下稍微官方点的解释。下面这段话摘自维基百科对负载均衡的定义：
{: id="20210330211656-h5gvw41"}

> 负载均衡改善了跨多个计算资源（例如计算机，计算机集群，网络链接，中央处理单元或磁盘驱动）的工作负载分布。负载平衡旨在优化资源使用，最大化吞吐量，最小化响应时间，并避免任何单个资源的过载。使用具有负载平衡而不是单个组件的多个组件可以通过冗余提高可靠性和可用性。负载平衡通常涉及专用软件或硬件。
> {: id="20210330211656-88nmqup"}
{: id="20210330211656-izncnrf"}

**上面讲的大家可能不太好理解，再用通俗的话给大家说一下。**
{: id="20210330211656-ju4dkpe"}

我们的系统中的某个服务的访问量特别大，我们将这个服务部署在了多台服务器上，当客户端发起请求的时候，多台服务器都可以处理这个请求。那么，如何正确选择处理该请求的服务器就很关键。假如，你就要一台服务器来处理该服务的请求，那该服务部署在多台服务器的意义就不复存在了。负载均衡就是为了避免单个服务器响应同一请求，容易造成服务器宕机、崩溃等问题，我们从负载均衡的这四个字就能明显感受到它的意义。
{: id="20210330211656-kh1ghcb"}

### Dubbo 提供的负载均衡策略有哪些？
{: id="20210330211656-1zavn00"}

在集群负载均衡时，Dubbo 提供了多种均衡策略，默认为 `random` 随机调用。我们还可以自行扩展负载均衡策略（参考Dubbo SPI机制）。
{: id="20210330211656-8zs83j5"}

在 Dubbo 中，所有负载均衡实现类均继承自 `AbstractLoadBalance`，该类实现了 `LoadBalance` 接口，并封装了一些公共的逻辑。
{: id="20210330211656-rxn3wxa"}

```java
public abstract class AbstractLoadBalance implements LoadBalance {

    static int calculateWarmupWeight(int uptime, int warmup, int weight) {
    }

    @Override
    public <T> Invoker<T> select(List<Invoker<T>> invokers, URL url, Invocation invocation) {
    }

    protected abstract <T> Invoker<T> doSelect(List<Invoker<T>> invokers, URL url, Invocation invocation);


    int getWeight(Invoker<?> invoker, Invocation invocation) {

    }
}
```
{: id="20210330211656-apua1zq"}

`AbstractLoadBalance` 的实现类有下面这些：
{: id="20210330211656-ft101rc"}

![](/Users/guide/Library/Application Support/typora-user-images/image-20210326105257812.png)
{: id="20210330211656-4fgngdz"}

官方文档对负载均衡这部分的介绍非常详细，推荐小伙伴们看看，地址：[https://dubbo.apache.org/zh/docs/v2.7/dev/source/loadbalance/#m-zhdocsv27devsourceloadbalance](https://dubbo.apache.org/zh/docs/v2.7/dev/source/loadbalance/#m-zhdocsv27devsourceloadbalance ) 。
{: id="20210330211656-046bo4a"}

#### RandomLoadBalance
{: id="20210330211656-o71thv7"}

根据权重随机选择（对加权随机算法的实现）。这是Dubbo默认采用的一种负载均衡策略。
{: id="20210330211656-e69ebot"}

` RandomLoadBalance` 具体的实现原理非常简单，假如有两个提供相同服务的服务器 S1,S2，S1的权重为7，S2的权重为3。
{: id="20210330211656-keha9zs"}

我们把这些权重值分布在坐标区间会得到：S1->[0, 7) ，S2->(7, 10]。我们生成[0, 10) 之间的随机数，随机数落到对应的区间，我们就选择对应的服务器来处理请求。
{: id="20210330211656-2827t9w"}

![RandomLoadBalance](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/java-guide-blog/%20RandomLoadBalance.png)
{: id="20210330211656-pta0a9v"}

`RandomLoadBalance` 的源码非常简单，简单花几分钟时间看一下。
{: id="20210330211656-uqgbzt2"}

> 以下源码来自 Dubbo master 分支上的最新的版本 2.7.9。
> {: id="20210330211656-vefk4nb"}
{: id="20210330211656-981iiye"}

```java
public class RandomLoadBalance extends AbstractLoadBalance {

    public static final String NAME = "random";

    @Override
    protected <T> Invoker<T> doSelect(List<Invoker<T>> invokers, URL url, Invocation invocation) {

        int length = invokers.size();
        boolean sameWeight = true;
        int[] weights = new int[length]; 
        int totalWeight = 0;
        // 下面这个for循环的主要作用就是计算所有该服务的提供者的权重之和 totalWeight（），
        // 除此之外，还会检测每个服务提供者的权重是否相同
        for (int i = 0; i < length; i++) {
            int weight = getWeight(invokers.get(i), invocation);
            totalWeight += weight;
            weights[i] = totalWeight;
            if (sameWeight && totalWeight != weight * (i + 1)) {
                sameWeight = false;
            }
        }
        if (totalWeight > 0 && !sameWeight) {
            // 随机生成一个 [0, totalWeight) 区间内的数字
            int offset = ThreadLocalRandom.current().nextInt(totalWeight);
            // 判断会落在哪个服务提供者的区间
            for (int i = 0; i < length; i++) {
                if (offset < weights[i]) {
                    return invokers.get(i);
                }
            }
  
        return invokers.get(ThreadLocalRandom.current().nextInt(length));
    }

}

```
{: id="20210330211656-u0nwkfr"}

#### LeastActiveLoadBalance
{: id="20210330211656-8xzgawx"}

`LeastActiveLoadBalance` 直译过来就是**最小活跃数负载均衡**。
{: id="20210330211656-6yw2c6z"}

这个名字起得有点不直观，不仔细看官方对活跃数的定义，你压根不知道这玩意是干嘛的。
{: id="20210330211656-1iu8i1v"}

我这么说吧！初始状态下所有服务提供者的活跃数均为 0（每个服务提供者的中特定方法都对应一个活跃数，我在后面的源码中会提到），每收到一个请求后，对应的服务提供者的活跃数 +1，当这个请求处理完之后，活跃数 -1。
{: id="20210330211656-rkwzz6z"}

因此，**Dubbo 就认为谁的活跃数越少，谁的处理速度就越快，性能也越好，这样的话，我就优先把请求给活跃数少的服务提供者处理。**
{: id="20210330211656-4ld8p0k"}

**如果有多个服务提供者的活跃数相等怎么办？**
{: id="20210330211656-qig1u3e"}

很简单，那就再走一遍  `RandomLoadBalance` 。
{: id="20210330211656-8fw4dzm"}

```java
public class LeastActiveLoadBalance extends AbstractLoadBalance {

    public static final String NAME = "leastactive";

    @Override
    protected <T> Invoker<T> doSelect(List<Invoker<T>> invokers, URL url, Invocation invocation) {
        int length = invokers.size();
        int leastActive = -1;
        int leastCount = 0;
        int[] leastIndexes = new int[length];
        int[] weights = new int[length];
        int totalWeight = 0;
        int firstWeight = 0;
        boolean sameWeight = true;
        // 这个 for 循环的主要作用是遍历 invokers 列表，找出活跃数最小的 Invoker
        // 如果有多个 Invoker 具有相同的最小活跃数，还会记录下这些 Invoker 在 invokers 集合中的下标，并累加它们的权重，比较它们的权重值是否相等
        for (int i = 0; i < length; i++) {
            Invoker<T> invoker = invokers.get(i);
            // 获取 invoker 对应的活跃(active)数
            int active = RpcStatus.getStatus(invoker.getUrl(), invocation.getMethodName()).getActive();
            int afterWarmup = getWeight(invoker, invocation);
            weights[i] = afterWarmup;
            if (leastActive == -1 || active < leastActive) {
                leastActive = active;
                leastCount = 1;
                leastIndexes[0] = i;
                totalWeight = afterWarmup;
                firstWeight = afterWarmup;
                sameWeight = true;
            } else if (active == leastActive) {
                leastIndexes[leastCount++] = i;
                totalWeight += afterWarmup;
                if (sameWeight && afterWarmup != firstWeight) {
                    sameWeight = false;
                }
            }
        }
       // 如果只有一个 Invoker 具有最小的活跃数，此时直接返回该 Invoker 即可
        if (leastCount == 1) {
            return invokers.get(leastIndexes[0]);
        }
        // 如果有多个 Invoker 具有相同的最小活跃数，但它们之间的权重不同
        // 这里的处理方式就和  RandomLoadBalance 一致了
        if (!sameWeight && totalWeight > 0) {
            int offsetWeight = ThreadLocalRandom.current().nextInt(totalWeight);
            for (int i = 0; i < leastCount; i++) {
                int leastIndex = leastIndexes[i];
                offsetWeight -= weights[leastIndex];
                if (offsetWeight < 0) {
                    return invokers.get(leastIndex);
                }
            }
        }
        return invokers.get(leastIndexes[ThreadLocalRandom.current().nextInt(leastCount)]);
    }
}

```
{: id="20210330211656-laearzo"}

活跃数是通过 `RpcStatus` 中的一个 `ConcurrentMap` 保存的，根据 URL 以及服务提供者被调用的方法的名称，我们便可以获取到对应的活跃数。也就是说服务提供者中的每一个方法的活跃数都是互相独立的。
{: id="20210330211656-aqyqept"}

```java
public class RpcStatus {
    
    private static final ConcurrentMap<String, ConcurrentMap<String, RpcStatus>> METHOD_STATISTICS =
            new ConcurrentHashMap<String, ConcurrentMap<String, RpcStatus>>();

   public static RpcStatus getStatus(URL url, String methodName) {
        String uri = url.toIdentityString();
        ConcurrentMap<String, RpcStatus> map = METHOD_STATISTICS.computeIfAbsent(uri, k -> new ConcurrentHashMap<>());
        return map.computeIfAbsent(methodName, k -> new RpcStatus());
    }
    public int getActive() {
        return active.get();
    }

}
```
{: id="20210330211656-fbxvty9"}

#### ConsistentHashLoadBalance
{: id="20210330211656-8vxpy0e"}

`ConsistentHashLoadBalance`  小伙伴们应该也不会陌生，在分库分表、各种集群中就经常使用这个负载均衡策略。
{: id="20210330211656-op1kq2p"}

`ConsistentHashLoadBalance` 即**一致性Hash负载均衡策略**。 `ConsistentHashLoadBalance` 中没有权重的概念，具体是哪个服务提供者处理请求是由你的请求的参数决定的，也就是说相同参数的请求总是发到同一个服务提供者。
{: id="20210330211656-zetkahe"}

![](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/java-guide-blog/consistent-hash-data-incline.jpg)
{: id="20210330211656-pxjrsor"}

另外，Dubbo 为了避免数据倾斜问题（节点不够分散，大量请求落到同一节点），还引入了虚拟节点的概念。通过虚拟节点可以让节点更加分散，有效均衡各个节点的请求量。
{: id="20210330211656-bm4lt9p"}

![](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/java-guide-blog/consistent-hash-invoker.jpg)
{: id="20210330211656-cpxotph"}

官方有详细的源码分析：[https://dubbo.apache.org/zh/docs/v2.7/dev/source/loadbalance/#23-consistenthashloadbalance](https://dubbo.apache.org/zh/docs/v2.7/dev/source/loadbalance/#23-consistenthashloadbalance) 。这里还有一个相关的 [PR#5440](https://github.com/apache/dubbo/pull/5440) 来修复老版本中 ConsistentHashLoadBalance 存在的一些Bug。感兴趣的小伙伴，可以多花点时间研究一下。我这里不多分析了，这个作业留给你们！
{: id="20210330211656-f5lh374"}

#### RoundRobinLoadBalance
{: id="20210330211656-otsxhc7"}

加权轮询负载均衡。
{: id="20210330211656-77pwrx6"}

轮询就是把请求依次分配给每个服务提供者。加权轮询就是在轮询的基础上，让更多的请求落到权重更大的服务提供者上。比如假如有两个提供相同服务的服务器 S1,S2，S1的权重为7，S2的权重为3。
{: id="20210330211656-ac9hopc"}

如果我们有 10 次请求，那么  7 次会被 S1处理，3次被 S2处理。
{: id="20210330211656-lqhrhae"}

但是，如果是 `RandomLoadBalance` 的话，很可能存在10次请求有9次都被 S1 处理的情况（概率性问题）。
{: id="20210330211656-e129dpa"}

Dubbo 中的 `RoundRobinLoadBalance` 的代码实现被修改重建了好几次，Dubbo-2.6.5 版本的 `RoundRobinLoadBalance` 为平滑加权轮询算法。
{: id="20210330211656-8qvt8z9"}

## Dubbo序列化协议
{: id="20210330211656-9ifk0hv"}

### Dubbo 支持哪些序列化方式呢？
{: id="20210330211656-b0eftua"}

![](https://img-blog.csdnimg.cn/20210328092219640.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0MzM3Mjcy,size_16,color_FFFFFF,t_70)
{: id="20210330211656-xx99lxo"}

Dubbo 支持多种序列化方式：JDK自带的序列化、hessian2、JSON、Kryo、FST、Protostuff，ProtoBuf等等。
{: id="20210330211656-ssg9og1"}

Dubbo 默认使用的序列化方式是 hession2。
{: id="20210330211656-8z6leno"}

### 谈谈你对这些序列化协议了解？
{: id="20210330211656-bk7ow2a"}

一般我们不会直接使用 JDK 自带的序列化方式。主要原因有两个：
{: id="20210330211656-oo2dc11"}

1. {: id="20210330211656-y6axkim"}**不支持跨语言调用** : 如果调用的是其他语言开发的服务的时候就不支持了。
   {: id="20210330211656-kdtrqmk"}
2. {: id="20210330211656-oc8yh87"}**性能差** ：相比于其他序列化框架性能更低，主要原因是序列化之后的字节数组体积较大，导致传输成本加大。
   {: id="20210330211656-ehjdn3x"}
{: id="20210330211656-aa94z5r"}

JSON 序列化由于性能问题，我们一般也不会考虑使用。
{: id="20210330211656-mlfbmnj"}

像 Protostuff，ProtoBuf、hessian2这些都是跨语言的序列化方式，如果有跨语言需求的话可以考虑使用。
{: id="20210330211656-3vfqixq"}

Kryo和FST这两种序列化方式是 Dubbo 后来才引入的，性能非常好。不过，这两者都是专门针对 Java 语言的。Dubbo 官网的一篇文章中提到说推荐使用 Kryo 作为生产环境的序列化方式。(文章地址：[https://dubbo.apache.org/zh/docs/v2.7/user/references/protocol/rest/](https://dubbo.apache.org/zh/docs/v2.7/user/references/protocol/rest/))
{: id="20210330211656-c48n4op"}

![](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2020-8/569e541a-22b2-4846-aa07-0ad479f07440.png)
{: id="20210330211656-gr9jdhb"}

Dubbo 官方文档中还有一个关于这些[序列化协议的性能对比图](https://dubbo.apache.org/zh/docs/v2.7/user/serialization/#m-zhdocsv27userserialization)可供参考。
{: id="20210330211656-4qa069h"}

![](https://img-blog.csdnimg.cn/20210328093219609.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0MzM3Mjcy,size_16,color_FFFFFF,t_70)
{: id="20210330211656-a4n3fx6"}


{: id="20210330211656-fvhpuo9" type="doc"}
