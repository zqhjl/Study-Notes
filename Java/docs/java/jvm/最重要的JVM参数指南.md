> 本文由 JavaGuide 翻译自 https://www.baeldung.com/jvm-parameters，并对文章进行了大量的完善补充。翻译不易，如需转载请注明出处为：   作者： 。
> {: id="20210330211655-pjd8hi6"}
{: id="20210330211655-uubz5tu"}

## 1.概述
{: id="20210330211655-bup7s56"}

在本篇文章中，你将掌握最常用的 JVM 参数配置。如果对于下面提到了一些概念比如堆、
{: id="20210330211655-3uciuqo"}

## 2.堆内存相关
{: id="20210330211655-w9u2d3j"}

> Java 虚拟机所管理的内存中最大的一块，Java 堆是所有线程共享的一块内存区域，在虚拟机启动时创建。**此内存区域的唯一目的就是存放对象实例，几乎所有的对象实例以及数组都在这里分配内存。**
> {: id="20210330211655-5cwzml0"}
{: id="20210330211655-xdavx7q"}

### 2.1.显式指定堆内存`–Xms`和`-Xmx`
{: id="20210330211655-tdsdjni"}

与性能有关的最常见实践之一是根据应用程序要求初始化堆内存。如果我们需要指定最小和最大堆大小（推荐显示指定大小），以下参数可以帮助你实现：
{: id="20210330211655-xkcrt6t"}

```
-Xms<heap size>[unit] 
-Xmx<heap size>[unit]
```
{: id="20210330211655-cgz4fue"}

- {: id="20210330211655-6003m68"}**heap size** 表示要初始化内存的具体大小。
  {: id="20210330211655-2e2s9wv"}
- {: id="20210330211655-hs02r6r"}**unit** 表示要初始化内存的单位。单位为***“ g”*** (GB) 、***“ m”***（MB）、***“ k”***（KB）。
  {: id="20210330211655-8pi45s6"}
{: id="20210330211655-yg8jhqb"}

举个栗子🌰，如果我们要为JVM分配最小2 GB和最大5 GB的堆内存大小，我们的参数应该这样来写：
{: id="20210330211655-ahi1ytq"}

```
-Xms2G -Xmx5G
```
{: id="20210330211655-rnr3euk"}

### 2.2.显式新生代内存(Young Ceneration)
{: id="20210330211655-mhnrfkp"}

