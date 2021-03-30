本文来自读者 [PR](https://github.com/Snailclimb/JavaGuide/pull/291)。
{: id="20210330211656-us6a7bg"}

<!-- TOC -->

- {: id="20210330211656-vm6n0vb"}[1 单机版消息中心](#1-%E5%8D%95%E6%9C%BA%E7%89%88%E6%B6%88%E6%81%AF%E4%B8%AD%E5%BF%83)
  {: id="20210330211656-n4pmb9p"}
- {: id="20210330211656-hh0wtze"}[2 分布式消息中心](#2-%E5%88%86%E5%B8%83%E5%BC%8F%E6%B6%88%E6%81%AF%E4%B8%AD%E5%BF%83)
  {: id="20210330211656-t3k1htq"}
  - {: id="20210330211656-yl5nc7x"}[2.1 问题与解决](#21-%E9%97%AE%E9%A2%98%E4%B8%8E%E8%A7%A3%E5%86%B3)
    {: id="20210330211656-gxfogfu"}
    - {: id="20210330211656-n3k5yfq"}[2.1.1 消息丢失的问题](#211-%E6%B6%88%E6%81%AF%E4%B8%A2%E5%A4%B1%E7%9A%84%E9%97%AE%E9%A2%98)
      {: id="20210330211656-imus71p"}
    - {: id="20210330211656-s77kp26"}[2.1.2 同步落盘怎么才能快](#212-%E5%90%8C%E6%AD%A5%E8%90%BD%E7%9B%98%E6%80%8E%E4%B9%88%E6%89%8D%E8%83%BD%E5%BF%AB)
      {: id="20210330211656-fhlgcmn"}
    - {: id="20210330211656-fztpkqp"}[2.1.3 消息堆积的问题](#213-%E6%B6%88%E6%81%AF%E5%A0%86%E7%A7%AF%E7%9A%84%E9%97%AE%E9%A2%98)
      {: id="20210330211656-lcbt14z"}
    - {: id="20210330211656-o5pr8xs"}[2.1.4 定时消息的实现](#214-%E5%AE%9A%E6%97%B6%E6%B6%88%E6%81%AF%E7%9A%84%E5%AE%9E%E7%8E%B0)
      {: id="20210330211656-p8xaz1u"}
    - {: id="20210330211656-8qcrfv4"}[2.1.5 顺序消息的实现](#215-%E9%A1%BA%E5%BA%8F%E6%B6%88%E6%81%AF%E7%9A%84%E5%AE%9E%E7%8E%B0)
      {: id="20210330211656-7wd9l4e"}
    - {: id="20210330211656-e4uvnez"}[2.1.6 分布式消息的实现](#216-%E5%88%86%E5%B8%83%E5%BC%8F%E6%B6%88%E6%81%AF%E7%9A%84%E5%AE%9E%E7%8E%B0)
      {: id="20210330211656-uyhxp69"}
    - {: id="20210330211656-f8uoc6w"}[2.1.7 消息的 push 实现](#217-%E6%B6%88%E6%81%AF%E7%9A%84-push-%E5%AE%9E%E7%8E%B0)
      {: id="20210330211656-eokiawu"}
    - {: id="20210330211656-kgmp2hd"}[2.1.8 消息重复发送的避免](#218-%E6%B6%88%E6%81%AF%E9%87%8D%E5%A4%8D%E5%8F%91%E9%80%81%E7%9A%84%E9%81%BF%E5%85%8D)
      {: id="20210330211656-5nb94ul"}
    - {: id="20210330211656-oxkskev"}[2.1.9 广播消费与集群消费](#219-%E5%B9%BF%E6%92%AD%E6%B6%88%E8%B4%B9%E4%B8%8E%E9%9B%86%E7%BE%A4%E6%B6%88%E8%B4%B9)
      {: id="20210330211656-q4hut4w"}
    - {: id="20210330211656-3df3odh"}[2.1.10 RocketMQ 不使用 ZooKeeper 作为注册中心的原因，以及自制的 NameServer 优缺点？](#2110-rocketmq-%E4%B8%8D%E4%BD%BF%E7%94%A8-zookeeper-%E4%BD%9C%E4%B8%BA%E6%B3%A8%E5%86%8C%E4%B8%AD%E5%BF%83%E7%9A%84%E5%8E%9F%E5%9B%A0%E4%BB%A5%E5%8F%8A%E8%87%AA%E5%88%B6%E7%9A%84-nameserver-%E4%BC%98%E7%BC%BA%E7%82%B9)
      {: id="20210330211656-4scwru7"}
    - {: id="20210330211656-jausg4w"}[2.1.11 其它](#2111-%E5%85%B6%E5%AE%83)
      {: id="20210330211656-ec4s05j"}
    {: id="20210330211656-tga3ceu"}
  {: id="20210330211656-qcwjasq"}
- {: id="20210330211656-n6g5smq"}[3 参考](#3-%E5%8F%82%E8%80%83)
  {: id="20210330211656-tqvnnzi"}
{: id="20210330211656-m1rsmds"}

<!-- TOC -->

# 1 单机版消息中心
{: id="20210330211656-vjlniwq"}

一个消息中心，最基本的需要支持多生产者、多消费者，例如下：
{: id="20210330211656-0r2fg8a"}

```java
class Scratch {

    public static void main(String[] args) {
        // 实际中会有 nameserver 服务来找到 broker 具体位置以及 broker 主从信息
        Broker broker = new Broker();
        Producer producer1 = new Producer();
        producer1.connectBroker(broker);
        Producer producer2 = new Producer();
        producer2.connectBroker(broker);

        Consumer consumer1 = new Consumer();
        consumer1.connectBroker(broker);
        Consumer consumer2 = new Consumer();
        consumer2.connectBroker(broker);

        for (int i = 0; i < 2; i++) {
            producer1.asyncSendMsg("producer1 send msg" + i);
            producer2.asyncSendMsg("producer2 send msg" + i);
        }
        System.out.println("broker has msg:" + broker.getAllMagByDisk());

        for (int i = 0; i < 1; i++) {
            System.out.println("consumer1 consume msg：" + consumer1.syncPullMsg());
        }
        for (int i = 0; i < 3; i++) {
            System.out.println("consumer2 consume msg：" + consumer2.syncPullMsg());
        }
    }

}

class Producer {

    private Broker broker;

    public void connectBroker(Broker broker) {
        this.broker = broker;
    }

    public void asyncSendMsg(String msg) {
        if (broker == null) {
            throw new RuntimeException("please connect broker first");
        }
        new Thread(() -> {
            broker.sendMsg(msg);
        }).start();
    }
}

class Consumer {
    private Broker broker;

    public void connectBroker(Broker broker) {
        this.broker = broker;
    }

    public String syncPullMsg() {
        return broker.getMsg();
    }

}

class Broker {

    // 对应 RocketMQ 中 MessageQueue，默认情况下 1 个 Topic 包含 4 个 MessageQueue
    private LinkedBlockingQueue<String> messageQueue = new LinkedBlockingQueue(Integer.MAX_VALUE);

    // 实际发送消息到 broker 服务器使用 Netty 发送
    public void sendMsg(String msg) {
        try {
            messageQueue.put(msg);
            // 实际会同步或异步落盘，异步落盘使用的定时任务定时扫描落盘
        } catch (InterruptedException e) {

        }
    }

    public String getMsg() {
        try {
            return messageQueue.take();
        } catch (InterruptedException e) {

        }
        return null;
    }

    public String getAllMagByDisk() {
        StringBuilder sb = new StringBuilder("\n");
        messageQueue.iterator().forEachRemaining((msg) -> {
            sb.append(msg + "\n");
        });
        return sb.toString();
    }
}
```
{: id="20210330211656-3rbbprd"}

问题：
{: id="20210330211656-24oswtn"}

1. {: id="20210330211656-acefyz9"}没有实现真正执行消息存储落盘
   {: id="20210330211656-l95gmzq"}
2. {: id="20210330211656-hs5w72z"}没有实现 NameServer 去作为注册中心，定位服务
   {: id="20210330211656-ks4x1l9"}
3. {: id="20210330211656-8pcwkmm"}使用 LinkedBlockingQueue 作为消息队列，注意，参数是无限大，在真正 RocketMQ 也是如此是无限大，理论上不会出现对进来的数据进行抛弃，但是会有内存泄漏问题（阿里巴巴开发手册也因为这个问题，建议我们使用自制线程池）
   {: id="20210330211656-pzlddbf"}
4. {: id="20210330211656-3tpo9y0"}没有使用多个队列（即多个 LinkedBlockingQueue），RocketMQ 的顺序消息是通过生产者和消费者同时使用同一个 MessageQueue 来实现，但是如果我们只有一个 MessageQueue，那我们天然就支持顺序消息
   {: id="20210330211656-8nwxmgf"}
5. {: id="20210330211656-2w9cubj"}没有使用 MappedByteBuffer 来实现文件映射从而使消息数据落盘非常的快（实际 RocketMQ 使用的是 FileChannel+DirectBuffer）
   {: id="20210330211656-g2fahae"}
{: id="20210330211656-dnzfa1i"}

# 2 分布式消息中心
{: id="20210330211656-kn6x8hb"}

## 2.1 问题与解决
{: id="20210330211656-0y1k81b"}

### 2.1.1 消息丢失的问题
{: id="20210330211656-sct5td6"}

1. {: id="20210330211656-l3na3vd"}当你系统需要保证百分百消息不丢失，你可以使用生产者每发送一个消息，Broker 同步返回一个消息发送成功的反馈消息
   {: id="20210330211656-uw7o1h1"}
2. {: id="20210330211656-58ssory"}即每发送一个消息，同步落盘后才返回生产者消息发送成功，这样只要生产者得到了消息发送生成的返回，事后除了硬盘损坏，都可以保证不会消息丢失
   {: id="20210330211656-zjn7i4q"}
3. {: id="20210330211656-u3iigh1"}但是这同时引入了一个问题，同步落盘怎么才能快？
   {: id="20210330211656-ahnf6lq"}
{: id="20210330211656-2tl02be"}

### 2.1.2 同步落盘怎么才能快
{: id="20210330211656-w3xqgqs"}

1. {: id="20210330211656-kgnivev"}使用 FileChannel + DirectBuffer 池，使用堆外内存，加快内存拷贝
   {: id="20210330211656-wt3oumx"}
2. {: id="20210330211656-5e7b9eo"}使用数据和索引分离，当消息需要写入时，使用 commitlog 文件顺序写，当需要定位某个消息时，查询index 文件来定位，从而减少文件IO随机读写的性能损耗
   {: id="20210330211656-5m97vx8"}
{: id="20210330211656-uqzbgb0"}

### 2.1.3 消息堆积的问题
{: id="20210330211656-zuxu3kf"}

1. {: id="20210330211656-zhowhvj"}后台定时任务每隔72小时，删除旧的没有使用过的消息信息
   {: id="20210330211656-gyjeyat"}
2. {: id="20210330211656-fud1c8i"}根据不同的业务实现不同的丢弃任务，具体参考线程池的 AbortPolicy，例如FIFO/LRU等（RocketMQ没有此策略）
   {: id="20210330211656-aik8qfo"}
3. {: id="20210330211656-p46j1lz"}消息定时转移，或者对某些重要的 TAG 型（支付型）消息真正落库
   {: id="20210330211656-rzsxmd9"}
{: id="20210330211656-trpswn1"}

### 2.1.4 定时消息的实现
{: id="20210330211656-b31v48d"}

1. {: id="20210330211656-h26p4a2"}实际 RocketMQ 没有实现任意精度的定时消息，它只支持某些特定的时间精度的定时消息
   {: id="20210330211656-ejmyleg"}
2. {: id="20210330211656-hiw3z4c"}实现定时消息的原理是：创建特定时间精度的 MessageQueue，例如生产者需要定时1s之后被消费者消费，你只需要将此消息发送到特定的 Topic，例如：MessageQueue-1 表示这个 MessageQueue 里面的消息都会延迟一秒被消费，然后 Broker 会在 1s 后发送到消费者消费此消息，使用 newSingleThreadScheduledExecutor 实现
   {: id="20210330211656-edkul0d"}
{: id="20210330211656-dg9xxur"}

### 2.1.5 顺序消息的实现
{: id="20210330211656-7rb74mo"}

1. {: id="20210330211656-unwfwyb"}与定时消息同原理，生产者生产消息时指定特定的 MessageQueue ，消费者消费消息时，消费特定的 MessageQueue，其实单机版的消息中心在一个 MessageQueue 就天然支持了顺序消息
   {: id="20210330211656-nn32q1t"}
2. {: id="20210330211656-4fir4rx"}注意：同一个 MessageQueue 保证里面的消息是顺序消费的前提是：消费者是串行的消费该 MessageQueue，因为就算 MessageQueue 是顺序的，但是当并行消费时，还是会有顺序问题，但是串行消费也同时引入了两个问题：
   {: id="20210330211656-c50242h"}
{: id="20210330211656-g5jgte0"}

> 1. {: id="20210330211656-iszmy6b"}引入锁来实现串行
>    {: id="20210330211656-0i3nhiz"}
> 2. {: id="20210330211656-lwpgwvq"}前一个消费阻塞时后面都会被阻塞
>    {: id="20210330211656-b7e8ss8"}
> {: id="20210330211656-9bjs2k6"}
{: id="20210330211656-jajvufl"}

### 2.1.6 分布式消息的实现
{: id="20210330211656-vj1y60b"}

1. {: id="20210330211656-zxwd02w"}需要前置知识：2PC
   {: id="20210330211656-88cx3w8"}
2. {: id="20210330211656-b9h72t8"}RocketMQ4.3 起支持，原理为2PC，即两阶段提交，prepared->commit/rollback
   {: id="20210330211656-sjf772z"}
3. {: id="20210330211656-76bebsp"}生产者发送事务消息，假设该事务消息 Topic 为 Topic1-Trans，Broker 得到后首先更改该消息的 Topic 为 Topic1-Prepared，该 Topic1-Prepared 对消费者不可见。然后定时回调生产者的本地事务A执行状态，根据本地事务A执行状态，来是否将该消息修改为 Topic1-Commit 或 Topic1-Rollback，消费者就可以正常找到该事务消息或者不执行等
   {: id="20210330211656-xqqdsia"}
{: id="20210330211656-ypnbz6b"}

> 注意，就算是事务消息最后回滚了也不会物理删除，只会逻辑删除该消息
> {: id="20210330211656-9nyglc2"}
{: id="20210330211656-z757x2h"}

### 2.1.7 消息的 push 实现
{: id="20210330211656-2cmvx23"}

1. {: id="20210330211656-bo1bwac"}注意，RocketMQ 已经说了自己会有低延迟问题，其中就包括这个消息的 push 延迟问题
   {: id="20210330211656-1n96u3o"}
2. {: id="20210330211656-hg3a7ih"}因为这并不是真正的将消息主动的推送到消费者，而是 Broker 定时任务每5s将消息推送到消费者
   {: id="20210330211656-2qaygtr"}
{: id="20210330211656-w18tfi1"}

### 2.1.8 消息重复发送的避免
{: id="20210330211656-grsriyr"}

1. {: id="20210330211656-hiwx5i8"}RocketMQ 会出现消息重复发送的问题，因为在网络延迟的情况下，这种问题不可避免的发生，如果非要实现消息不可重复发送，那基本太难，因为网络环境无法预知，还会使程序复杂度加大，因此默认允许消息重复发送
   {: id="20210330211656-dudgb74"}
2. {: id="20210330211656-s7pxv4j"}RocketMQ 让使用者在消费者端去解决该问题，即需要消费者端在消费消息时支持幂等性的去消费消息
   {: id="20210330211656-9k47owj"}
3. {: id="20210330211656-rqqv9w6"}最简单的解决方案是每条消费记录有个消费状态字段，根据这个消费状态字段来是否消费或者使用一个集中式的表，来存储所有消息的消费状态，从而避免重复消费
   {: id="20210330211656-5s52bz6"}
4. {: id="20210330211656-51ure5b"}具体实现可以查询关于消息幂等消费的解决方案
   {: id="20210330211656-1lbc88o"}
{: id="20210330211656-hkhn5w2"}

### 2.1.9 广播消费与集群消费
{: id="20210330211656-y2bumgg"}

1. {: id="20210330211656-o7g1dgf"}消息消费区别：广播消费，订阅该 Topic 的消息者们都会消费**每个**消息。集群消费，订阅该 Topic 的消息者们只会有一个去消费**某个**消息
   {: id="20210330211656-a1atnp3"}
2. {: id="20210330211656-vekq7n3"}消息落盘区别：具体表现在消息消费进度的保存上。广播消费，由于每个消费者都独立的去消费每个消息，因此每个消费者各自保存自己的消息消费进度。而集群消费下，订阅了某个 Topic，而旗下又有多个 MessageQueue，每个消费者都可能会去消费不同的 MessageQueue，因此总体的消费进度保存在 Broker 上集中的管理
   {: id="20210330211656-en6aqdp"}
{: id="20210330211656-pj5j9m9"}

### 2.1.10 RocketMQ 不使用 ZooKeeper 作为注册中心的原因，以及自制的 NameServer 优缺点？
{: id="20210330211656-2wt011u"}

1. {: id="20210330211656-sybbxzz"}ZooKeeper 作为支持顺序一致性的中间件，在某些情况下，它为了满足一致性，会丢失一定时间内的可用性，RocketMQ 需要注册中心只是为了发现组件地址，在某些情况下，RocketMQ 的注册中心可以出现数据不一致性，这同时也是 NameServer 的缺点，因为 NameServer 集群间互不通信，它们之间的注册信息可能会不一致
   {: id="20210330211656-zwm46n2"}
2. {: id="20210330211656-esyexpp"}另外，当有新的服务器加入时，NameServer 并不会立马通知到 Produer，而是由 Produer 定时去请求 NameServer 获取最新的 Broker/Consumer 信息（这种情况是通过 Producer 发送消息时，负载均衡解决）
   {: id="20210330211656-096zrf8"}
{: id="20210330211656-jmzj4qi"}

### 2.1.11 其它
{: id="20210330211656-mz6c03h"}

![](https://leran2deeplearnjavawebtech.oss-cn-beijing.aliyuncs.com/somephoto/RocketMQ%E6%B5%81%E7%A8%8B.png)
{: id="20210330211656-cxktypl"}

加分项咯
{: id="20210330211656-8vmi47g"}

1. {: id="20210330211656-p02923m"}包括组件通信间使用 Netty 的自定义协议
   {: id="20210330211656-13k6xyf"}
2. {: id="20210330211656-pqq5lsh"}消息重试负载均衡策略（具体参考 Dubbo 负载均衡策略）
   {: id="20210330211656-beiwrs4"}
3. {: id="20210330211656-ncb4ww5"}消息过滤器（Producer 发送消息到 Broker，Broker 存储消息信息，Consumer 消费时请求 Broker 端从磁盘文件查询消息文件时,在 Broker 端就使用过滤服务器进行过滤）
   {: id="20210330211656-5q3am0y"}
4. {: id="20210330211656-02q4dmz"}Broker 同步双写和异步双写中 Master 和 Slave 的交互
   {: id="20210330211656-cy1wpeu"}
5. {: id="20210330211656-xvu2bza"}Broker 在 4.5.0 版本更新中引入了基于 Raft 协议的多副本选举，之前这是商业版才有的特性 [ISSUE-1046][2]
   {: id="20210330211656-efa1nyw"}
{: id="20210330211656-oys93ws"}

# 3 参考
{: id="20210330211656-eegll95"}

1. {: id="20210330211656-0wfy76k"}《RocketMQ技术内幕》：https://blog.csdn.net/prestigeding/article/details/85233529
   {: id="20210330211656-q5mdm8z"}
2. {: id="20210330211656-uae4wv3"}关于 RocketMQ 对 MappedByteBuffer 的一点优化：https://lishoubo.github.io/2017/09/27/MappedByteBuffer%E7%9A%84%E4%B8%80%E7%82%B9%E4%BC%98%E5%8C%96/
   {: id="20210330211656-l1gvcnm"}
3. {: id="20210330211656-fp5agdj"}阿里中间件团队博客-十分钟入门RocketMQ：http://jm.taobao.org/2017/01/12/rocketmq-quick-start-in-10-minutes/
   {: id="20210330211656-3uhl5ja"}
4. {: id="20210330211656-h2erm6m"}分布式事务的种类以及 RocketMQ 支持的分布式消息：https://www.infoq.cn/article/2018/08/rocketmq-4.3-release
   {: id="20210330211656-xi99vfa"}
5. {: id="20210330211656-657mfx9"}滴滴出行基于RocketMQ构建企业级消息队列服务的实践：https://yq.aliyun.com/articles/664608
   {: id="20210330211656-15d3k4y"}
6. {: id="20210330211656-8wkrsmz"}基于《RocketMQ技术内幕》源码注释：https://github.com/LiWenGu/awesome-rocketmq
   {: id="20210330211656-sno7ohc"}
{: id="20210330211656-p5q0ey8"}

[1]: https://leran2deeplearnjavawebtech.oss-cn-beijing.aliyuncs.com/somephoto/RocketMQ%E6%B5%81%E7%A8%8B.png
[2]: http://rocketmq.apache.org/release_notes/release-notes-4.5.0/

{: id="20210330211656-wagdsh5" type="doc"}
