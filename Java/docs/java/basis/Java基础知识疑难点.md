<!-- TOC -->

- {: id="20210330211654-ktrrstu"}[1. 基础](#1-基础)
  {: id="20210330211654-4j8hfs4"}
  - {: id="20210330211654-6t201jl"}[1.1. 正确使用 equals 方法](#11-正确使用-equals-方法)
    {: id="20210330211654-iug1353"}
  - {: id="20210330211654-3ku9zqh"}[1.2. 整型包装类值的比较](#12-整型包装类值的比较)
    {: id="20210330211654-xz8aywe"}
  - {: id="20210330211654-d4e0c1v"}[1.3. BigDecimal](#13-bigdecimal)
    {: id="20210330211654-mamkkih"}
    - {: id="20210330211654-hx0zu8h"}[1.3.1. BigDecimal 的用处](#131-bigdecimal-的用处)
      {: id="20210330211654-7jn3yt2"}
    - {: id="20210330211654-posern4"}[1.3.2. BigDecimal 的大小比较](#132-bigdecimal-的大小比较)
      {: id="20210330211654-oggz8ks"}
    - {: id="20210330211654-hhl6h16"}[1.3.3. BigDecimal 保留几位小数](#133-bigdecimal-保留几位小数)
      {: id="20210330211654-6mbvy06"}
    - {: id="20210330211654-jw3ui3k"}[1.3.4. BigDecimal 的使用注意事项](#134-bigdecimal-的使用注意事项)
      {: id="20210330211654-dou1ev5"}
    - {: id="20210330211654-9z33335"}[1.3.5. 总结](#135-总结)
      {: id="20210330211654-gowgtbt"}
    {: id="20210330211654-2b3ipx3"}
  - {: id="20210330211654-j2jgayn"}[1.4. 基本数据类型与包装数据类型的使用标准](#14-基本数据类型与包装数据类型的使用标准)
    {: id="20210330211654-odbxnph"}
  {: id="20210330211654-edh9n95"}
- {: id="20210330211654-essyzvk"}[2. 集合](#_2-集合)
  {: id="20210330211654-42w6yt4"}
  - {: id="20210330211654-7uujjqp"}[2.1. Arrays.asList()使用指南](#21-arraysaslist使用指南)
    {: id="20210330211654-geokjq4"}
    - {: id="20210330211654-00kv4gm"}[2.1.1. 简介](#211-简介)
      {: id="20210330211654-i495ezj"}
    - {: id="20210330211654-j20qszi"}[2.1.2. 《阿里巴巴Java 开发手册》对其的描述](#212-阿里巴巴java-开发手册对其的描述)
      {: id="20210330211654-k2fqejm"}
    - {: id="20210330211654-wtltc2t"}[2.1.3. 使用时的注意事项总结](#213-使用时的注意事项总结)
      {: id="20210330211654-xchma75"}
    - {: id="20210330211654-w4vchdi"}[2.1.4. 如何正确的将数组转换为ArrayList?](#214-如何正确的将数组转换为arraylist)
      {: id="20210330211654-esdkdan"}
    {: id="20210330211654-fhqb1s1"}
  - {: id="20210330211654-n3kbyyu"}[2.2. Collection.toArray()方法使用的坑&如何反转数组](#22-collectiontoarray方法使用的坑如何反转数组)
    {: id="20210330211654-sp6por7"}
  - {: id="20210330211654-ra92uvi"}[2.3. 不要在 foreach 循环里进行元素的 remove/add 操作](#23-不要在-foreach-循环里进行元素的-removeadd-操作)
    {: id="20210330211654-3s55hey"}
  {: id="20210330211654-adii9ne"}
{: id="20210330211654-7fljv6q"}

<!-- /TOC -->

# 1. 基础
{: id="20210330211654-y1jcdg7"}

## 1.1. 正确使用 equals 方法
{: id="20210330211654-keakzd4"}

Object的equals方法容易抛空指针异常，应使用常量或确定有值的对象来调用 equals。
{: id="20210330211654-jdhhpra"}

举个例子：
{: id="20210330211654-0pvslck"}

```java
// 不能使用一个值为null的引用类型变量来调用非静态方法，否则会抛出异常
String str = null;
if (str.equals("SnailClimb")) {
  ...
} else {
  ..
}
```
{: id="20210330211654-e9h21kl"}

运行上面的程序会抛出空指针异常，但是我们把第二行的条件判断语句改为下面这样的话，就不会抛出空指针异常，else 语句块得到执行。：
{: id="20210330211654-872yn2o"}

```java
"SnailClimb".equals(str);// false 
```
{: id="20210330211654-908yhpp"}

不过更推荐使用 `java.util.Objects#equals`(JDK7 引入的工具类)。
{: id="20210330211654-5k0bdik"}

```java
Objects.equals(null,"SnailClimb");// false
```
{: id="20210330211654-65xpsbh"}

我们看一下`java.util.Objects#equals`的源码就知道原因了。
{: id="20210330211654-geby60o"}

```java
public static boolean equals(Object a, Object b) {
    // 可以避免空指针异常。如果a==null的话此时a.equals(b)就不会得到执行，避免出现空指针异常。
    return (a == b) || (a != null && a.equals(b));
}
```
{: id="20210330211654-25ciusv"}

**注意：**
{: id="20210330211654-1p6v2c1"}

Reference:[Java中equals方法造成空指针异常的原因及解决方案](https://blog.csdn.net/tick_tock97/article/details/72824894)
{: id="20210330211654-wfnhfq0"}

- {: id="20210330211654-rhbny1i"}每种原始类型都有默认值一样，如int默认值为 0，boolean 的默认值为 false，null 是任何引用类型的默认值，不严格的说是所有 Object 类型的默认值。
  {: id="20210330211654-t677n5h"}
- {: id="20210330211654-6nvjfcx"}可以使用 == 或者 != 操作来比较null值，但是不能使用其他算法或者逻辑操作。在Java中`null == null`将返回true。
  {: id="20210330211654-ixkiv95"}
- {: id="20210330211654-ilc4i0g"}不能使用一个值为null的引用类型变量来调用非静态方法，否则会抛出异常
  {: id="20210330211654-8uxzoka"}
{: id="20210330211654-xtzeqim"}

## 1.2. 整型包装类值的比较
{: id="20210330211654-czgefvd"}

所有整型包装类对象值的比较必须使用equals方法。
{: id="20210330211654-c9jzbcp"}

先看下面这个例子：
{: id="20210330211654-e7k31g5"}

```java
Integer x = 3;
Integer y = 3;
System.out.println(x == y);// true
Integer a = new Integer(3);
Integer b = new Integer(3);
System.out.println(a == b);//false
System.out.println(a.equals(b));//true
```
{: id="20210330211654-70801cu"}

当使用自动装箱方式创建一个Integer对象时，当数值在-128 ~127时，会将创建的 Integer 对象缓存起来，当下次再出现该数值时，直接从缓存中取出对应的Integer对象。所以上述代码中，x和y引用的是相同的Integer对象。
{: id="20210330211654-9tw6bub"}

**注意：** 如果你的IDE(IDEA/Eclipse)上安装了阿里巴巴的p3c插件，这个插件如果检测到你用 ==的话会报错提示，推荐安装一个这个插件，很不错。
{: id="20210330211654-9c3k224"}

## 1.3. BigDecimal
{: id="20210330211654-qr9vmpl"}

### 1.3.1. BigDecimal 的用处
{: id="20210330211654-bec0rxn"}

《阿里巴巴Java开发手册》中提到：**浮点数之间的等值判断，基本数据类型不能用==来比较，包装数据类型不能用 equals 来判断。** 具体原理和浮点数的编码方式有关，这里就不多提了，我们下面直接上实例：
{: id="20210330211654-ttchlmp"}

```java
float a = 1.0f - 0.9f;
float b = 0.9f - 0.8f;
System.out.println(a);// 0.100000024
System.out.println(b);// 0.099999964
System.out.println(a == b);// false
```
{: id="20210330211654-y22g12q"}

具有基本数学知识的我们很清楚的知道输出并不是我们想要的结果（**精度丢失**），我们如何解决这个问题呢？一种很常用的方法是：**使用使用 BigDecimal 来定义浮点数的值，再进行浮点数的运算操作。**
{: id="20210330211654-dem1wgn"}

```java
BigDecimal a = new BigDecimal("1.0");
BigDecimal b = new BigDecimal("0.9");
BigDecimal c = new BigDecimal("0.8");

BigDecimal x = a.subtract(b); 
BigDecimal y = b.subtract(c); 

System.out.println(x); /* 0.1 */
System.out.println(y); /* 0.1 */
System.out.println(Objects.equals(x, y)); /* true */
```
{: id="20210330211654-1ckv2vp"}

### 1.3.2. BigDecimal 的大小比较
{: id="20210330211654-7th1sv2"}

`a.compareTo(b)` : 返回 -1 表示 `a` 小于 `b`，0 表示 `a` 等于 `b` ， 1表示 `a` 大于 `b`。
{: id="20210330211654-sdoqg4d"}

```java
BigDecimal a = new BigDecimal("1.0");
BigDecimal b = new BigDecimal("0.9");
System.out.println(a.compareTo(b));// 1
```
{: id="20210330211654-b85w5f2"}

### 1.3.3. BigDecimal 保留几位小数
{: id="20210330211654-s7ipw9a"}

通过 `setScale`方法设置保留几位小数以及保留规则。保留规则有挺多种，不需要记，IDEA会提示。
{: id="20210330211654-nxkuaz8"}

```java
BigDecimal m = new BigDecimal("1.255433");
BigDecimal n = m.setScale(3,BigDecimal.ROUND_HALF_DOWN);
System.out.println(n);// 1.255
```
{: id="20210330211654-98vtgyb"}

### 1.3.4. BigDecimal 的使用注意事项
{: id="20210330211654-71pf7x2"}

注意：我们在使用BigDecimal时，为了防止精度丢失，推荐使用它的 **BigDecimal(String)** 构造方法来创建对象。《阿里巴巴Java开发手册》对这部分内容也有提到如下图所示。
{: id="20210330211654-5fuhr4x"}

![《阿里巴巴Java开发手册》对这部分BigDecimal的描述](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019/7/BigDecimal.png)
{: id="20210330211654-d54uv1o"}

### 1.3.5. 总结
{: id="20210330211654-lkb2511"}

BigDecimal 主要用来操作（大）浮点数，BigInteger 主要用来操作大整数（超过 long 类型）。
{: id="20210330211654-o74akc1"}

BigDecimal 的实现利用到了 BigInteger, 所不同的是 BigDecimal 加入了小数位的概念
{: id="20210330211654-jy8yakc"}

## 1.4. 基本数据类型与包装数据类型的使用标准
{: id="20210330211654-vqo9l0c"}

Reference:《阿里巴巴Java开发手册》
{: id="20210330211654-99k1wcp"}

- {: id="20210330211654-lr6q8ok"}【强制】所有的 POJO 类属性必须使用包装数据类型。
  {: id="20210330211654-gxunfcz"}
- {: id="20210330211654-u1qicda"}【强制】RPC 方法的返回值和参数必须使用包装数据类型。
  {: id="20210330211654-t0dvp8k"}
- {: id="20210330211654-4vg4d17"}【推荐】所有的局部变量使用基本数据类型。
  {: id="20210330211654-9qijfrt"}
{: id="20210330211654-72rbdx5"}

比如我们如果自定义了一个Student类,其中有一个属性是成绩score,如果用Integer而不用int定义,一次考试,学生可能没考,值是null,也可能考了,但考了0分,值是0,这两个表达的状态明显不一样.
{: id="20210330211654-gcyt5in"}

**说明** :POJO 类属性没有初值是提醒使用者在需要使用时，必须自己显式地进行赋值，任何 NPE 问题，或者入库检查，都由使用者来保证。
{: id="20210330211654-rgl5jqw"}

**正例** : 数据库的查询结果可能是 null，因为自动拆箱，用基本数据类型接收有 NPE 风险。
{: id="20210330211654-9lbo3uu"}

**反例** : 比如显示成交总额涨跌情况，即正负 x%，x 为基本数据类型，调用的 RPC 服务，调用不成功时，返回的是默认值，页面显示为 0%，这是不合理的，应该显示成中划线。所以包装数据类型的 null 值，能够表示额外的信息，如:远程调用失败，异常退出。
{: id="20210330211654-c8on2ew"}

# 2. 集合
{: id="20210330211654-hybk331"}

## 2.1. Arrays.asList()使用指南
{: id="20210330211654-y3ovmbw"}

最近使用`Arrays.asList()`遇到了一些坑，然后在网上看到这篇文章：[Java Array to List Examples](http://javadevnotes.com/java-array-to-list-examples) 感觉挺不错的，但是还不是特别全面。所以，自己对于这块小知识点进行了简单的总结。
{: id="20210330211654-jovc8mx"}

### 2.1.1. 简介
{: id="20210330211654-yqlkjj4"}

`Arrays.asList()`在平时开发中还是比较常见的，我们可以使用它将一个数组转换为一个List集合。
{: id="20210330211654-6rgi859"}

```java
String[] myArray = {"Apple", "Banana", "Orange"};
List<String> myList = Arrays.asList(myArray);
//上面两个语句等价于下面一条语句
List<String> myList = Arrays.asList("Apple","Banana", "Orange");
```
{: id="20210330211654-bolz5ck"}

JDK 源码对于这个方法的说明：
{: id="20210330211654-em87j8i"}

```java
/**
  *返回由指定数组支持的固定大小的列表。此方法作为基于数组和基于集合的API之间的桥梁，
  * 与 Collection.toArray()结合使用。返回的List是可序列化并实现RandomAccess接口。
  */
public static <T> List<T> asList(T... a) {
    return new ArrayList<>(a);
}
```
{: id="20210330211654-0hp6pox"}

### 2.1.2. 《阿里巴巴Java 开发手册》对其的描述
{: id="20210330211654-qbx6o3s"}

`Arrays.asList()`将数组转换为集合后,底层其实还是数组，《阿里巴巴Java 开发手册》对于这个方法有如下描述：
{: id="20210330211654-lau12fj"}

![阿里巴巴Java开发手-Arrays.asList()方法](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-6/阿里巴巴Java开发手-Arrays.asList()方法.png)
{: id="20210330211654-plm33dq"}

### 2.1.3. 使用时的注意事项总结
{: id="20210330211654-x2c20os"}

**传递的数组必须是对象数组，而不是基本类型。**
{: id="20210330211654-51v7bu8"}

`Arrays.asList()`是泛型方法，传入的对象必须是对象数组。
{: id="20210330211654-liyu2xy"}

```java
int[] myArray = {1, 2, 3};
List myList = Arrays.asList(myArray);
System.out.println(myList.size());//1
System.out.println(myList.get(0));//数组地址值
System.out.println(myList.get(1));//报错：ArrayIndexOutOfBoundsException
int[] array = (int[]) myList.get(0);
System.out.println(array[0]);//1
```
{: id="20210330211654-x97zwmt"}

当传入一个原生数据类型数组时，`Arrays.asList()` 的真正得到的参数就不是数组中的元素，而是数组对象本身！此时List 的唯一元素就是这个数组，这也就解释了上面的代码。
{: id="20210330211654-ktg08o7"}

我们使用包装类型数组就可以解决这个问题。
{: id="20210330211654-n3e6bjv"}

```java
Integer[] myArray = {1, 2, 3};
```
{: id="20210330211654-mu53dni"}

**使用集合的修改方法:`add()`、`remove()`、`clear()`会抛出异常。**
{: id="20210330211654-43yy3we"}

```java
List myList = Arrays.asList(1, 2, 3);
myList.add(4);//运行时报错：UnsupportedOperationException
myList.remove(1);//运行时报错：UnsupportedOperationException
myList.clear();//运行时报错：UnsupportedOperationException
```
{: id="20210330211654-lw0zysc"}

`Arrays.asList()` 方法返回的并不是 `java.util.ArrayList` ，而是 `java.util.Arrays` 的一个内部类,这个内部类并没有实现集合的修改方法或者说并没有重写这些方法。
{: id="20210330211654-6g7o54x"}

```java
List myList = Arrays.asList(1, 2, 3);
System.out.println(myList.getClass());//class java.util.Arrays$ArrayList
```
{: id="20210330211654-anzl8w0"}

下图是`java.util.Arrays$ArrayList`的简易源码，我们可以看到这个类重写的方法有哪些。
{: id="20210330211654-bt00th5"}

```java
  private static class ArrayList<E> extends AbstractList<E>
        implements RandomAccess, java.io.Serializable
    {
        ...

        @Override
        public E get(int index) {
          ...
        }

        @Override
        public E set(int index, E element) {
          ...
        }

        @Override
        public int indexOf(Object o) {
          ...
        }

        @Override
        public boolean contains(Object o) {
           ...
        }

        @Override
        public void forEach(Consumer<? super E> action) {
          ...
        }

        @Override
        public void replaceAll(UnaryOperator<E> operator) {
          ...
        }

        @Override
        public void sort(Comparator<? super E> c) {
          ...
        }
    }
```
{: id="20210330211654-78ugjkg"}

我们再看一下`java.util.AbstractList`的`remove()`方法，这样我们就明白为啥会抛出`UnsupportedOperationException`。
{: id="20210330211654-r2ezryh"}

```java
public E remove(int index) {
    throw new UnsupportedOperationException();
}
```
{: id="20210330211654-fth9icx"}

### 2.1.4. 如何正确的将数组转换为ArrayList?
{: id="20210330211654-8gzmg2l"}

stackoverflow：https://dwz.cn/vcBkTiTW
{: id="20210330211654-xgj3oi6"}

**1. 自己动手实现（教育目的）**
{: id="20210330211654-x9he4qz"}

```java
//JDK1.5+
static <T> List<T> arrayToList(final T[] array) {
  final List<T> l = new ArrayList<T>(array.length);

  for (final T s : array) {
    l.add(s);
  }
  return l;
}
```
{: id="20210330211654-crw7spn"}

```java
Integer [] myArray = { 1, 2, 3 };
System.out.println(arrayToList(myArray).getClass());//class java.util.ArrayList
```
{: id="20210330211654-8koqmmy"}

**2. 最简便的方法(推荐)**
{: id="20210330211654-sicl6l7"}

```java
List list = new ArrayList<>(Arrays.asList("a", "b", "c"))
```
{: id="20210330211654-4aulbgx"}

**3. 使用 Java8 的Stream(推荐)**
{: id="20210330211654-cagw37z"}

```java
Integer [] myArray = { 1, 2, 3 };
List myList = Arrays.stream(myArray).collect(Collectors.toList());
//基本类型也可以实现转换（依赖boxed的装箱操作）
int [] myArray2 = { 1, 2, 3 };
List myList = Arrays.stream(myArray2).boxed().collect(Collectors.toList());
```
{: id="20210330211654-m5d1c0r"}

**4. 使用 Guava(推荐)**
{: id="20210330211654-s8mxamf"}

对于不可变集合，你可以使用[`ImmutableList`](https://github.com/google/guava/blob/master/guava/src/com/google/common/collect/ImmutableList.java)类及其[`of()`](https://github.com/google/guava/blob/master/guava/src/com/google/common/collect/ImmutableList.java#L101)与[`copyOf()`](https://github.com/google/guava/blob/master/guava/src/com/google/common/collect/ImmutableList.java#L225)工厂方法：（参数不能为空）
{: id="20210330211654-0ypcg01"}

```java
List<String> il = ImmutableList.of("string", "elements");  // from varargs
List<String> il = ImmutableList.copyOf(aStringArray);      // from array
```
{: id="20210330211654-9b07e4e"}

对于可变集合，你可以使用[`Lists`](https://github.com/google/guava/blob/master/guava/src/com/google/common/collect/Lists.java)类及其[`newArrayList()`](https://github.com/google/guava/blob/master/guava/src/com/google/common/collect/Lists.java#L87)工厂方法：
{: id="20210330211654-jg342lb"}

```java
List<String> l1 = Lists.newArrayList(anotherListOrCollection);    // from collection
List<String> l2 = Lists.newArrayList(aStringArray);               // from array
List<String> l3 = Lists.newArrayList("or", "string", "elements"); // from varargs
```
{: id="20210330211654-3wn3do1"}

**5. 使用 Apache Commons Collections**
{: id="20210330211654-lvw6yqt"}

```java
List<String> list = new ArrayList<String>();
CollectionUtils.addAll(list, str);
```
{: id="20210330211654-bcplm1o"}

**6. 使用 Java9 的 `List.of()`方法**
{: id="20210330211654-cusgzfe"}

```java
Integer[] array = {1, 2, 3};
List<Integer> list = List.of(array);
System.out.println(list); /* [1, 2, 3] */
/* 不支持基本数据类型 */
```
{: id="20210330211654-ctzqz15"}

## 2.2. Collection.toArray()方法使用的坑&如何反转数组
{: id="20210330211654-ej4gcz5"}

该方法是一个泛型方法：`<T> T[] toArray(T[] a);` 如果`toArray`方法中没有传递任何参数的话返回的是`Object`类型数组。
{: id="20210330211654-wbkyegd"}

```java
String [] s= new String[]{
    "dog", "lazy", "a", "over", "jumps", "fox", "brown", "quick", "A"
};
List<String> list = Arrays.asList(s);
Collections.reverse(list);
s=list.toArray(new String[0]);//没有指定类型的话会报错
```
{: id="20210330211654-i6qoqfc"}

由于JVM优化，`new String[0]`作为`Collection.toArray()`方法的参数现在使用更好，`new String[0]`就是起一个模板的作用，指定了返回数组的类型，0是为了节省空间，因为它只是为了说明返回的类型。详见：[https://shipilev.net/blog/2016/arrays-wisdom-ancients/](https://shipilev.net/blog/2016/arrays-wisdom-ancients/)
{: id="20210330211654-mw5pfqx"}

## 2.3. 不要在 foreach 循环里进行元素的 remove/add 操作
{: id="20210330211654-zhgx8j3"}

如果要进行`remove`操作，可以调用迭代器的 `remove `方法而不是集合类的 remove 方法。因为如果列表在任何时间从结构上修改创建迭代器之后，以任何方式除非通过迭代器自身`remove/add`方法，迭代器都将抛出一个`ConcurrentModificationException`,这就是单线程状态下产生的 **fail-fast 机制**。
{: id="20210330211654-u53sgx3"}

> **fail-fast 机制** ：多个线程对 fail-fast 集合进行修改的时，可能会抛出ConcurrentModificationException，单线程下也会出现这种情况，上面已经提到过。
> {: id="20210330211654-gag7m9s"}
{: id="20210330211654-ugqx7dg"}

Java8开始，可以使用`Collection#removeIf()`方法删除满足特定条件的元素,如
{: id="20210330211654-87c4izo"}

```java
List<Integer> list = new ArrayList<>();
for (int i = 1; i <= 10; ++i) {
    list.add(i);
}
list.removeIf(filter -> filter % 2 == 0); /* 删除list中的所有偶数 */
System.out.println(list); /* [1, 3, 5, 7, 9] */
```
{: id="20210330211654-jus1zps"}

`java.util`包下面的所有的集合类都是fail-fast的，而`java.util.concurrent`包下面的所有的类都是fail-safe的。
{: id="20210330211654-azhiotl"}

![不要在 foreach 循环里进行元素的 remove/add 操作](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019/7/foreach-remove:add.png)
{: id="20210330211654-yd6c7x2"}


{: id="20210330211654-91nxshd" type="doc"}
