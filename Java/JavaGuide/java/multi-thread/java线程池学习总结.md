<!-- TOC -->

- {: id="20210330211656-a9b1vlt"}[一 使用线程池的好处](#一-使用线程池的好处)
  {: id="20210330211656-zk9pf37"}
- {: id="20210330211656-pu1xscl"}[二 Executor 框架](#二-executor-框架)
  {: id="20210330211656-xl8iygm"}
  - {: id="20210330211656-zd34upr"}[2.1 简介](#21-简介)
    {: id="20210330211656-nx262xu"}
  - {: id="20210330211656-s0z3rvd"}[2.2 Executor 框架结构(主要由三大部分组成)](#22-executor-框架结构主要由三大部分组成)
    {: id="20210330211656-d4nsbpu"}
    - {: id="20210330211656-fuw8edc"}[1) 任务(`Runnable` /`Callable`)](#1-任务runnable-callable)
      {: id="20210330211656-c6p6rsn"}
    - {: id="20210330211656-kc06i7s"}[2) 任务的执行(`Executor`)](#2-任务的执行executor)
      {: id="20210330211656-1279bn3"}
    - {: id="20210330211656-nwc4hak"}[3) 异步计算的结果(`Future`)](#3-异步计算的结果future)
      {: id="20210330211656-1ydpc1o"}
    {: id="20210330211656-cwgpgsp"}
  - {: id="20210330211656-2aodjos"}[2.3 Executor 框架的使用示意图](#23-executor-框架的使用示意图)
    {: id="20210330211656-kcrpcoh"}
  {: id="20210330211656-l1doj6f"}
- {: id="20210330211656-2zcbbt7"}[三 (重要)ThreadPoolExecutor 类简单介绍](#三-重要threadpoolexecutor-类简单介绍)
  {: id="20210330211656-gb4ggc4"}
  - {: id="20210330211656-5xwsmo9"}[3.1 ThreadPoolExecutor 类分析](#31-threadpoolexecutor-类分析)
    {: id="20210330211656-cfk2zgr"}
  - {: id="20210330211656-53qlxvu"}[3.2 推荐使用 `ThreadPoolExecutor` 构造函数创建线程池](#32-推荐使用-threadpoolexecutor-构造函数创建线程池)
    {: id="20210330211656-sijxmfi"}
  {: id="20210330211656-pjulku0"}
- {: id="20210330211656-t3v4wi4"}[四 (重要)ThreadPoolExecutor 使用示例](#四-重要threadpoolexecutor-使用示例)
  {: id="20210330211656-rpag879"}
  - {: id="20210330211656-1m28k11"}[4.1 示例代码:`Runnable`+`ThreadPoolExecutor`](#41-示例代码runnablethreadpoolexecutor)
    {: id="20210330211656-y9yht7h"}
  - {: id="20210330211656-rfgxk2l"}[4.2 线程池原理分析](#42-线程池原理分析)
    {: id="20210330211656-qtgdzz3"}
  - {: id="20210330211656-9fzpq65"}[4.3 几个常见的对比](#43-几个常见的对比)
    {: id="20210330211656-gn5kakv"}
    - {: id="20210330211656-1elsafk"}[4.3.1 `Runnable` vs `Callable`](#431-runnable-vs-callable)
      {: id="20210330211656-pn0aquw"}
    - {: id="20210330211656-8i6635m"}[4.3.2 `execute()` vs `submit()`](#432-execute-vs-submit)
      {: id="20210330211656-7m7btdc"}
    - {: id="20210330211656-s8mxqd0"}[4.3.3 `shutdown()`VS`shutdownNow()`](#433-shutdownvsshutdownnow)
      {: id="20210330211656-oyeh234"}
    - {: id="20210330211656-zolm7nv"}[4.3.2 `isTerminated()` VS `isShutdown()`](#432-isterminated-vs-isshutdown)
      {: id="20210330211656-wq1619j"}
    {: id="20210330211656-goewf3d"}
  - {: id="20210330211656-7aiz85x"}[4.4 加餐:`Callable`+`ThreadPoolExecutor`示例代码](#44-加餐callablethreadpoolexecutor示例代码)
    {: id="20210330211656-i0w12hr"}
  {: id="20210330211656-llwhd3g"}
- {: id="20210330211656-i6giki0"}[五 几种常见的线程池详解](#五-几种常见的线程池详解)
  {: id="20210330211656-tz525zq"}
  - {: id="20210330211656-9oh5qyi"}[5.1 FixedThreadPool](#51-fixedthreadpool)
    {: id="20210330211656-52w4k5g"}
    - {: id="20210330211656-0r2o9nk"}[5.1.1 介绍](#511-介绍)
      {: id="20210330211656-699c9y3"}
    - {: id="20210330211656-0p3mg9k"}[5.1.2 执行任务过程介绍](#512-执行任务过程介绍)
      {: id="20210330211656-0nzvp32"}
    - {: id="20210330211656-dadlzka"}[5.1.3 为什么不推荐使用`FixedThreadPool`？](#513-为什么不推荐使用fixedthreadpool)
      {: id="20210330211656-v3gg5zu"}
    {: id="20210330211656-sdvqnds"}
  - {: id="20210330211656-nn04ine"}[5.2 SingleThreadExecutor 详解](#52-singlethreadexecutor-详解)
    {: id="20210330211656-7ko2p91"}
    - {: id="20210330211656-nv6n4fk"}[5.2.1 介绍](#521-介绍)
      {: id="20210330211656-kzs7p88"}
    - {: id="20210330211656-ap2jtnq"}[5.2.2 执行任务过程介绍](#522-执行任务过程介绍)
      {: id="20210330211656-1tf7cwy"}
    - {: id="20210330211656-o8bv4mq"}[5.2.3 为什么不推荐使用`SingleThreadExecutor`？](#523-为什么不推荐使用singlethreadexecutor)
      {: id="20210330211656-ogg8uz2"}
    {: id="20210330211656-002eegm"}
  - {: id="20210330211656-ri1k4yp"}[5.3 CachedThreadPool 详解](#53-cachedthreadpool-详解)
    {: id="20210330211656-u64kdib"}
    - {: id="20210330211656-4lj086b"}[5.3.1 介绍](#531-介绍)
      {: id="20210330211656-287n6md"}
    - {: id="20210330211656-hmp4d1c"}[5.3.2 执行任务过程介绍](#532-执行任务过程介绍)
      {: id="20210330211656-ezkzk2w"}
    - {: id="20210330211656-avzasz7"}[5.3.3 为什么不推荐使用`CachedThreadPool`？](#533-为什么不推荐使用cachedthreadpool)
      {: id="20210330211656-6b4je18"}
    {: id="20210330211656-5r704xt"}
  {: id="20210330211656-syd669i"}
- {: id="20210330211656-ohik899"}[六 ScheduledThreadPoolExecutor 详解](#六-scheduledthreadpoolexecutor-详解)
  {: id="20210330211656-djbdntl"}
  - {: id="20210330211656-tdmweqd"}[6.1 简介](#61-简介)
    {: id="20210330211656-v0k652g"}
  - {: id="20210330211656-rfbqs8l"}[6.2 运行机制](#62-运行机制)
    {: id="20210330211656-c4937yi"}
  - {: id="20210330211656-vwt2dby"}[6.3 ScheduledThreadPoolExecutor 执行周期任务的步骤](#63-scheduledthreadpoolexecutor-执行周期任务的步骤)
    {: id="20210330211656-81wvoac"}
  {: id="20210330211656-txd7b23"}
- {: id="20210330211656-wc25g5q"}[七 线程池大小确定](#七-线程池大小确定)
  {: id="20210330211656-iyx2429"}
- {: id="20210330211656-hhxkwdw"}[八 参考](#八-参考)
  {: id="20210330211656-mwbbxwz"}
- {: id="20210330211656-5ehg2fh"}[九 其他推荐阅读](#九-其他推荐阅读)
  {: id="20210330211656-arqmryf"}
{: id="20210330211656-y412bhe"}

<!-- /TOC -->

## 一 使用线程池的好处
{: id="20210330211656-9p7ib1s"}

> **池化技术相比大家已经屡见不鲜了，线程池、数据库连接池、Http 连接池等等都是对这个思想的应用。池化技术的思想主要是为了减少每次获取资源的消耗，提高对资源的利用率。**
> {: id="20210330211656-ynguzqu"}
{: id="20210330211656-5m4c6u7"}

**线程池**提供了一种限制和管理资源（包括执行一个任务）。 每个**线程池**还维护一些基本统计信息，例如已完成任务的数量。
{: id="20210330211656-n11flxj"}

这里借用《Java 并发编程的艺术》提到的来说一下**使用线程池的好处**：
{: id="20210330211656-v1aildr"}

- {: id="20210330211656-6erzahv"}**降低资源消耗**。通过重复利用已创建的线程降低线程创建和销毁造成的消耗。
  {: id="20210330211656-p6u4y8e"}
- {: id="20210330211656-3k3bvm2"}**提高响应速度**。当任务到达时，任务可以不需要的等到线程创建就能立即执行。
  {: id="20210330211656-trojxz9"}
- {: id="20210330211656-361l45q"}**提高线程的可管理性**。线程是稀缺资源，如果无限制的创建，不仅会消耗系统资源，还会降低系统的稳定性，使用线程池可以进行统一的分配，调优和监控。
  {: id="20210330211656-ss96kgl"}
{: id="20210330211656-dap90fe"}

## 二 Executor 框架
{: id="20210330211656-8udc3r6"}

### 2.1 简介
{: id="20210330211656-vr2puqb"}

Executor 框架是 Java5 之后引进的，在 Java 5 之后，通过 Executor 来启动线程比使用 Thread 的 start 方法更好，除了更易管理，效率更好（用线程池实现，节约开销）外，还有关键的一点：有助于避免 this 逃逸问题。
{: id="20210330211656-ntk8nwt"}

> 补充：this 逃逸是指在构造函数返回之前其他线程就持有该对象的引用. 调用尚未构造完全的对象的方法可能引发令人疑惑的错误。
> {: id="20210330211656-yci72if"}
{: id="20210330211656-xg0hib0"}

Executor 框架不仅包括了线程池的管理，还提供了线程工厂、队列以及拒绝策略等，Executor 框架让并发编程变得更加简单。
{: id="20210330211656-v3258s2"}

### 2.2 Executor 框架结构(主要由三大部分组成)
{: id="20210330211656-6wvfbel"}

#### 1) 任务(`Runnable` /`Callable`)
{: id="20210330211656-0lbmg1t"}

执行任务需要实现的 **`Runnable` 接口** 或 **`Callable`接口**。**`Runnable` 接口**或 **`Callable` 接口** 实现类都可以被 **`ThreadPoolExecutor`** 或 **`ScheduledThreadPoolExecutor`** 执行。
{: id="20210330211656-bn8qu0u"}

#### 2) 任务的执行(`Executor`)
{: id="20210330211656-1f9yhwr"}

如下图所示，包括任务执行机制的核心接口 **`Executor`** ，以及继承自 `Executor` 接口的 **`ExecutorService` 接口。`ThreadPoolExecutor`** 和 **`ScheduledThreadPoolExecutor`** 这两个关键类实现了 **ExecutorService 接口**。
{: id="20210330211656-mdf9wv1"}

**这里提了很多底层的类关系，但是，实际上我们需要更多关注的是 `ThreadPoolExecutor` 这个类，这个类在我们实际使用线程池的过程中，使用频率还是非常高的。**
{: id="20210330211656-1ponvyq"}

> **注意：** 通过查看 `ScheduledThreadPoolExecutor` 源代码我们发现 `ScheduledThreadPoolExecutor` 实际上是继承了 `ThreadPoolExecutor` 并实现了 ScheduledExecutorService ，而 `ScheduledExecutorService` 又实现了 `ExecutorService`，正如我们下面给出的类关系图显示的一样。
> {: id="20210330211656-rmqrj1h"}
{: id="20210330211656-orygjk8"}

**`ThreadPoolExecutor` 类描述:**
{: id="20210330211656-mbl7b1j"}

```java
//AbstractExecutorService实现了ExecutorService接口
public class ThreadPoolExecutor extends AbstractExecutorService
```
{: id="20210330211656-l25p810"}

**`ScheduledThreadPoolExecutor` 类描述:**
{: id="20210330211656-tmh9jlr"}

```java
//ScheduledExecutorService继承ExecutorService接口
public class ScheduledThreadPoolExecutor
        extends ThreadPoolExecutor
        implements ScheduledExecutorService
```
{: id="20210330211656-tstb3yg"}

![任务的执行相关接口](images/java线程池学习总结/任务的执行相关接口.png)
{: id="20210330211656-26khkjh"}

#### 3) 异步计算的结果(`Future`)
{: id="20210330211656-gogkjcf"}

**`Future`** 接口以及 `Future` 接口的实现类 **`FutureTask`** 类都可以代表异步计算的结果。
{: id="20210330211656-dqttlse"}

当我们把 **`Runnable`接口** 或 **`Callable` 接口** 的实现类提交给 **`ThreadPoolExecutor`** 或 **`ScheduledThreadPoolExecutor`** 执行。（调用 `submit()` 方法时会返回一个 **`FutureTask`** 对象）
{: id="20210330211656-qgzkq5f"}

### 2.3 Executor 框架的使用示意图
{: id="20210330211656-yyfrkj5"}

![Executor 框架的使用示意图](images/java线程池学习总结/Executor框架的使用示意图.png)
{: id="20210330211656-e9tabz4"}

1. {: id="20210330211656-9ntyl0e"}**主线程首先要创建实现 `Runnable` 或者 `Callable` 接口的任务对象。**
   {: id="20210330211656-n9jy3cm"}
2. {: id="20210330211656-z5dfsvv"}**把创建完成的实现 `Runnable`/`Callable`接口的 对象直接交给 `ExecutorService` 执行**: `ExecutorService.execute（Runnable command）`）或者也可以把 `Runnable` 对象或`Callable` 对象提交给 `ExecutorService` 执行（`ExecutorService.submit（Runnable task）`或 `ExecutorService.submit（Callable <T> task）`）。
   {: id="20210330211656-yt1b0ym"}
3. {: id="20210330211656-cextl0b"}**如果执行 `ExecutorService.submit（…）`，`ExecutorService` 将返回一个实现`Future`接口的对象**（我们刚刚也提到过了执行 `execute()`方法和 `submit()`方法的区别，`submit()`会返回一个 `FutureTask 对象）。由于 FutureTask` 实现了 `Runnable`，我们也可以创建 `FutureTask`，然后直接交给 `ExecutorService` 执行。
   {: id="20210330211656-96eqp80"}
4. {: id="20210330211656-uqnt6ff"}**最后，主线程可以执行 `FutureTask.get()`方法来等待任务执行完成。主线程也可以执行 `FutureTask.cancel（boolean mayInterruptIfRunning）`来取消此任务的执行。**
   {: id="20210330211656-2sw5uja"}
{: id="20210330211656-nb4vv71"}

## 三 (重要)ThreadPoolExecutor 类简单介绍
{: id="20210330211656-ogu84pn"}

**线程池实现类 `ThreadPoolExecutor` 是 `Executor` 框架最核心的类。**
{: id="20210330211656-t4xegeg"}

### 3.1 ThreadPoolExecutor 类分析
{: id="20210330211656-xjxgqe2"}

`ThreadPoolExecutor` 类中提供的四个构造方法。我们来看最长的那个，其余三个都是在这个构造方法的基础上产生（其他几个构造方法说白点都是给定某些默认参数的构造方法比如默认制定拒绝策略是什么），这里就不贴代码讲了，比较简单。
{: id="20210330211656-rmh9j8g"}

```java
    /**
     * 用给定的初始参数创建一个新的ThreadPoolExecutor。
     */
    public ThreadPoolExecutor(int corePoolSize,//线程池的核心线程数量
                              int maximumPoolSize,//线程池的最大线程数
                              long keepAliveTime,//当线程数大于核心线程数时，多余的空闲线程存活的最长时间
                              TimeUnit unit,//时间单位
                              BlockingQueue<Runnable> workQueue,//任务队列，用来储存等待执行任务的队列
                              ThreadFactory threadFactory,//线程工厂，用来创建线程，一般默认即可
                              RejectedExecutionHandler handler//拒绝策略，当提交的任务过多而不能及时处理时，我们可以定制策略来处理任务
                               ) {
        if (corePoolSize < 0 ||
            maximumPoolSize <= 0 ||
            maximumPoolSize < corePoolSize ||
            keepAliveTime < 0)
            throw new IllegalArgumentException();
        if (workQueue == null || threadFactory == null || handler == null)
            throw new NullPointerException();
        this.corePoolSize = corePoolSize;
        this.maximumPoolSize = maximumPoolSize;
        this.workQueue = workQueue;
        this.keepAliveTime = unit.toNanos(keepAliveTime);
        this.threadFactory = threadFactory;
        this.handler = handler;
    }
```
{: id="20210330211656-ug8e0fv"}

**下面这些对创建 非常重要，在后面使用线程池的过程中你一定会用到！所以，务必拿着小本本记清楚。**
{: id="20210330211656-byr0zlk"}

**`ThreadPoolExecutor` 3 个最重要的参数：**
{: id="20210330211656-b96mt62"}

- {: id="20210330211656-4l843rc"}**`corePoolSize` :** 核心线程数线程数定义了最小可以同时运行的线程数量。
  {: id="20210330211656-qnqel5b"}
- {: id="20210330211656-znjntcg"}**`maximumPoolSize` :** 当队列中存放的任务达到队列容量的时候，当前可以同时运行的线程数量变为最大线程数。
  {: id="20210330211656-2egpfvb"}
- {: id="20210330211656-8lgfryj"}**`workQueue`:** 当新任务来的时候会先判断当前运行的线程数量是否达到核心线程数，如果达到的话，新任务就会被存放在队列中。
  {: id="20210330211656-8m3xa9b"}
{: id="20210330211656-s2wwdzx"}

`ThreadPoolExecutor`其他常见参数:
{: id="20210330211656-mkrwr80"}

1. {: id="20210330211656-4c53w4x"}**`keepAliveTime`**:当线程池中的线程数量大于 `corePoolSize` 的时候，如果这时没有新的任务提交，核心线程外的线程不会立即销毁，而是会等待，直到等待的时间超过了 `keepAliveTime`才会被回收销毁；
   {: id="20210330211656-e2efymc"}
2. {: id="20210330211656-n154sxw"}**`unit`** : `keepAliveTime` 参数的时间单位。
   {: id="20210330211656-1z208mv"}
3. {: id="20210330211656-iofzlfg"}**`threadFactory`** :executor 创建新线程的时候会用到。
   {: id="20210330211656-0qm3f81"}
4. {: id="20210330211656-6p61ipw"}**`handler`** :饱和策略。关于饱和策略下面单独介绍一下。
   {: id="20210330211656-tfll5kf"}
{: id="20210330211656-xgddwup"}

下面这张图可以加深你对线程池中各个参数的相互关系的理解（图片来源：《Java 性能调优实战》）：
{: id="20210330211656-vvcw1oo"}

![线程池各个参数的关系](images/java线程池学习总结/线程池各个参数之间的关系.png)
{: id="20210330211656-w9ekdgn"}

**`ThreadPoolExecutor` 饱和策略定义:**
{: id="20210330211656-sf5z4a4"}

如果当前同时运行的线程数量达到最大线程数量并且队列也已经被放满了任务时，`ThreadPoolTaskExecutor` 定义一些策略:
{: id="20210330211656-0fecfq6"}

- {: id="20210330211656-58ym4xu"}**`ThreadPoolExecutor.AbortPolicy`**：抛出 `RejectedExecutionException`来拒绝新任务的处理。
  {: id="20210330211656-fn5f98y"}
- {: id="20210330211656-8pxdxzu"}**`ThreadPoolExecutor.CallerRunsPolicy`**：调用执行自己的线程运行任务，也就是直接在调用`execute`方法的线程中运行(`run`)被拒绝的任务，如果执行程序已关闭，则会丢弃该任务。因此这种策略会降低对于新任务提交速度，影响程序的整体性能。如果您的应用程序可以承受此延迟并且你要求任何一个任务请求都要被执行的话，你可以选择这个策略。
  {: id="20210330211656-ddjz0k6"}
- {: id="20210330211656-3qufrv8"}**`ThreadPoolExecutor.DiscardPolicy`：** 不处理新任务，直接丢弃掉。
  {: id="20210330211656-xjwws0n"}
- {: id="20210330211656-q8ks7cs"}**`ThreadPoolExecutor.DiscardOldestPolicy`：** 此策略将丢弃最早的未处理的任务请求。
  {: id="20210330211656-ofi4hw8"}
{: id="20210330211656-5dggq06"}

举个例子：
{: id="20210330211656-gh846jb"}

> Spring 通过 `ThreadPoolTaskExecutor` 或者我们直接通过 `ThreadPoolExecutor` 的构造函数创建线程池的时候，当我们不指定 `RejectedExecutionHandler` 饱和策略的话来配置线程池的时候默认使用的是 `ThreadPoolExecutor.AbortPolicy`。在默认情况下，`ThreadPoolExecutor` 将抛出 `RejectedExecutionException` 来拒绝新来的任务 ，这代表你将丢失对这个任务的处理。 对于可伸缩的应用程序，建议使用 `ThreadPoolExecutor.CallerRunsPolicy`。当最大池被填满时，此策略为我们提供可伸缩队列。（这个直接查看 `ThreadPoolExecutor` 的构造函数源码就可以看出，比较简单的原因，这里就不贴代码了。）
> {: id="20210330211656-2oz6daa"}
{: id="20210330211656-f8nuluw"}

### 3.2 推荐使用 `ThreadPoolExecutor` 构造函数创建线程池
{: id="20210330211656-59cubxo"}

**在《阿里巴巴 Java 开发手册》“并发处理”这一章节，明确指出线程资源必须通过线程池提供，不允许在应用中自行显示创建线程。**
{: id="20210330211656-zdpj6q5"}

**为什么呢？**
{: id="20210330211656-4pf0hv6"}

> **使用线程池的好处是减少在创建和销毁线程上所消耗的时间以及系统资源开销，解决资源不足的问题。如果不使用线程池，有可能会造成系统创建大量同类线程而导致消耗完内存或者“过度切换”的问题。**
> {: id="20210330211656-dm8p963"}
{: id="20210330211656-r30xdav"}

**另外《阿里巴巴 Java 开发手册》中强制线程池不允许使用 Executors 去创建，而是通过 ThreadPoolExecutor 构造函数的方式，这样的处理方式让写的同学更加明确线程池的运行规则，规避资源耗尽的风险**
{: id="20210330211656-8p6ij1n"}

> Executors 返回线程池对象的弊端如下：
> {: id="20210330211656-s4lzh9k"}
>
> - {: id="20210330211656-m8jwl4k"}**`FixedThreadPool` 和 `SingleThreadExecutor`** ： 允许请求的队列长度为 Integer.MAX_VALUE,可能堆积大量的请求，从而导致 OOM。
>   {: id="20210330211656-zltidog"}
> - {: id="20210330211656-46fmess"}**CachedThreadPool 和 ScheduledThreadPool** ： 允许创建的线程数量为 Integer.MAX_VALUE ，可能会创建大量线程，从而导致 OOM。
>   {: id="20210330211656-zl5gqm4"}
> {: id="20210330211656-mx9u91e"}
{: id="20210330211656-97jnbwy"}

**方式一：通过`ThreadPoolExecutor`构造函数实现（推荐）**
![通过构造方法实现](images/java线程池学习总结/threadpoolexecutor构造函数.png)
**方式二：通过 Executor 框架的工具类 Executors 来实现**
我们可以创建三种类型的 ThreadPoolExecutor：
{: id="20210330211656-3t1ley5"}

- {: id="20210330211656-101hgsn"}**FixedThreadPool**
  {: id="20210330211656-bkjitan"}
- {: id="20210330211656-99whrrl"}**SingleThreadExecutor**
  {: id="20210330211656-ksjmnx6"}
- {: id="20210330211656-tgro6av"}**CachedThreadPool**
  {: id="20210330211656-q8o47jr"}
{: id="20210330211656-znrfid5"}

对应 Executors 工具类中的方法如图所示：
![通过Executor 框架的工具类Executors来实现](images/java线程池学习总结/Executors工具类.png)
{: id="20210330211656-dalmwu6"}

## 四 (重要)ThreadPoolExecutor 使用示例
{: id="20210330211656-wv64sb0"}

我们上面讲解了 `Executor`框架以及 `ThreadPoolExecutor` 类，下面让我们实战一下，来通过写一个 `ThreadPoolExecutor` 的小 Demo 来回顾上面的内容。
{: id="20210330211656-spt0a68"}

### 4.1 示例代码:`Runnable`+`ThreadPoolExecutor`
{: id="20210330211656-y6xu0aq"}

首先创建一个 `Runnable` 接口的实现类（当然也可以是 `Callable` 接口，我们上面也说了两者的区别。）
{: id="20210330211656-5u44t54"}

`MyRunnable.java`
{: id="20210330211656-w23xpct"}

```java
import java.util.Date;

/**
 * 这是一个简单的Runnable类，需要大约5秒钟来执行其任务。
 * @author shuang.kou
 */
public class MyRunnable implements Runnable {

    private String command;

    public MyRunnable(String s) {
        this.command = s;
    }

    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName() + " Start. Time = " + new Date());
        processCommand();
        System.out.println(Thread.currentThread().getName() + " End. Time = " + new Date());
    }

    private void processCommand() {
        try {
            Thread.sleep(5000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    @Override
    public String toString() {
        return this.command;
    }
}

```
{: id="20210330211656-jh3ag8g"}

编写测试程序，我们这里以阿里巴巴推荐的使用 `ThreadPoolExecutor` 构造函数自定义参数的方式来创建线程池。
{: id="20210330211656-lnpino4"}

`ThreadPoolExecutorDemo.java`
{: id="20210330211656-1oekqqv"}

```java
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;

public class ThreadPoolExecutorDemo {

    private static final int CORE_POOL_SIZE = 5;
    private static final int MAX_POOL_SIZE = 10;
    private static final int QUEUE_CAPACITY = 100;
    private static final Long KEEP_ALIVE_TIME = 1L;
    public static void main(String[] args) {

        //使用阿里巴巴推荐的创建线程池的方式
        //通过ThreadPoolExecutor构造函数自定义参数创建
        ThreadPoolExecutor executor = new ThreadPoolExecutor(
                CORE_POOL_SIZE,
                MAX_POOL_SIZE,
                KEEP_ALIVE_TIME,
                TimeUnit.SECONDS,
                new ArrayBlockingQueue<>(QUEUE_CAPACITY),
                new ThreadPoolExecutor.CallerRunsPolicy());

        for (int i = 0; i < 10; i++) {
            //创建WorkerThread对象（WorkerThread类实现了Runnable 接口）
            Runnable worker = new MyRunnable("" + i);
            //执行Runnable
            executor.execute(worker);
        }
        //终止线程池
        executor.shutdown();
        while (!executor.isTerminated()) {
        }
        System.out.println("Finished all threads");
    }
}

```
{: id="20210330211656-fpc8j4e"}

可以看到我们上面的代码指定了：
{: id="20210330211656-t9pkqjx"}

1. {: id="20210330211656-v3f3l44"}`corePoolSize`: 核心线程数为 5。
   {: id="20210330211656-w64q4u8"}
2. {: id="20210330211656-5mzw3hu"}`maximumPoolSize` ：最大线程数 10
   {: id="20210330211656-bizw1vl"}
3. {: id="20210330211656-p19mz9t"}`keepAliveTime` : 等待时间为 1L。
   {: id="20210330211656-saf8g4p"}
4. {: id="20210330211656-njcedqy"}`unit`: 等待时间的单位为 TimeUnit.SECONDS。
   {: id="20210330211656-wrajqot"}
5. {: id="20210330211656-30ust7q"}`workQueue`：任务队列为 `ArrayBlockingQueue`，并且容量为 100;
   {: id="20210330211656-6bex0dh"}
6. {: id="20210330211656-fo09jw6"}`handler`:饱和策略为 `CallerRunsPolicy`。
   {: id="20210330211656-2ar76m0"}
{: id="20210330211656-alfmh6m"}

**Output：**
{: id="20210330211656-qfau0dp"}

```
pool-1-thread-3 Start. Time = Sun Apr 12 11:14:37 CST 2020
pool-1-thread-5 Start. Time = Sun Apr 12 11:14:37 CST 2020
pool-1-thread-2 Start. Time = Sun Apr 12 11:14:37 CST 2020
pool-1-thread-1 Start. Time = Sun Apr 12 11:14:37 CST 2020
pool-1-thread-4 Start. Time = Sun Apr 12 11:14:37 CST 2020
pool-1-thread-3 End. Time = Sun Apr 12 11:14:42 CST 2020
pool-1-thread-4 End. Time = Sun Apr 12 11:14:42 CST 2020
pool-1-thread-1 End. Time = Sun Apr 12 11:14:42 CST 2020
pool-1-thread-5 End. Time = Sun Apr 12 11:14:42 CST 2020
pool-1-thread-1 Start. Time = Sun Apr 12 11:14:42 CST 2020
pool-1-thread-2 End. Time = Sun Apr 12 11:14:42 CST 2020
pool-1-thread-5 Start. Time = Sun Apr 12 11:14:42 CST 2020
pool-1-thread-4 Start. Time = Sun Apr 12 11:14:42 CST 2020
pool-1-thread-3 Start. Time = Sun Apr 12 11:14:42 CST 2020
pool-1-thread-2 Start. Time = Sun Apr 12 11:14:42 CST 2020
pool-1-thread-1 End. Time = Sun Apr 12 11:14:47 CST 2020
pool-1-thread-4 End. Time = Sun Apr 12 11:14:47 CST 2020
pool-1-thread-5 End. Time = Sun Apr 12 11:14:47 CST 2020
pool-1-thread-3 End. Time = Sun Apr 12 11:14:47 CST 2020
pool-1-thread-2 End. Time = Sun Apr 12 11:14:47 CST 2020

```
{: id="20210330211656-alj893j"}

### 4.2 线程池原理分析
{: id="20210330211656-xtecq1o"}

承接 4.1 节，我们通过代码输出结果可以看出：**线程首先会先执行 5 个任务，然后这些任务有任务被执行完的话，就会去拿新的任务执行。** 大家可以先通过上面讲解的内容，分析一下到底是咋回事？（自己独立思考一会）
{: id="20210330211656-epnlm21"}

现在，我们就分析上面的输出内容来简单分析一下线程池原理。
{: id="20210330211656-idn9v3e"}

**为了搞懂线程池的原理，我们需要首先分析一下 `execute`方法。** 在 4.1 节中的 Demo 中我们使用 `executor.execute(worker)`来提交一个任务到线程池中去，这个方法非常重要，下面我们来看看它的源码：
{: id="20210330211656-qoffj4j"}

```java
   // 存放线程池的运行状态 (runState) 和线程池内有效线程的数量 (workerCount)
   private final AtomicInteger ctl = new AtomicInteger(ctlOf(RUNNING, 0));
   
    private static int workerCountOf(int c) {
        return c & CAPACITY;
    }
    //任务队列
    private final BlockingQueue<Runnable> workQueue;

    public void execute(Runnable command) {
        // 如果任务为null，则抛出异常。
        if (command == null)
            throw new NullPointerException();
        // ctl 中保存的线程池当前的一些状态信息
        int c = ctl.get();

        //  下面会涉及到 3 步 操作
        // 1.首先判断当前线程池中之行的任务数量是否小于 corePoolSize
        // 如果小于的话，通过addWorker(command, true)新建一个线程，并将任务(command)添加到该线程中；然后，启动该线程从而执行任务。
        if (workerCountOf(c) < corePoolSize) {
            if (addWorker(command, true))
                return;
            c = ctl.get();
        }
        // 2.如果当前之行的任务数量大于等于 corePoolSize 的时候就会走到这里
        // 通过 isRunning 方法判断线程池状态，线程池处于 RUNNING 状态才会被并且队列可以加入任务，该任务才会被加入进去
        if (isRunning(c) && workQueue.offer(command)) {
            int recheck = ctl.get();
            // 再次获取线程池状态，如果线程池状态不是 RUNNING 状态就需要从任务队列中移除任务，并尝试判断线程是否全部执行完毕。同时执行拒绝策略。
            if (!isRunning(recheck) && remove(command))
                reject(command);
                // 如果当前线程池为空就新创建一个线程并执行。
            else if (workerCountOf(recheck) == 0)
                addWorker(null, false);
        }
        //3. 通过addWorker(command, false)新建一个线程，并将任务(command)添加到该线程中；然后，启动该线程从而执行任务。
        //如果addWorker(command, false)执行失败，则通过reject()执行相应的拒绝策略的内容。
        else if (!addWorker(command, false))
            reject(command);
    }
```
{: id="20210330211656-uqa724m"}

通过下图可以更好的对上面这 3 步做一个展示，下图是我为了省事直接从网上找到，原地址不明。
{: id="20210330211656-9vpawti"}

![图解线程池实现原理](images/java线程池学习总结/图解线程池实现原理.png)
{: id="20210330211656-ol9ok2c"}

**`addWorker` 这个方法主要用来创建新的工作线程，如果返回true说明创建和启动工作线程成功，否则的话返回的就是false。**
{: id="20210330211656-ozqxyiw"}

```java
    // 全局锁，并发操作必备
    private final ReentrantLock mainLock = new ReentrantLock();
    // 跟踪线程池的最大大小，只有在持有全局锁mainLock的前提下才能访问此集合
    private int largestPoolSize;
    // 工作线程集合，存放线程池中所有的（活跃的）工作线程，只有在持有全局锁mainLock的前提下才能访问此集合
    private final HashSet<Worker> workers = new HashSet<>();
    //获取线程池状态
    private static int runStateOf(int c)     { return c & ~CAPACITY; }
    //判断线程池的状态是否为 Running
    private static boolean isRunning(int c) {
        return c < SHUTDOWN;
    }


    /**
     * 添加新的工作线程到线程池
     * @param firstTask 要执行
     * @param core参数为true的话表示使用线程池的基本大小，为false使用线程池最大大小
     * @return 添加成功就返回true否则返回false
     */
   private boolean addWorker(Runnable firstTask, boolean core) {
        retry:
        for (;;) {
            //这两句用来获取线程池的状态
            int c = ctl.get();
            int rs = runStateOf(c);

            // Check if queue empty only if necessary.
            if (rs >= SHUTDOWN &&
                ! (rs == SHUTDOWN &&
                   firstTask == null &&
                   ! workQueue.isEmpty()))
                return false;

            for (;;) {
               //获取线程池中线程的数量
                int wc = workerCountOf(c);
                // core参数为true的话表明队列也满了，线程池大小变为 maximumPoolSize 
                if (wc >= CAPACITY ||
                    wc >= (core ? corePoolSize : maximumPoolSize))
                    return false;
               //原子操作将workcount的数量加1
                if (compareAndIncrementWorkerCount(c))
                    break retry;
                // 如果线程的状态改变了就再次执行上述操作
                c = ctl.get();  
                if (runStateOf(c) != rs)
                    continue retry;
                // else CAS failed due to workerCount change; retry inner loop
            }
        }
        // 标记工作线程是否启动成功
        boolean workerStarted = false;
        // 标记工作线程是否创建成功
        boolean workerAdded = false;
        Worker w = null;
        try {
        
            w = new Worker(firstTask);
            final Thread t = w.thread;
            if (t != null) {
              // 加锁
                final ReentrantLock mainLock = this.mainLock;
                mainLock.lock();
                try {
                   //获取线程池状态
                    int rs = runStateOf(ctl.get());
                   //rs < SHUTDOWN 如果线程池状态依然为RUNNING,并且线程的状态是存活的话，就会将工作线程添加到工作线程集合中
                  //(rs=SHUTDOWN && firstTask == null)如果线程池状态小于STOP，也就是RUNNING或者SHUTDOWN状态下，同时传入的任务实例firstTask为null，则需要添加到工作线程集合和启动新的Worker
                   // firstTask == null证明只新建线程而不执行任务
                    if (rs < SHUTDOWN ||
                        (rs == SHUTDOWN && firstTask == null)) {
                        if (t.isAlive()) // precheck that t is startable
                            throw new IllegalThreadStateException();
                        workers.add(w);
                       //更新当前工作线程的最大容量
                        int s = workers.size();
                        if (s > largestPoolSize)
                            largestPoolSize = s;
                      // 工作线程是否启动成功
                        workerAdded = true;
                    }
                } finally {
                    // 释放锁
                    mainLock.unlock();
                }
                //// 如果成功添加工作线程，则调用Worker内部的线程实例t的Thread#start()方法启动真实的线程实例
                if (workerAdded) {
                    t.start();
                  /// 标记线程启动成功
                    workerStarted = true;
                }
            }
        } finally {
           // 线程启动失败，需要从工作线程中移除对应的Worker
            if (! workerStarted)
                addWorkerFailed(w);
        }
        return workerStarted;
    }
```
{: id="20210330211656-4459q10"}

更多关于线程池源码分析的内容推荐这篇文章：《[JUC线程池ThreadPoolExecutor源码分析](http://www.throwable.club/2019/07/15/java-concurrency-thread-pool-executor/)》
{: id="20210330211656-xm9e9fh"}

现在，让我们在回到 4.1 节我们写的 Demo， 现在应该是不是很容易就可以搞懂它的原理了呢？
{: id="20210330211656-slfo42g"}

没搞懂的话，也没关系，可以看看我的分析：
{: id="20210330211656-d4jjw78"}

> 我们在代码中模拟了 10 个任务，我们配置的核心线程数为 5 、等待队列容量为 100 ，所以每次只可能存在 5 个任务同时执行，剩下的 5 个任务会被放到等待队列中去。当前的5个任务中如果有任务被执行完了，线程池就会去拿新的任务执行。
> {: id="20210330211656-j4hzaia"}
{: id="20210330211656-mvi0y7d"}

### 4.3 几个常见的对比
{: id="20210330211656-94xw0nu"}

#### 4.3.1 `Runnable` vs `Callable`
{: id="20210330211656-l4h4ey4"}

`Runnable`自 Java 1.0 以来一直存在，但`Callable`仅在 Java 1.5 中引入,目的就是为了来处理`Runnable`不支持的用例。**`Runnable` 接口**不会返回结果或抛出检查异常，但是**`Callable` 接口**可以。所以，如果任务不需要返回结果或抛出异常推荐使用 **`Runnable` 接口**，这样代码看起来会更加简洁。
{: id="20210330211656-u0kn43p"}

工具类 `Executors` 可以实现 `Runnable` 对象和 `Callable` 对象之间的相互转换。（`Executors.callable（Runnable task`）或 `Executors.callable（Runnable task，Object resule）`）。
{: id="20210330211656-fe4zeb5"}

`Runnable.java`
{: id="20210330211656-fwy60ob"}

```java
@FunctionalInterface
public interface Runnable {
   /**
    * 被线程执行，没有返回值也无法抛出异常
    */
    public abstract void run();
}
```
{: id="20210330211656-5srroa3"}

`Callable.java`
{: id="20210330211656-1rm3jji"}

```java
@FunctionalInterface
public interface Callable<V> {
    /**
     * 计算结果，或在无法这样做时抛出异常。
     * @return 计算得出的结果
     * @throws 如果无法计算结果，则抛出异常
     */
    V call() throws Exception;
}

```
{: id="20210330211656-ekeqr1v"}

#### 4.3.2 `execute()` vs `submit()`
{: id="20210330211656-j57aea1"}

1. {: id="20210330211656-gir9en2"}**`execute()`方法用于提交不需要返回值的任务，所以无法判断任务是否被线程池执行成功与否；**
   {: id="20210330211656-0p0hxa6"}
2. {: id="20210330211656-aubtdgu"}**`submit()`方法用于提交需要返回值的任务。线程池会返回一个 `Future` 类型的对象，通过这个 `Future` 对象可以判断任务是否执行成功** ，并且可以通过 `Future` 的 `get()`方法来获取返回值，`get()`方法会阻塞当前线程直到任务完成，而使用 `get（long timeout，TimeUnit unit）`方法则会阻塞当前线程一段时间后立即返回，这时候有可能任务没有执行完。
   {: id="20210330211656-rxto283"}
{: id="20210330211656-teb9f9e"}

我们以**`AbstractExecutorService`**接口中的一个 `submit` 方法为例子来看看源代码：
{: id="20210330211656-ksg395s"}

```java
    public Future<?> submit(Runnable task) {
        if (task == null) throw new NullPointerException();
        RunnableFuture<Void> ftask = newTaskFor(task, null);
        execute(ftask);
        return ftask;
    }
```
{: id="20210330211656-ye3vg7b"}

上面方法调用的 `newTaskFor` 方法返回了一个 `FutureTask` 对象。
{: id="20210330211656-siwlsm6"}

```java
    protected <T> RunnableFuture<T> newTaskFor(Runnable runnable, T value) {
        return new FutureTask<T>(runnable, value);
    }
```
{: id="20210330211656-fbt9tgq"}

我们再来看看`execute()`方法：
{: id="20210330211656-766xyfr"}

```java
    public void execute(Runnable command) {
      ...
    }
```
{: id="20210330211656-22arlsk"}

#### 4.3.3 `shutdown()`VS`shutdownNow()`
{: id="20210330211656-5lzwjnb"}

- {: id="20210330211656-1b4qvfl"}**`shutdown（）`** :关闭线程池，线程池的状态变为 `SHUTDOWN`。线程池不再接受新任务了，但是队列里的任务得执行完毕。
  {: id="20210330211656-0bw3l9l"}
- {: id="20210330211656-vluz6rl"}**`shutdownNow（）`** :关闭线程池，线程的状态变为 `STOP`。线程池会终止当前正在运行的任务，并停止处理排队的任务并返回正在等待执行的 List。
  {: id="20210330211656-bgiai5m"}
{: id="20210330211656-qxdnm7w"}

#### 4.3.2 `isTerminated()` VS `isShutdown()`
{: id="20210330211656-u0q0scw"}

- {: id="20210330211656-0lm1djg"}**`isShutDown`** 当调用 `shutdown()` 方法后返回为 true。
  {: id="20210330211656-lwvzep5"}
- {: id="20210330211656-nafzr76"}**`isTerminated`** 当调用 `shutdown()` 方法后，并且所有提交的任务完成后返回为 true
  {: id="20210330211656-zvmqkoo"}
{: id="20210330211656-iow8sxu"}

### 4.4 加餐:`Callable`+`ThreadPoolExecutor`示例代码
{: id="20210330211656-yf6szk7"}

`MyCallable.java`
{: id="20210330211656-dii9ptz"}

```java

import java.util.concurrent.Callable;

public class MyCallable implements Callable<String> {
    @Override
    public String call() throws Exception {
        Thread.sleep(1000);
        //返回执行当前 Callable 的线程名字
        return Thread.currentThread().getName();
    }
}
```
{: id="20210330211656-vqlvgg2"}

`CallableDemo.java`
{: id="20210330211656-hc7yfqg"}

```java

import java.util.ArrayList;
import java.util.Date;
import java.util.List;
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.Future;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;

public class CallableDemo {

    private static final int CORE_POOL_SIZE = 5;
    private static final int MAX_POOL_SIZE = 10;
    private static final int QUEUE_CAPACITY = 100;
    private static final Long KEEP_ALIVE_TIME = 1L;

    public static void main(String[] args) {

        //使用阿里巴巴推荐的创建线程池的方式
        //通过ThreadPoolExecutor构造函数自定义参数创建
        ThreadPoolExecutor executor = new ThreadPoolExecutor(
                CORE_POOL_SIZE,
                MAX_POOL_SIZE,
                KEEP_ALIVE_TIME,
                TimeUnit.SECONDS,
                new ArrayBlockingQueue<>(QUEUE_CAPACITY),
                new ThreadPoolExecutor.CallerRunsPolicy());

        List<Future<String>> futureList = new ArrayList<>();
        Callable<String> callable = new MyCallable();
        for (int i = 0; i < 10; i++) {
            //提交任务到线程池
            Future<String> future = executor.submit(callable);
            //将返回值 future 添加到 list，我们可以通过 future 获得 执行 Callable 得到的返回值
            futureList.add(future);
        }
        for (Future<String> fut : futureList) {
            try {
                System.out.println(new Date() + "::" + fut.get());
            } catch (InterruptedException | ExecutionException e) {
                e.printStackTrace();
            }
        }
        //关闭线程池
        executor.shutdown();
    }
}
```
{: id="20210330211656-4hp90wl"}

Output:
{: id="20210330211656-eq0zxqm"}

```
Wed Nov 13 13:40:41 CST 2019::pool-1-thread-1
Wed Nov 13 13:40:42 CST 2019::pool-1-thread-2
Wed Nov 13 13:40:42 CST 2019::pool-1-thread-3
Wed Nov 13 13:40:42 CST 2019::pool-1-thread-4
Wed Nov 13 13:40:42 CST 2019::pool-1-thread-5
Wed Nov 13 13:40:42 CST 2019::pool-1-thread-3
Wed Nov 13 13:40:43 CST 2019::pool-1-thread-2
Wed Nov 13 13:40:43 CST 2019::pool-1-thread-1
Wed Nov 13 13:40:43 CST 2019::pool-1-thread-4
Wed Nov 13 13:40:43 CST 2019::pool-1-thread-5
```
{: id="20210330211656-qlonsch"}

## 五 几种常见的线程池详解
{: id="20210330211656-czscpn7"}

### 5.1 FixedThreadPool
{: id="20210330211656-vh54a1w"}

#### 5.1.1 介绍
{: id="20210330211656-l6qpquv"}

`FixedThreadPool` 被称为可重用固定线程数的线程池。通过 Executors 类中的相关源代码来看一下相关实现：
{: id="20210330211656-j03jw37"}

```java
   /**
     * 创建一个可重用固定数量线程的线程池
     */
    public static ExecutorService newFixedThreadPool(int nThreads, ThreadFactory threadFactory) {
        return new ThreadPoolExecutor(nThreads, nThreads,
                                      0L, TimeUnit.MILLISECONDS,
                                      new LinkedBlockingQueue<Runnable>(),
                                      threadFactory);
    }
```
{: id="20210330211656-pfz4ddg"}

另外还有一个 `FixedThreadPool` 的实现方法，和上面的类似，所以这里不多做阐述：
{: id="20210330211656-yutfmt6"}

```java
    public static ExecutorService newFixedThreadPool(int nThreads) {
        return new ThreadPoolExecutor(nThreads, nThreads,
                                      0L, TimeUnit.MILLISECONDS,
                                      new LinkedBlockingQueue<Runnable>());
    }
```
{: id="20210330211656-fukiwl4"}

**从上面源代码可以看出新创建的 `FixedThreadPool` 的 `corePoolSize` 和 `maximumPoolSize` 都被设置为 nThreads，这个 nThreads 参数是我们使用的时候自己传递的。**
{: id="20210330211656-br14g1x"}

#### 5.1.2 执行任务过程介绍
{: id="20210330211656-9fzke25"}

`FixedThreadPool` 的 `execute()` 方法运行示意图（该图片来源：《Java 并发编程的艺术》）：
{: id="20210330211656-b2ur8qj"}

![FixedThreadPool的execute()方法运行示意图](images/java线程池学习总结/FixedThreadPool.png)
{: id="20210330211656-ppf9p6l"}

**上图说明：**
{: id="20210330211656-ghfqz2q"}

1. {: id="20210330211656-k56lk96"}如果当前运行的线程数小于 corePoolSize， 如果再来新任务的话，就创建新的线程来执行任务；
   {: id="20210330211656-e9x5d76"}
2. {: id="20210330211656-zjk9nu2"}当前运行的线程数等于 corePoolSize 后， 如果再来新任务的话，会将任务加入 `LinkedBlockingQueue`；
   {: id="20210330211656-ucn28j1"}
3. {: id="20210330211656-k59u0l0"}线程池中的线程执行完 手头的任务后，会在循环中反复从 `LinkedBlockingQueue` 中获取任务来执行；
   {: id="20210330211656-06wxby8"}
{: id="20210330211656-0c1a3p9"}

#### 5.1.3 为什么不推荐使用`FixedThreadPool`？
{: id="20210330211656-xu9ltbw"}

**`FixedThreadPool` 使用无界队列 `LinkedBlockingQueue`（队列的容量为 Intger.MAX_VALUE）作为线程池的工作队列会对线程池带来如下影响 ：**
{: id="20210330211656-05d4fj2"}

1. {: id="20210330211656-1qtn719"}当线程池中的线程数达到 `corePoolSize` 后，新任务将在无界队列中等待，因此线程池中的线程数不会超过 corePoolSize；
   {: id="20210330211656-tphlxab"}
2. {: id="20210330211656-i56yt8w"}由于使用无界队列时 `maximumPoolSize` 将是一个无效参数，因为不可能存在任务队列满的情况。所以，通过创建 `FixedThreadPool`的源码可以看出创建的 `FixedThreadPool` 的 `corePoolSize` 和 `maximumPoolSize` 被设置为同一个值。
   {: id="20210330211656-kbylop8"}
3. {: id="20210330211656-8olxokz"}由于 1 和 2，使用无界队列时 `keepAliveTime` 将是一个无效参数；
   {: id="20210330211656-smsrke5"}
4. {: id="20210330211656-m2s1nv7"}运行中的 `FixedThreadPool`（未执行 `shutdown()`或 `shutdownNow()`）不会拒绝任务，在任务比较多的时候会导致 OOM（内存溢出）。
   {: id="20210330211656-rxmad4o"}
{: id="20210330211656-94url16"}

### 5.2 SingleThreadExecutor 详解
{: id="20210330211656-6mh8i4k"}

#### 5.2.1 介绍
{: id="20210330211656-0gy7ea4"}

`SingleThreadExecutor` 是只有一个线程的线程池。下面看看**SingleThreadExecutor 的实现：**
{: id="20210330211656-k0s66gj"}

```java
   /**
     *返回只有一个线程的线程池
     */
    public static ExecutorService newSingleThreadExecutor(ThreadFactory threadFactory) {
        return new FinalizableDelegatedExecutorService
            (new ThreadPoolExecutor(1, 1,
                                    0L, TimeUnit.MILLISECONDS,
                                    new LinkedBlockingQueue<Runnable>(),
                                    threadFactory));
    }
```
{: id="20210330211656-9riiskz"}

```java
   public static ExecutorService newSingleThreadExecutor() {
        return new FinalizableDelegatedExecutorService
            (new ThreadPoolExecutor(1, 1,
                                    0L, TimeUnit.MILLISECONDS,
                                    new LinkedBlockingQueue<Runnable>()));
    }
```
{: id="20210330211656-74w5cc0"}

从上面源代码可以看出新创建的 `SingleThreadExecutor` 的 `corePoolSize` 和 `maximumPoolSize` 都被设置为 1.其他参数和 `FixedThreadPool` 相同。
{: id="20210330211656-fbmgdyc"}

#### 5.2.2 执行任务过程介绍
{: id="20210330211656-13m3xwa"}

**`SingleThreadExecutor` 的运行示意图（该图片来源：《Java 并发编程的艺术》）：**
![SingleThreadExecutor的运行示意图](images/java线程池学习总结/SingleThreadExecutor.png)
{: id="20210330211656-1nb8h6x"}

**上图说明;**
{: id="20210330211656-lnanxq1"}

1. {: id="20210330211656-qkyep8u"}如果当前运行的线程数少于 corePoolSize，则创建一个新的线程执行任务；
   {: id="20210330211656-i4pags0"}
2. {: id="20210330211656-m9sogkv"}当前线程池中有一个运行的线程后，将任务加入 `LinkedBlockingQueue`
   {: id="20210330211656-h575cik"}
3. {: id="20210330211656-3zb095r"}线程执行完当前的任务后，会在循环中反复从`LinkedBlockingQueue` 中获取任务来执行；
   {: id="20210330211656-h13tymh"}
{: id="20210330211656-9vhcy2f"}

#### 5.2.3 为什么不推荐使用`SingleThreadExecutor`？
{: id="20210330211656-p5vd7p1"}

`SingleThreadExecutor` 使用无界队列 `LinkedBlockingQueue` 作为线程池的工作队列（队列的容量为 Intger.MAX_VALUE）。`SingleThreadExecutor` 使用无界队列作为线程池的工作队列会对线程池带来的影响与 `FixedThreadPool` 相同。说简单点就是可能会导致 OOM，
{: id="20210330211656-w3xr3n7"}

### 5.3 CachedThreadPool 详解
{: id="20210330211656-7mvr8ds"}

#### 5.3.1 介绍
{: id="20210330211656-mx75zb6"}

`CachedThreadPool` 是一个会根据需要创建新线程的线程池。下面通过源码来看看 `CachedThreadPool` 的实现：
{: id="20210330211656-gjmvp5r"}

```java
    /**
     * 创建一个线程池，根据需要创建新线程，但会在先前构建的线程可用时重用它。
     */
    public static ExecutorService newCachedThreadPool(ThreadFactory threadFactory) {
        return new ThreadPoolExecutor(0, Integer.MAX_VALUE,
                                      60L, TimeUnit.SECONDS,
                                      new SynchronousQueue<Runnable>(),
                                      threadFactory);
    }

```
{: id="20210330211656-fi2hhie"}

```java
    public static ExecutorService newCachedThreadPool() {
        return new ThreadPoolExecutor(0, Integer.MAX_VALUE,
                                      60L, TimeUnit.SECONDS,
                                      new SynchronousQueue<Runnable>());
    }
```
{: id="20210330211656-xzps1k2"}

`CachedThreadPool` 的`corePoolSize` 被设置为空（0），`maximumPoolSize`被设置为 Integer.MAX.VALUE，即它是无界的，这也就意味着如果主线程提交任务的速度高于 `maximumPool` 中线程处理任务的速度时，`CachedThreadPool` 会不断创建新的线程。极端情况下，这样会导致耗尽 cpu 和内存资源。
{: id="20210330211656-b19e3dc"}

#### 5.3.2 执行任务过程介绍
{: id="20210330211656-e8lpy8s"}

**CachedThreadPool 的 execute()方法的执行示意图（该图片来源：《Java 并发编程的艺术》）：**
![CachedThreadPool的execute()方法的执行示意图](images/java线程池学习总结/CachedThreadPool-execute.png)
{: id="20210330211656-ab71k0v"}

**上图说明：**
{: id="20210330211656-rmrdivm"}

1. {: id="20210330211656-caa6wft"}首先执行 `SynchronousQueue.offer(Runnable task)` 提交任务到任务队列。如果当前 `maximumPool` 中有闲线程正在执行 `SynchronousQueue.poll(keepAliveTime,TimeUnit.NANOSECONDS)`，那么主线程执行 offer 操作与空闲线程执行的 `poll` 操作配对成功，主线程把任务交给空闲线程执行，`execute()`方法执行完成，否则执行下面的步骤 2；
   {: id="20210330211656-miayzdc"}
2. {: id="20210330211656-vywe7ww"}当初始 `maximumPool` 为空，或者 `maximumPool` 中没有空闲线程时，将没有线程执行 `SynchronousQueue.poll(keepAliveTime,TimeUnit.NANOSECONDS)`。这种情况下，步骤 1 将失败，此时 `CachedThreadPool` 会创建新线程执行任务，execute 方法执行完成；
   {: id="20210330211656-49eucpx"}
{: id="20210330211656-6248hwz"}

#### 5.3.3 为什么不推荐使用`CachedThreadPool`？
{: id="20210330211656-1c9y560"}

`CachedThreadPool`允许创建的线程数量为 Integer.MAX_VALUE ，可能会创建大量线程，从而导致 OOM。
{: id="20210330211656-qlno22v"}

## 六 ScheduledThreadPoolExecutor 详解
{: id="20210330211656-20mjhgh"}

**`ScheduledThreadPoolExecutor` 主要用来在给定的延迟后运行任务，或者定期执行任务。** 这个在实际项目中基本不会被用到，因为有其他方案选择比如`quartz`。大家只需要简单了解一下它的思想。关于如何在 Spring Boot 中 实现定时任务，可以查看这篇文章[《5 分钟搞懂如何在 Spring Boot 中 Schedule Tasks》](https://github.com/Snailclimb/springboot-guide/blob/master/docs/advanced/SpringBoot-ScheduleTasks.md)。
{: id="20210330211656-h14bpjv"}

### 6.1 简介
{: id="20210330211656-3smrcqi"}

**`ScheduledThreadPoolExecutor` 使用的任务队列 `DelayQueue` 封装了一个 `PriorityQueue`，`PriorityQueue` 会对队列中的任务进行排序，执行所需时间短的放在前面先被执行(`ScheduledFutureTask` 的 `time` 变量小的先执行)，如果执行所需时间相同则先提交的任务将被先执行(`ScheduledFutureTask` 的 `squenceNumber` 变量小的先执行)。**
{: id="20210330211656-55e94cm"}

**`ScheduledThreadPoolExecutor` 和 `Timer` 的比较：**
{: id="20210330211656-qznyvpm"}

- {: id="20210330211656-2mo7b3z"}`Timer` 对系统时钟的变化敏感，`ScheduledThreadPoolExecutor`不是；
  {: id="20210330211656-xl7zemt"}
- {: id="20210330211656-yxodpr5"}`Timer` 只有一个执行线程，因此长时间运行的任务可以延迟其他任务。 `ScheduledThreadPoolExecutor` 可以配置任意数量的线程。 此外，如果你想（通过提供 ThreadFactory），你可以完全控制创建的线程;
  {: id="20210330211656-18dlxhp"}
- {: id="20210330211656-6md4mug"}在`TimerTask` 中抛出的运行时异常会杀死一个线程，从而导致 `Timer` 死机:-( ...即计划任务将不再运行。`ScheduledThreadExecutor` 不仅捕获运行时异常，还允许您在需要时处理它们（通过重写 `afterExecute` 方法`ThreadPoolExecutor`）。抛出异常的任务将被取消，但其他任务将继续运行。
  {: id="20210330211656-kghh8zw"}
{: id="20210330211656-3tf8x7s"}

**综上，在 JDK1.5 之后，你没有理由再使用 Timer 进行任务调度了。**
{: id="20210330211656-bu42yuj"}

> **备注：** Quartz 是一个由 java 编写的任务调度库，由 OpenSymphony 组织开源出来。在实际项目开发中使用 Quartz 的还是居多，比较推荐使用 Quartz。因为 Quartz 理论上能够同时对上万个任务进行调度，拥有丰富的功能特性，包括任务调度、任务持久化、可集群化、插件等等。
> {: id="20210330211656-if46ygj"}
{: id="20210330211656-3m18q3p"}

### 6.2 运行机制
{: id="20210330211656-bow7je6"}

![ScheduledThreadPoolExecutor运行机制](images/java线程池学习总结/ScheduledThreadPoolExecutor机制.png)
{: id="20210330211656-tmbh2bx"}

**`ScheduledThreadPoolExecutor` 的执行主要分为两大部分：**
{: id="20210330211656-tyb0b1l"}

1. {: id="20210330211656-hcpz9v2"}当调用 `ScheduledThreadPoolExecutor` 的 **`scheduleAtFixedRate()`** 方法或者 **`scheduleWithFixedDelay()`** 方法时，会向 `ScheduledThreadPoolExecutor` 的 **`DelayQueue`** 添加一个实现了 **`RunnableScheduledFuture`** 接口的 **`ScheduledFutureTask`** 。
   {: id="20210330211656-nu4va2c"}
2. {: id="20210330211656-7xwkpoh"}线程池中的线程从 `DelayQueue` 中获取 `ScheduledFutureTask`，然后执行任务。
   {: id="20210330211656-03vvdju"}
{: id="20210330211656-pc9teg1"}

**`ScheduledThreadPoolExecutor` 为了实现周期性的执行任务，对 `ThreadPoolExecutor`做了如下修改：**
{: id="20210330211656-ibz9ezt"}

- {: id="20210330211656-ltfg100"}使用 **`DelayQueue`** 作为任务队列；
  {: id="20210330211656-o7yoh84"}
- {: id="20210330211656-8qa0k83"}获取任务的方不同
  {: id="20210330211656-kj0jep1"}
- {: id="20210330211656-410fh7z"}执行周期任务后，增加了额外的处理
  {: id="20210330211656-kvf8q33"}
{: id="20210330211656-9t9bpx7"}

### 6.3 ScheduledThreadPoolExecutor 执行周期任务的步骤
{: id="20210330211656-xl4o0q8"}

![ScheduledThreadPoolExecutor执行周期任务的步骤](images/java线程池学习总结/ScheduledThreadPoolExecutor执行周期任务步骤.png)
{: id="20210330211656-stvtqvm"}

1. {: id="20210330211656-uobl2tw"}线程 1 从 `DelayQueue` 中获取已到期的 `ScheduledFutureTask（DelayQueue.take()）`。到期任务是指 `ScheduledFutureTask`的 time 大于等于当前系统的时间；
   {: id="20210330211656-72b1bhs"}
2. {: id="20210330211656-2ke3jbq"}线程 1 执行这个 `ScheduledFutureTask`；
   {: id="20210330211656-9zdp49x"}
3. {: id="20210330211656-ywz0buy"}线程 1 修改 `ScheduledFutureTask` 的 time 变量为下次将要被执行的时间；
   {: id="20210330211656-sg88u2m"}
4. {: id="20210330211656-wjtfz0k"}线程 1 把这个修改 time 之后的 `ScheduledFutureTask` 放回 `DelayQueue` 中（`DelayQueue.add()`)。
   {: id="20210330211656-5eks6ly"}
{: id="20210330211656-tleut4v"}

## 七 线程池大小确定
{: id="20210330211656-mmv1wkf"}

**线程池数量的确定一直是困扰着程序员的一个难题，大部分程序员在设定线程池大小的时候就是随心而定。**
{: id="20210330211656-bw65kjf"}

很多人甚至可能都会觉得把线程池配置过大一点比较好！我觉得这明显是有问题的。就拿我们生活中非常常见的一例子来说：**并不是人多就能把事情做好，增加了沟通交流成本。你本来一件事情只需要 3 个人做，你硬是拉来了 6 个人，会提升做事效率嘛？我想并不会。** 线程数量过多的影响也是和我们分配多少人做事情一样，对于多线程这个场景来说主要是增加了**上下文切换**成本。不清楚什么是上下文切换的话，可以看我下面的介绍。
{: id="20210330211656-pqx4c4s"}

> 上下文切换：
> {: id="20210330211656-lfnbof5"}
>
> 多线程编程中一般线程的个数都大于 CPU 核心的个数，而一个 CPU 核心在任意时刻只能被一个线程使用，为了让这些线程都能得到有效执行，CPU 采取的策略是为每个线程分配时间片并轮转的形式。当一个线程的时间片用完的时候就会重新处于就绪状态让给其他线程使用，这个过程就属于一次上下文切换。概括来说就是：当前任务在执行完 CPU 时间片切换到另一个任务之前会先保存自己的状态，以便下次再切换回这个任务时，可以再加载这个任务的状态。**任务从保存到再加载的过程就是一次上下文切换**。
> {: id="20210330211656-l05cczj"}
>
> 上下文切换通常是计算密集型的。也就是说，它需要相当可观的处理器时间，在每秒几十上百次的切换中，每次切换都需要纳秒量级的时间。所以，上下文切换对系统来说意味着消耗大量的 CPU 时间，事实上，可能是操作系统中时间消耗最大的操作。
> {: id="20210330211656-03vmygu"}
>
> Linux 相比与其他操作系统（包括其他类 Unix 系统）有很多的优点，其中有一项就是，其上下文切换和模式切换的时间消耗非常少。
> {: id="20210330211656-i7qz7v7"}
{: id="20210330211656-irftbcy"}

**类比于实现世界中的人类通过合作做某件事情，我们可以肯定的一点是线程池大小设置过大或者过小都会有问题，合适的才是最好。**
{: id="20210330211656-jbahgyg"}

**如果我们设置的线程池数量太小的话，如果同一时间有大量任务/请求需要处理，可能会导致大量的请求/任务在任务队列中排队等待执行，甚至会出现任务队列满了之后任务/请求无法处理的情况，或者大量任务堆积在任务队列导致 OOM。这样很明显是有问题的！ CPU 根本没有得到充分利用。**
{: id="20210330211656-sap34kh"}

**但是，如果我们设置线程数量太大，大量线程可能会同时在争取 CPU 资源，这样会导致大量的上下文切换，从而增加线程的执行时间，影响了整体执行效率。**
{: id="20210330211656-0mgvlow"}

有一个简单并且适用面比较广的公式：
{: id="20210330211656-e1pim80"}

- {: id="20210330211656-aer87q9"}**CPU 密集型任务(N+1)：** 这种任务消耗的主要是 CPU 资源，可以将线程数设置为 N（CPU 核心数）+1，比 CPU 核心数多出来的一个线程是为了防止线程偶发的缺页中断，或者其它原因导致的任务暂停而带来的影响。一旦任务暂停，CPU 就会处于空闲状态，而在这种情况下多出来的一个线程就可以充分利用 CPU 的空闲时间。
  {: id="20210330211656-g9sq66v"}
- {: id="20210330211656-fxn9j76"}**I/O 密集型任务(2N)：** 这种任务应用起来，系统会用大部分的时间来处理 I/O 交互，而线程在处理 I/O 的时间段内不会占用 CPU 来处理，这时就可以将 CPU 交出给其它线程使用。因此在 I/O 密集型任务的应用中，我们可以多配置一些线程，具体的计算方法是 2N。
  {: id="20210330211656-4rup62n"}
{: id="20210330211656-c0kgrs8"}

**如何判断是 CPU 密集任务还是 IO 密集任务？**
{: id="20210330211656-j1ncq8h"}

CPU 密集型简单理解就是利用 CPU 计算能力的任务比如你在内存中对大量数据进行排序。单凡涉及到网络读取，文件读取这类都是 IO 密集型，这类任务的特点是 CPU 计算耗费时间相比于等待 IO 操作完成的时间来说很少，大部分时间都花在了等待 IO 操作完成上。
{: id="20210330211656-7p2eun8"}

## 八 参考
{: id="20210330211656-bwbx83v"}

- {: id="20210330211656-zb8l2ov"}《Java 并发编程的艺术》
  {: id="20210330211656-xvfyhul"}
- {: id="20210330211656-jsufpvm"}[Java Scheduler ScheduledExecutorService ScheduledThreadPoolExecutor Example](https://www.journaldev.com/2340/java-scheduler-scheduledexecutorservice-scheduledthreadpoolexecutor-example "Java Scheduler ScheduledExecutorService ScheduledThreadPoolExecutor Example")
  {: id="20210330211656-kjlvw4j"}
- {: id="20210330211656-xhf9d7q"}[java.util.concurrent.ScheduledThreadPoolExecutor Example](https://examples.javacodegeeks.com/core-java/util/concurrent/scheduledthreadpoolexecutor/java-util-concurrent-scheduledthreadpoolexecutor-example/ "java.util.concurrent.ScheduledThreadPoolExecutor Example")
  {: id="20210330211656-q0vp5ki"}
- {: id="20210330211656-ztvmaca"}[ThreadPoolExecutor – Java Thread Pool Example](https://www.journaldev.com/1069/threadpoolexecutor-java-thread-pool-example-executorservice "ThreadPoolExecutor – Java Thread Pool Example")
  {: id="20210330211656-whxrua7"}
{: id="20210330211656-z5ozbvm"}

## 九 其他推荐阅读
{: id="20210330211656-uwn8710"}

- {: id="20210330211656-ra25djz"}[Java 并发（三）线程池原理](https://www.cnblogs.com/warehouse/p/10720781.html "Java并发（三）线程池原理")
  {: id="20210330211656-s6zb81p"}
- {: id="20210330211656-fu4yko5"}[如何优雅的使用和理解线程池](https://github.com/crossoverJie/JCSprout/blob/master/MD/ThreadPoolExecutor.md "如何优雅的使用和理解线程池")
  {: id="20210330211656-z0lz80x"}
{: id="20210330211656-w4xawr2"}


{: id="20210330211656-8ejmfql" type="doc"}