根据[Oracle官方文档](https://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/sizing.html)，在堆总可用内存配置完成之后，第二大影响因素是为 `Young Generation` 在堆内存所占的比例。默认情况下，YG 的最小大小为 1310 *MB*，最大大小为*无限制*。
{: id="20210330211655-c62ansd"}

一共有两种指定 新生代内存(Young Ceneration)大小的方法：
{: id="20210330211655-tbzaivp"}

**1.通过`-XX:NewSize`和`-XX:MaxNewSize`指定**
{: id="20210330211655-dagl3af"}

```
-XX:NewSize=<young size>[unit] 
-XX:MaxNewSize=<young size>[unit]
```
{: id="20210330211655-27cu5fw"}

举个栗子🌰，如果我们要为 新生代分配 最小256m 的内存，最大 1024m的内存我们的参数应该这样来写：
{: id="20210330211655-gyhgeio"}

```
-XX:NewSize=256m
-XX:MaxNewSize=1024m
```
{: id="20210330211655-mj5ms3b"}

**2.通过`-Xmn<young size>[unit] `指定**
{: id="20210330211655-t49qbb2"}

举个栗子🌰，如果我们要为 新生代分配256m的内存（NewSize与MaxNewSize设为一致），我们的参数应该这样来写：
{: id="20210330211655-hm3rndc"}

```
-Xmn256m 
```
{: id="20210330211655-1pjyxtk"}

GC 调优策略中很重要的一条经验总结是这样说的：
{: id="20210330211655-6bhbmhh"}

> 将新对象预留在新生代，由于 Full GC 的成本远高于 Minor GC，因此尽可能将对象分配在新生代是明智的做法，实际项目中根据 GC 日志分析新生代空间大小分配是否合理，适当通过“-Xmn”命令调节新生代大小，最大限度降低新对象直接进入老年代的情况。
> {: id="20210330211655-c8ckuc9"}
{: id="20210330211655-hwaicm3"}

另外，你还可以通过**`-XX:NewRatio=<int>`**来设置新生代和老年代内存的比值。
{: id="20210330211655-mry9el0"}

比如下面的参数就是设置新生代（包括Eden和两个Survivor区）与老年代的比值为1。也就是说：新生代与老年代所占比值为1：1，新生代占整个堆栈的 1/2。
{: id="20210330211655-qjcpflp"}

```
-XX:NewRatio=1
```
{: id="20210330211655-5h3uew5"}

### 2.3.显式指定永久代/元空间的大小
{: id="20210330211655-g2v4pqy"}

**从Java 8开始，如果我们没有指定 Metaspace 的大小，随着更多类的创建，虚拟机会耗尽所有可用的系统内存（永久代并不会出现这种情况）。**
{: id="20210330211655-zax59xj"}

JDK 1.8 之前永久代还没被彻底移除的时候通常通过下面这些参数来调节方法区大小
{: id="20210330211655-4ypab9k"}

```java
-XX:PermSize=N //方法区 (永久代) 初始大小
-XX:MaxPermSize=N //方法区 (永久代) 最大大小,超过这个值将会抛出 OutOfMemoryError 异常:java.lang.OutOfMemoryError: PermGen
```
{: id="20210330211655-p4pb3i8"}

相对而言，垃圾收集行为在这个区域是比较少出现的，但并非数据进入方法区后就“永久存在”了。
{: id="20210330211655-ha0w1hi"}

**JDK 1.8 的时候，方法区（HotSpot 的永久代）被彻底移除了（JDK1.7 就已经开始了），取而代之是元空间，元空间使用的是本地内存。**
{: id="20210330211655-sdewool"}

下面是一些常用参数：
{: id="20210330211655-ed0wdvi"}

```java
-XX:MetaspaceSize=N //设置 Metaspace 的初始（和最小大小）
-XX:MaxMetaspaceSize=N //设置 Metaspace 的最大大小，如果不指定大小的话，随着更多类的创建，虚拟机会耗尽所有可用的系统内存。
```
{: id="20210330211655-0xtl95n"}

## 3.垃圾收集相关
{: id="20210330211655-dr8g17u"}

### 3.1.垃圾回收器
{: id="20210330211655-sd01ibq"}

为了提高应用程序的稳定性，选择正确的[垃圾收集](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html)算法至关重要。
{: id="20210330211655-mieaf0l"}

JVM具有四种类型的*GC*实现：
{: id="20210330211655-nag6cvu"}

- {: id="20210330211655-zr6cnrz"}串行垃圾收集器
  {: id="20210330211655-5ljmbo7"}
- {: id="20210330211655-m0nzo43"}并行垃圾收集器
  {: id="20210330211655-n6odou8"}
- {: id="20210330211655-6fytidt"}CMS垃圾收集器
  {: id="20210330211655-wbc8olj"}
- {: id="20210330211655-gvm7ky5"}G1垃圾收集器
  {: id="20210330211655-gj8dkt6"}
{: id="20210330211655-qjn7k10"}

可以使用以下参数声明这些实现：
{: id="20210330211655-hxhbb8p"}

```
-XX:+UseSerialGC
-XX:+UseParallelGC
-XX:+USeParNewGC
-XX:+UseG1GC
```
{: id="20210330211655-jdluji2"}

有关*垃圾回收*实施的更多详细信息，请参见[此处](https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/jvm/JVM%E5%9E%83%E5%9C%BE%E5%9B%9E%E6%94%B6.md)。
{: id="20210330211655-s20vlxx"}

### 3.2.GC记录
{: id="20210330211655-gwpdg60"}

为了严格监控应用程序的运行状况，我们应该始终检查JVM的*垃圾回收*性能。最简单的方法是以人类可读的格式记录*GC*活动。
{: id="20210330211655-kayya11"}

使用以下参数，我们可以记录*GC*活动：
{: id="20210330211655-yr95drs"}

```
-XX:+UseGCLogFileRotation 
-XX:NumberOfGCLogFiles=< number of log files > 
-XX:GCLogFileSize=< file size >[ unit ]
-Xloggc:/path/to/gc.log
```
{: id="20210330211655-roy381k"}

## 推荐阅读
{: id="20210330211655-58313lb"}

- {: id="20210330211655-zpmd0z8"}[CMS GC 默认新生代是多大？](https://www.jianshu.com/p/832fc4d4cb53)
  {: id="20210330211655-jmjz6fo"}
- {: id="20210330211655-490si9m"}[CMS GC启动参数优化配置](https://www.cnblogs.com/hongdada/p/10277782.html)
  {: id="20210330211655-9tu7m9z"}
- {: id="20210330211655-r95opm9"}[从实际案例聊聊Java应用的GC优化-美团技术团队](https://tech.meituan.com/2017/12/29/jvm-optimize.html)
  {: id="20210330211655-grv0z9h"}
- {: id="20210330211655-cjtejc5"}[JVM性能调优详解](https://www.choupangxia.com/2019/11/11/interview-jvm-gc-08/) （2019-11-11）
  {: id="20210330211655-fwap7o4"}
- {: id="20210330211655-epqxq6a"}[JVM参数使用手册](https://segmentfault.com/a/1190000010603813)
  {: id="20210330211655-ov00yfp"}
{: id="20210330211655-1j6s991"}


{: id="20210330211655-3araxzs" type="doc"}
