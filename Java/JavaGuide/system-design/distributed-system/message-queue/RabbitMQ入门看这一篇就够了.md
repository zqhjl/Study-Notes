<!-- TOC -->

- {: id="20210330211656-847gpmf"}[一文搞懂 RabbitMQ 的重要概念以及安装](#一文搞懂-rabbitmq-的重要概念以及安装)
  {: id="20210330211656-zveartw"}
  - {: id="20210330211656-5xcmat9"}[一 RabbitMQ 介绍](#一-rabbitmq-介绍)
    {: id="20210330211656-fd0xzse"}
    - {: id="20210330211656-9j5gchw"}[1.1 RabbitMQ 简介](#11-rabbitmq-简介)
      {: id="20210330211656-ktbn312"}
    - {: id="20210330211656-tniywp3"}[1.2 RabbitMQ 核心概念](#12-rabbitmq-核心概念)
      {: id="20210330211656-uapnmnd"}
      - {: id="20210330211656-crul2wi"}[1.2.1 Producer(生产者) 和 Consumer(消费者)](#121-producer生产者-和-consumer消费者)
        {: id="20210330211656-u2ixqkg"}
      - {: id="20210330211656-zmwpad4"}[1.2.2 Exchange(交换器)](#122-exchange交换器)
        {: id="20210330211656-ohwaxn6"}
      - {: id="20210330211656-pd1wxhb"}[1.2.3 Queue(消息队列)](#123-queue消息队列)
        {: id="20210330211656-rhnjbqz"}
      - {: id="20210330211656-h3call8"}[1.2.4 Broker（消息中间件的服务节点）](#124-broker消息中间件的服务节点)
        {: id="20210330211656-ra2ttwc"}
      - {: id="20210330211656-3rthj2x"}[1.2.5 Exchange Types(交换器类型)](#125-exchange-types交换器类型)
        {: id="20210330211656-gpcw9fv"}
        - {: id="20210330211656-ra1cxe7"}[① fanout](#①-fanout)
          {: id="20210330211656-0ntgx5x"}
        - {: id="20210330211656-dndkcoh"}[② direct](#②-direct)
          {: id="20210330211656-cecbff4"}
        - {: id="20210330211656-rjxeg4v"}[③ topic](#③-topic)
          {: id="20210330211656-2yjzgpm"}
        - {: id="20210330211656-1cp5iiw"}[④ headers(不推荐)](#④-headers不推荐)
          {: id="20210330211656-uq04izu"}
        {: id="20210330211656-kb3p8n7"}
      {: id="20210330211656-nsb1u51"}
    {: id="20210330211656-vdmrci7"}
  - {: id="20210330211656-fqxbqp0"}[二 安装 RabbitMq](#二-安装-rabbitmq)
    {: id="20210330211656-6zuv9tb"}
    - {: id="20210330211656-x1c4qpk"}[2.1 安装 erlang](#21-安装-erlang)
      {: id="20210330211656-vr33shn"}
    - {: id="20210330211656-cevz7p7"}[2.2 安装 RabbitMQ](#22-安装-rabbitmq)
      {: id="20210330211656-h9qnubq"}
    {: id="20210330211656-fnjlqk2"}
  {: id="20210330211656-kddojnq"}
{: id="20210330211656-5s7ta9v"}

<!-- /TOC -->

# 一文搞懂 RabbitMQ 的重要概念以及安装
{: id="20210330211656-4clrz20"}

## 一 RabbitMQ 介绍
{: id="20210330211656-k23bkrg"}

这部分参考了 《RabbitMQ实战指南》这本书的第 1 章和第 2 章。
{: id="20210330211656-nmocqwj"}

### 1.1 RabbitMQ 简介
{: id="20210330211656-y2erwou"}

RabbitMQ 是采用 Erlang 语言实现 AMQP(Advanced Message Queuing Protocol，高级消息队列协议）的消息中间件，它最初起源于金融系统，用于在分布式系统中存储转发消息。
{: id="20210330211656-191gbv1"}

RabbitMQ 发展到今天，被越来越多的人认可，这和它在易用性、扩展性、可靠性和高可用性等方面的卓著表现是分不开的。RabbitMQ 的具体特点可以概括为以下几点：
{: id="20210330211656-64tqfee"}

- {: id="20210330211656-77xw895"}**可靠性：** RabbitMQ使用一些机制来保证消息的可靠性，如持久化、传输确认及发布确认等。
  {: id="20210330211656-miyctyu"}
- {: id="20210330211656-o25wdf8"}**灵活的路由：** 在消息进入队列之前，通过交换器来路由消息。对于典型的路由功能，RabbitMQ 己经提供了一些内置的交换器来实现。针对更复杂的路由功能，可以将多个交换器绑定在一起，也可以通过插件机制来实现自己的交换器。这个后面会在我们将 RabbitMQ 核心概念的时候详细介绍到。
  {: id="20210330211656-y50sco8"}
- {: id="20210330211656-uru3pv5"}**扩展性：** 多个RabbitMQ节点可以组成一个集群，也可以根据实际业务情况动态地扩展集群中节点。
  {: id="20210330211656-yl9hzwz"}
- {: id="20210330211656-qw4tn7v"}**高可用性：** 队列可以在集群中的机器上设置镜像，使得在部分节点出现问题的情况下队列仍然可用。
  {: id="20210330211656-pwkexa7"}
- {: id="20210330211656-rq7wgvl"}**支持多种协议：** RabbitMQ 除了原生支持 AMQP 协议，还支持 STOMP、MQTT 等多种消息中间件协议。
  {: id="20210330211656-k775bek"}
- {: id="20210330211656-ehxpk4i"}**多语言客户端：** RabbitMQ几乎支持所有常用语言，比如 Java、Python、Ruby、PHP、C#、JavaScript等。
  {: id="20210330211656-4usfy39"}
- {: id="20210330211656-ejvj7mw"}**易用的管理界面：** RabbitMQ提供了一个易用的用户界面，使得用户可以监控和管理消息、集群中的节点等。在安装 RabbitMQ 的时候会介绍到，安装好 RabbitMQ 就自带管理界面。
  {: id="20210330211656-nfvb5ti"}
- {: id="20210330211656-xw3s3rc"}**插件机制：** RabbitMQ 提供了许多插件，以实现从多方面进行扩展，当然也可以编写自己的插件。感觉这个有点类似 Dubbo 的 SPI机制。
  {: id="20210330211656-oya9beb"}
{: id="20210330211656-0muody7"}

### 1.2 RabbitMQ 核心概念
{: id="20210330211656-qwfa05s"}

RabbitMQ 整体上是一个生产者与消费者模型，主要负责接收、存储和转发消息。可以把消息传递的过程想象成：当你将一个包裹送到邮局，邮局会暂存并最终将邮件通过邮递员送到收件人的手上，RabbitMQ就好比由邮局、邮箱和邮递员组成的一个系统。从计算机术语层面来说，RabbitMQ 模型更像是一种交换机模型。
{: id="20210330211656-ls9cs02"}

下面再来看看图1—— RabbitMQ 的整体模型架构。
{: id="20210330211656-hs94hop"}

![图1-RabbitMQ 的整体模型架构](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-12-16/96388546.jpg)
{: id="20210330211656-3jhadmi"}

下面我会一一介绍上图中的一些概念。
{: id="20210330211656-zce4bpk"}

#### 1.2.1 Producer(生产者) 和 Consumer(消费者)
{: id="20210330211656-glmpsuk"}

- {: id="20210330211656-8xw42ig"}**Producer(生产者)** :生产消息的一方（邮件投递者）
  {: id="20210330211656-74iavb6"}
- {: id="20210330211656-vrnxres"}**Consumer(消费者)** :消费消息的一方（邮件收件人）
  {: id="20210330211656-vudkllb"}
{: id="20210330211656-mmqfnao"}

消息一般由 2 部分组成：**消息头**（或者说是标签 Label）和 **消息体**。消息体也可以称为 payLoad ,消息体是不透明的，而消息头则由一系列的可选属性组成，这些属性包括 routing-key（路由键）、priority（相对于其他消息的优先权）、delivery-mode（指出该消息可能需要持久性存储）等。生产者把消息交由 RabbitMQ 后，RabbitMQ 会根据消息头把消息发送给感兴趣的 Consumer(消费者)。
{: id="20210330211656-7ug7k8b"}

#### 1.2.2 Exchange(交换器)
{: id="20210330211656-tyuuzlu"}

在 RabbitMQ 中，消息并不是直接被投递到 **Queue(消息队列)** 中的，中间还必须经过 **Exchange(交换器)** 这一层，**Exchange(交换器)** 会把我们的消息分配到对应的 **Queue(消息队列)** 中。
{: id="20210330211656-apmbmqe"}

**Exchange(交换器)** 用来接收生产者发送的消息并将这些消息路由给服务器中的队列中，如果路由不到，或许会返回给 **Producer(生产者)** ，或许会被直接丢弃掉 。这里可以将RabbitMQ中的交换器看作一个简单的实体。
{: id="20210330211656-5z7fsk3"}

**RabbitMQ 的 Exchange(交换器) 有4种类型，不同的类型对应着不同的路由策略**：**direct(默认)**，**fanout**, **topic**, 和 **headers**，不同类型的Exchange转发消息的策略有所区别。这个会在介绍 **Exchange Types(交换器类型)** 的时候介绍到。
{: id="20210330211656-gr83zli"}

Exchange(交换器) 示意图如下：
{: id="20210330211656-zagp6wv"}

![Exchange(交换器) 示意图](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-12-16/24007899.jpg)
{: id="20210330211656-ru6a56k"}

生产者将消息发给交换器的时候，一般会指定一个 **RoutingKey(路由键)**，用来指定这个消息的路由规则，而这个 **RoutingKey 需要与交换器类型和绑定键(BindingKey)联合使用才能最终生效**。
{: id="20210330211656-kybu5m7"}

RabbitMQ 中通过 **Binding(绑定)** 将 **Exchange(交换器)** 与 **Queue(消息队列)** 关联起来，在绑定的时候一般会指定一个 **BindingKey(绑定建)** ,这样 RabbitMQ 就知道如何正确将消息路由到队列了,如下图所示。一个绑定就是基于路由键将交换器和消息队列连接起来的路由规则，所以可以将交换器理解成一个由绑定构成的路由表。Exchange 和 Queue 的绑定可以是多对多的关系。
{: id="20210330211656-0yy5g7n"}

Binding(绑定) 示意图：
{: id="20210330211656-yt7ni8j"}

![Binding(绑定) 示意图](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-12-16/70553134.jpg)
{: id="20210330211656-uhtqr57"}

生产者将消息发送给交换器时，需要一个RoutingKey,当 BindingKey 和 RoutingKey 相匹配时，消息会被路由到对应的队列中。在绑定多个队列到同一个交换器的时候，这些绑定允许使用相同的 BindingKey。BindingKey 并不是在所有的情况下都生效，它依赖于交换器类型，比如fanout类型的交换器就会无视，而是将消息路由到所有绑定到该交换器的队列中。
{: id="20210330211656-8uazkof"}

#### 1.2.3 Queue(消息队列)
{: id="20210330211656-mq79s8c"}

**Queue(消息队列)** 用来保存消息直到发送给消费者。它是消息的容器，也是消息的终点。一个消息可投入一个或多个队列。消息一直在队列里面，等待消费者连接到这个队列将其取走。
{: id="20210330211656-dsve6rl"}

**RabbitMQ** 中消息只能存储在 **队列** 中，这一点和 **Kafka** 这种消息中间件相反。Kafka 将消息存储在 **topic（主题）** 这个逻辑层面，而相对应的队列逻辑只是topic实际存储文件中的位移标识。 RabbitMQ 的生产者生产消息并最终投递到队列中，消费者可以从队列中获取消息并消费。
{: id="20210330211656-0hgfiaz"}

**多个消费者可以订阅同一个队列**，这时队列中的消息会被平均分摊（Round-Robin，即轮询）给多个消费者进行处理，而不是每个消费者都收到所有的消息并处理，这样避免的消息被重复消费。
{: id="20210330211656-0ioym2u"}

**RabbitMQ** 不支持队列层面的广播消费,如果有广播消费的需求，需要在其上进行二次开发,这样会很麻烦，不建议这样做。
{: id="20210330211656-sqqruvn"}

#### 1.2.4 Broker（消息中间件的服务节点）
{: id="20210330211656-6g5s1e3"}

对于 RabbitMQ 来说，一个 RabbitMQ Broker 可以简单地看作一个 RabbitMQ 服务节点，或者RabbitMQ服务实例。大多数情况下也可以将一个 RabbitMQ Broker 看作一台 RabbitMQ 服务器。
{: id="20210330211656-z7bmakx"}

下图展示了生产者将消息存入 RabbitMQ Broker,以及消费者从Broker中消费数据的整个流程。
{: id="20210330211656-k1hzrgy"}

![消息队列的运转过程](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-12-16/67952922.jpg)
{: id="20210330211656-amamlso"}

这样图1中的一些关于 RabbitMQ 的基本概念我们就介绍完毕了，下面再来介绍一下 **Exchange Types(交换器类型)** 。
{: id="20210330211656-e8a0ibk"}

#### 1.2.5 Exchange Types(交换器类型)
{: id="20210330211656-qkcb5d2"}

RabbitMQ 常用的 Exchange Type 有 **fanout**、**direct**、**topic**、**headers** 这四种（AMQP规范里还提到两种 Exchange Type，分别为 system 与 自定义，这里不予以描述）。
{: id="20210330211656-9s4xqp6"}

##### ① fanout
{: id="20210330211656-jfo2vdl"}

fanout 类型的Exchange路由规则非常简单，它会把所有发送到该Exchange的消息路由到所有与它绑定的Queue中，不需要做任何判断操作，所以 fanout 类型是所有的交换机类型里面速度最快的。fanout 类型常用来广播消息。
{: id="20210330211656-0weri8o"}

##### ② direct
{: id="20210330211656-x9e73y8"}

direct 类型的Exchange路由规则也很简单，它会把消息路由到那些 Bindingkey 与 RoutingKey 完全匹配的 Queue 中。
{: id="20210330211656-rq3q68j"}

![direct 类型交换器](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-12-16/37008021.jpg)
{: id="20210330211656-94948hk"}

以上图为例，如果发送消息的时候设置路由键为“warning”,那么消息会路由到 Queue1 和 Queue2。如果在发送消息的时候设置路由键为"Info”或者"debug”，消息只会路由到Queue2。如果以其他的路由键发送消息，则消息不会路由到这两个队列中。
{: id="20210330211656-ix46tcf"}

direct 类型常用在处理有优先级的任务，根据任务的优先级把消息发送到对应的队列，这样可以指派更多的资源去处理高优先级的队列。
{: id="20210330211656-tq7zmrq"}

##### ③ topic
{: id="20210330211656-ev7wqbk"}

前面讲到direct类型的交换器路由规则是完全匹配 BindingKey 和 RoutingKey ，但是这种严格的匹配方式在很多情况下不能满足实际业务的需求。topic类型的交换器在匹配规则上进行了扩展，它与 direct 类型的交换器相似，也是将消息路由到 BindingKey 和 RoutingKey 相匹配的队列中，但这里的匹配规则有些不同，它约定：
{: id="20210330211656-bem76uc"}

- {: id="20210330211656-lcnf6wz"}RoutingKey 为一个点号“．”分隔的字符串（被点号“．”分隔开的每一段独立的字符串称为一个单词），如 “com.rabbitmq.client”、“java.util.concurrent”、“com.hidden.client”;
  {: id="20210330211656-808qq0t"}
- {: id="20210330211656-gxsodtj"}BindingKey 和 RoutingKey 一样也是点号“．”分隔的字符串；
  {: id="20210330211656-ayvbzv9"}
- {: id="20210330211656-jh2yovp"}BindingKey 中可以存在两种特殊字符串“*”和“#”，用于做模糊匹配，其中“*”用于匹配一个单词，“#”用于匹配多个单词(可以是零个)。
  {: id="20210330211656-3xriwx9"}
{: id="20210330211656-2ylamv5"}

![topic 类型交换器](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-12-16/73843.jpg)
{: id="20210330211656-7tfj9u0"}

以上图为例：
{: id="20210330211656-wdb4rfm"}

- {: id="20210330211656-53o6jgh"}路由键为 “com.rabbitmq.client” 的消息会同时路由到 Queuel 和 Queue2;
  {: id="20210330211656-34ggtht"}
- {: id="20210330211656-aya5vx2"}路由键为 “com.hidden.client” 的消息只会路由到 Queue2 中；
  {: id="20210330211656-89mqovf"}
- {: id="20210330211656-gvazri7"}路由键为 “com.hidden.demo” 的消息只会路由到 Queue2 中；
  {: id="20210330211656-a0oyfum"}
- {: id="20210330211656-d4atstf"}路由键为 “java.rabbitmq.demo” 的消息只会路由到Queuel中；
  {: id="20210330211656-kmxhfql"}
- {: id="20210330211656-3liyo5h"}路由键为 “java.util.concurrent” 的消息将会被丢弃或者返回给生产者（需要设置 mandatory 参数），因为它没有匹配任何路由键。
  {: id="20210330211656-pdl7rif"}
{: id="20210330211656-vjai8iv"}

##### ④ headers(不推荐)
{: id="20210330211656-3bpyjw4"}

headers 类型的交换器不依赖于路由键的匹配规则来路由消息，而是根据发送的消息内容中的 headers 属性进行匹配。在绑定队列和交换器时制定一组键值对，当发送消息到交换器时，RabbitMQ会获取到该消息的 headers（也是一个键值对的形式)'对比其中的键值对是否完全匹配队列和交换器绑定时指定的键值对，如果完全匹配则消息会路由到该队列，否则不会路由到该队列。headers 类型的交换器性能会很差，而且也不实用，基本上不会看到它的存在。
{: id="20210330211656-lb5lx7n"}

## 二 安装 RabbitMq
{: id="20210330211656-wcqjz1l"}

通过 Docker 安装非常方便，只需要几条命令就好了，我这里是只说一下常规安装方法。
{: id="20210330211656-zk8iasc"}

前面提到了 RabbitMQ 是由 Erlang语言编写的，也正因如此，在安装RabbitMQ 之前需要安装 Erlang。
{: id="20210330211656-34pgdke"}

注意：在安装 RabbitMQ 的时候需要注意 RabbitMQ 和 Erlang 的版本关系，如果不注意的话会导致出错，两者对应关系如下:
{: id="20210330211656-vuyth62"}

![RabbitMQ 和 Erlang 的版本关系](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-3/RabbitMQ-Erlang.png)
{: id="20210330211656-ffo5x5c"}

### 2.1 安装 erlang
{: id="20210330211656-mbe09d0"}

**1 下载 erlang 安装包**
{: id="20210330211656-34fl3kh"}

在官网下载然后上传到 Linux 上或者直接使用下面的命令下载对应的版本。
{: id="20210330211656-9e2rj97"}

```shell
[root@SnailClimb local]#wget http://erlang.org/download/otp_src_19.3.tar.gz
```
{: id="20210330211656-rcd2hy7"}

erlang 官网下载：[http://www.erlang.org/downloads](http://www.erlang.org/downloads)
{: id="20210330211656-9iqybnr"}

**2 解压 erlang 安装包**
{: id="20210330211656-8dy2mkd"}

```shell
[root@SnailClimb local]#tar -xvzf otp_src_19.3.tar.gz
```
{: id="20210330211656-avqprd3"}

**3 删除 erlang 安装包**
{: id="20210330211656-u8qlndi"}

```shell
[root@SnailClimb local]#rm -rf otp_src_19.3.tar.gz
```
{: id="20210330211656-ozqrrw2"}

**4 安装 erlang 的依赖工具**
{: id="20210330211656-jduzjk2"}

```shell
[root@SnailClimb local]#yum -y install make gcc gcc-c++ kernel-devel m4 ncurses-devel openssl-devel unixODBC-devel
```
{: id="20210330211656-65oy7k8"}

**5 进入erlang 安装包解压文件对 erlang 进行安装环境的配置**
{: id="20210330211656-vwub1od"}

新建一个文件夹
{: id="20210330211656-uxop5mg"}

```shell
[root@SnailClimb local]# mkdir erlang
```
{: id="20210330211656-ccu9smg"}

对 erlang 进行安装环境的配置
{: id="20210330211656-wn5krfy"}

```shell
[root@SnailClimb otp_src_19.3]# 
./configure --prefix=/usr/local/erlang --without-javac
```
{: id="20210330211656-gaq5fuf"}

**6 编译安装**
{: id="20210330211656-htqbd3s"}

```shell
[root@SnailClimb otp_src_19.3]# 
make && make install
```
{: id="20210330211656-e5b3k4e"}

**7 验证一下 erlang 是否安装成功了**
{: id="20210330211656-3y6kagf"}

```shell
[root@SnailClimb otp_src_19.3]# ./bin/erl
```
{: id="20210330211656-2wollj4"}

运行下面的语句输出“hello world”
{: id="20210330211656-16acbrs"}

```erlang
 io:format("hello world~n", []).
```
{: id="20210330211656-ilw74bq"}

![输出“hello world”](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-12-12/49570541.jpg)
{: id="20210330211656-8tdwq59"}

大功告成，我们的 erlang 已经安装完成。
{: id="20210330211656-ljwbvbu"}

**8 配置  erlang 环境变量**
{: id="20210330211656-9bb3x95"}

```shell
[root@SnailClimb etc]# vim profile
```
{: id="20210330211656-xtc89c8"}

追加下列环境变量到文件末尾
{: id="20210330211656-0z1e79d"}

```shell
#erlang
ERL_HOME=/usr/local/erlang
PATH=$ERL_HOME/bin:$PATH
export ERL_HOME PATH
```
{: id="20210330211656-imeml5s"}

运行下列命令使配置文件`profile`生效
{: id="20210330211656-8j94jpp"}

```shell
[root@SnailClimb etc]# source /etc/profile
```
{: id="20210330211656-xh8qoz4"}

输入 erl 查看 erlang 环境变量是否配置正确
{: id="20210330211656-4hyd5cd"}

```shell
[root@SnailClimb etc]# erl
```
{: id="20210330211656-h947hb8"}

![输入 erl 查看 erlang 环境变量是否配置正确](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-12-12/62504246.jpg)
{: id="20210330211656-0wjzdty"}

### 2.2 安装 RabbitMQ
{: id="20210330211656-acr29t7"}

**1. 下载rpm**
{: id="20210330211656-fn2bhe5"}

```shell
wget https://www.rabbitmq.com/releases/rabbitmq-server/v3.6.8/rabbitmq-server-3.6.8-1.el7.noarch.rpm
```
{: id="20210330211656-mxihrcg"}

或者直接在官网下载
{: id="20210330211656-opusy1a"}

[https://www.rabbitmq.com/install-rpm.html](https://www.rabbitmq.com/install-rpm.html)
{: id="20210330211656-ocqa12s"}

**2. 安装rpm**
{: id="20210330211656-dk7w7ca"}

```shell
rpm --import https://www.rabbitmq.com/rabbitmq-release-signing-key.asc
```
{: id="20210330211656-0l3sx2g"}

紧接着执行：
{: id="20210330211656-azsoo11"}

```shell
yum install rabbitmq-server-3.6.8-1.el7.noarch.rpm
```
{: id="20210330211656-6edo9jb"}

中途需要你输入"y"才能继续安装。
{: id="20210330211656-twofu4w"}

**3 开启 web 管理插件**
{: id="20210330211656-xdcb4bb"}

```shell
rabbitmq-plugins enable rabbitmq_management
```
{: id="20210330211656-mr60c50"}

**4 设置开机启动**
{: id="20210330211656-9rn1pcn"}

```shell
chkconfig rabbitmq-server on
```
{: id="20210330211656-bx009qe"}

**4. 启动服务**
{: id="20210330211656-1yp5tg0"}

```shell
service rabbitmq-server start
```
{: id="20210330211656-4xrgubp"}

**5. 查看服务状态**
{: id="20210330211656-cbxywax"}

```shell
service rabbitmq-server status
```
{: id="20210330211656-p0631na"}

**6. 访问 RabbitMQ 控制台**
{: id="20210330211656-qu8byjn"}

浏览器访问：http://你的ip地址:15672/
{: id="20210330211656-ob1emce"}

默认用户名和密码： guest/guest;但是需要注意的是：guestuest用户只是被容许从localhost访问。官网文档描述如下：
{: id="20210330211656-d06bepp"}

```shell
“guest” user can only connect via localhost
```
{: id="20210330211656-o07c3us"}

**解决远程访问 RabbitMQ 远程访问密码错误**
{: id="20210330211656-i5i9s86"}

新建用户并授权
{: id="20210330211656-ec05uko"}

```shell
[root@SnailClimb rabbitmq]# rabbitmqctl add_user root root
Creating user "root" ...
[root@SnailClimb rabbitmq]# rabbitmqctl set_user_tags root administrator

Setting tags for user "root" to [administrator] ...
[root@SnailClimb rabbitmq]# 
[root@SnailClimb rabbitmq]# rabbitmqctl set_permissions -p / root ".*" ".*" ".*"
Setting permissions for user "root" in vhost "/" ...

```
{: id="20210330211656-mg233wd"}

再次访问:http://你的ip地址:15672/ ,输入用户名和密码：root root
{: id="20210330211656-wj41h99"}

![RabbitMQ控制台](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-12-12/45835332.jpg)
{: id="20210330211656-gzcg3ie"}


{: id="20210330211656-jdj0vvo" type="doc"}
