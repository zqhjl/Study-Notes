### MyBatis
{: id="20210330204518-dy81mqm" updated="20210330225322"}

ORMapping: Object Relationship Mapping 对象关系映射
对象指面向对象
关系指关系型数据库
Java 到 MySQL 的映射，开发者可以以面向对象的思想来管理数据库。
{: id="20210330204518-w695buz"}

#### 如何使用
{: id="20210330204518-ooexvfb" updated="20210330225327"}

- {: id="20210330204518-f290sn8"}新建 Maven 工程,pom.xml
  {: id="20210330204518-med21mp"}
{: id="20210330204518-dud7no7"}

```xml
<dependencies>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.4.5</version>
    </dependency>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.11</version>
    </dependency>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>1.18.6</version>
        <scope>provided</scope>
    </dependency>
</dependencies>
<build>
    <resources>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.xml</include>
            </includes>
        </resource>
    </resources>
</build>
```
{: id="20210330204518-4fjb405"}

- {: id="20210330204518-u72gamh"}新建数据表
  {: id="20210330204518-n7vr8g9"}
{: id="20210330204518-fig2bgr"}

```sql
use mybatis;
create table t_account(
    id int primary key auto_increment,
    username varchar(11),
    password varchar(11),
    age int
)
```
{: id="20210330204518-k81uokm"}

- {: id="20210330204518-4p33876"}新建数据表对应的实体类 Account
  {: id="20210330204518-rrcstwm"}
{: id="20210330204518-b019xfv"}

```java
package com.southwind.entity;
import lombok.Data;
@Data
public class Account {
    private long id;
    private String username;
    private String password; private int age;
}
```
{: id="20210330204518-1rxdt0t"}

- {: id="20210330204518-biyd7b1"}创建 MyBatis 的配置文件 config.xml,文件名可自定义
  {: id="20210330204518-icscsyg"}
{: id="20210330204518-9v7hdmz"}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--配置MyBatis运行环境-->
    <environments default="development">
    <environment id="development">
        <!--配置JDBC事务管理-->
        <transactionManager type="JDBC"></transactionManager>
        <!-- POOLED配置JDB C数据源连接池-->
        <dataSource type="POOLED"〉
                    <property name="driver" value="com.mysql.cj.jdbc.Driver">
        </property>
    <property name="url" value="jdbc:mysql://localhost:3306/mybatis? useUnicode=true&characterEncoding=UTF-8"></property>
    <property name="username" value="root"></property>
    <property name="password" value="root"></property>
    </dataSource>
</environment>
</environments>
</configuration>
```
{: id="20210330204518-skutlsm"}

### 使用原生接口
{: id="20210330204518-t81yqj7"}

1. {: id="20210330204518-ngc6n7e"}MyBatis框架需要开发者自定义SQL语句，写在Mapper.xml文件中，实际开发中，会为每个实体 类创建对应的Mapper.xml，定义管理该对象数据的SQL。
   {: id="20210330204518-p0w2bom"}
{: id="20210330204518-jt514n9"}

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.orgZ/DTD Mapper 3.0//EN"
"http://mybatis.Org/dtd/mybatis-3-:mapper.dtd">
<mapper namespace="com.southwind.mapper.AccoutMapper">
    <insert id="save" parameterType="com.southwind.entity.Account">
        insert into t_account(username,password,age) values(#{username},#
        {password},#{age})
    </insert>
</mapper>
```
{: id="20210330204518-bam3hkb"}

- {: id="20210330204518-wyw1vz4"}namespace通常设置为文件所在包+文件名的形式。
  {: id="20210330204518-k1pzush"}
- {: id="20210330204518-aq2secx"}insert标签表示执行添加操作。
  {: id="20210330204518-yqpu1ze"}
- {: id="20210330204518-f53ar43"}select标签表示执行查询操作。
  {: id="20210330204518-uowtxrr"}
- {: id="20210330204518-8omh2r7"}update标签表示执行更新操作。
  {: id="20210330204518-xeb39ll"}
- {: id="20210330204518-8uioq2h"}delete标签表示执行删除操作。
  {: id="20210330204518-no3aycx"}
- {: id="20210330204518-3mbm7kx"}id是实际调用MyBatis方法时需要用到的参数。
  {: id="20210330204518-v31vfch"}
- {: id="20210330204518-jbane9u"}parameterType是调用对应方法时参数的数据类型。
  {: id="20210330204518-bnbnmvv"}
{: id="20210330204518-jnnv5mq"}

2. {: id="20210330204518-feou7kb"}在全局配置文件config.xml中注册AccountMapper.xml
   {: id="20210330204518-n50l37j"}
{: id="20210330204518-5wdr8fp"}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--配置MyBatis运行环境-->
    <environments default="development">
        <environment id="development">
            <!--配置JDBC事务管理-->
            <transactionManager type="JDBC"></transactionManager>
            <!-- POOLED配置JDB C数据源连接池-->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver">
                </property>
                <property name="url"
                          value="jdbc:mysql://localhost:3306/mybatis?useUnicode=true&characterEncoding=UTF-8"></property>
                <property name="username" value="root"></property>
                <property name="password" value="root"></property>
            </dataSource>
        </environment>
    </environments>
    <!一一 注册 AccountMapper.xml -->
    <mappers>
        <mapper resource=Hcom/southwind/mapper/AccountMapper.xmlH></mapper> </mappers>
</configuration>
```
{: id="20210330204518-splyv1j"}

3. {: id="20210330204518-42sblv2"}调用MyBatis的原生接口执行添加操作。
   {: id="20210330204518-9te5zsw"}
{: id="20210330204518-oif6si9"}

```java
public class Test {
    public static void main(String[] args) {
        //加载MyBatis配置文件
        InputStream inputStream =
            Test.class.getClassLoader().getResourceAsStream("config.xml");
        SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
        SqlSessionFactory sqlSessionFactory =
            sqlSessionFactoryBuilder.build(inputStream);
        SqlSession sqlSession = sqlSessionFactory.openSession();
        String statement = "com.southwind.mapper.AccoutMapper.save";
        Account account = new Account( 1L,"张三"，"123123",22);
        sqlSession.insert(statement,account);
        sqlSession.commit();
    }
}
```
{: id="20210330204518-gt1063w"}

### 通过Mapper代理实现自定义接口
{: id="20210330204518-o0mcagd"}

- {: id="20210330204518-6apzjuw"}自定义接口，定义相关业务方法。
  {: id="20210330204518-mf3712i"}
- {: id="20210330204518-rltqybk"}编写与方法相对应的Mapper.xml。
  {: id="20210330204518-ewf69ak"}
{: id="20210330204518-z015fxe"}

1. {: id="20210330204518-5fpds4s"}自定义接口
   {: id="20210330204518-rx16u6l"}
{: id="20210330204518-orm1loq"}

```java
package com.southwind.repository;
import com.southwind.entity.Account;
import java.util.List;
public interface AccountRepository {
    public int save(Account account);
    public int update(Account account);
    public int deleteById(long id);
    public List<Account> findAll();
    public Account findById(long id);
}
```
{: id="20210330204518-dj9p6fd"}

2. {: id="20210330204518-hi78up2"}创建接口对应的Mapper.xml,定义接口方法对应的SQL语句。
   {: id="20210330204518-zimuw7b"}
{: id="20210330204518-epbl63v"}

statement 标签可根据 SQL 执行的业务选择 insert、delete、update、select。
MyBatis框架会根据规则自动创建接口实现类的代理对象。
规则：
{: id="20210330204518-cam1vkt"}

- {: id="20210330204518-68hpqu4"}Mapper.xml 中 namespace 为接口的全类名。
  {: id="20210330204518-t4ikdzt"}
- {: id="20210330204518-w6xj58z"}Mapper.xml中statement的id为接口中对应的方法名。
  {: id="20210330204518-m1k5ae3"}
- {: id="20210330204518-jvmyaft"}Mapper.xml中statement的parameterType和接口中对应方法的参数类型一致。
  {: id="20210330204518-pbch7r9"}
- {: id="20210330204518-k6f8z9c"}Mapper.xml中statement的resultType和接口中对应方法的返回值类型一致。
  {: id="20210330204518-wbnul2t"}
{: id="20210330204518-f3loe2p"}

```xml
<?xml version=H1.0H encoding=HUTF-8H ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.orgZ/DTD Mapper 3.0//EN"
"http://mybatis.Org/dtd/mybatis-3-:mapper.dtd">
<mapper namespace="com.southwind.repository.AccountRepository">
    <insert id="save" parameterType="com.southwind.entity.Account">
        insert into t_account(username,password,age) values(#{username},#
        {password},#{age})
    </insert>
    <update id="update" parameterType="com.southwind.entity.Account">
        update t_account set username = #{username},password = #{password},age
        = #{age} where id = #{id}
    </update>
    <delete id="deleteById" parameterType="long">
        delete from t_account where id = #{id}
    </delete>
    <select id="findAll" resultType="com.southwind.entity.Account">
        select * from t_account
    </select>
    <select id="findById" parameterType="long"
            resultType="com.southwind.entity.Account">
        select * from t_account where id = #{id}
    </select>
</mapper>
```
{: id="20210330204518-wq2wi6w"}

3. {: id="20210330204518-ryxtc77"}在 config.xml 中注册 AccountRepository.xml
   {: id="20210330204518-henmymz"}
{: id="20210330204518-ylvfb2p"}

```xml
<!一一 注册 AccountMapper.xml -->
<mappers>
    <mapper resource="com/southwind/mapper/AccountMapper.xml"></mapper>
    <mapper resource="com/southwind/repository/AccountRepository.xml"></mapper>
</mappers>
```
{: id="20210330204518-t1evgw9"}

4. {: id="20210330204518-8se28kz"}调用接口的代理对象完成相关的业务操作
   {: id="20210330204518-nxuyq16"}
{: id="20210330204518-lvjuaga"}

```java
package com.southwind.test;
import com.southwind.entity.Account;
import com.southwind.repository.AccountRepository;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import java.io.InputStream;
import java.util.List;
public class Test2 {
    public static void main(String[] args) {
        InputStream inputStream =
            Test.class.getClassLoader().getResourceAsStream("config.xml");
        SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
        SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(inputStream);
        SqlSession sqlSession = sqlSessionFactory.openSession();
        //获取实现接口的代理对象
        AccountRepository accountRepository = sqlSession.getMapper(AccountRepository.class);
        // 添加对象
        // Account account = new Account(3L,"王五","111111",24);
        // int result = accountRepository.save(account);
        // sqlSession.commit();
        // 查询全部对象
        // List<Account> list =	accountRepository.findAll();
        // for (Account account:list){
        // System.out.println(account);
        // }
        // sqlSession.close();
        // 通过id查询对象
        // Account account = accountRepository.findById(3L);
        // System.out.println(account);
        // sqlSession.close();
        // 修改对象
        // Account account = accountRepository.findById(3L);
        // account.setUsername("小明");
        // account.setPassword("OOO");
        // account.setAge(18);
        // int result = accountRepository.update(account);
        // sqlSession.commit();
        // System.out.println(result);
        // sqlSession.close();
        // 通过id删除对象
        int result = accountRepository.deleteById(3L);
        System.out.println(result);
        sqlSession.commit();
        sqlSession.close();
    }
}
```
{: id="20210330204518-stz1swc"}

### Mapper.xml
{: id="20210330204518-3tbjbz6"}

- {: id="20210330204518-i0rsva4"}statement标签：select、update、delete, insert分别对应查询、修改、删除、添加操作。
  {: id="20210330204518-4vtyoo4"}
- {: id="20210330204518-3543i7a"}parameterType:参数数据类型
  {: id="20210330204518-8aw9quw"}

  1. {: id="20210330204518-baavbye"}基本数据类型，通过id查询Account
     {: id="20210330204518-ht5hncz"}
  {: id="20210330204518-z0hl0q6"}
{: id="20210330204518-gvt4k1e"}

```xml
<select id="findById" parameterType="long" resultType="com.southwind.entity.Account">
    select * from t_account where id = #{id}
</select>
```
{: id="20210330204518-u2dxl9i"}

2. {: id="20210330204518-2tsainh"}String 类型，通过 name 查询 Account
   {: id="20210330204518-cz1yytb"}
{: id="20210330204518-d97gs4u"}

```xml
<select id="findByName" parameterType="java.lang.String" resultType="com.southwind.entity.Account">
    select * from t_account where username = #{username}
</select>
```
{: id="20210330204518-qjoejiz"}

3. {: id="20210330204518-pgmiiwm"}包装类，通过id查询Account
   {: id="20210330204518-5o8onm6"}
{: id="20210330204518-ixw0q8r"}

```xml
<select id="findById2" parameterType="java.lang.Long"
        resultType="com.southwind.entity.Account">
    select * from t_account where id = #{id}
</select>
```
{: id="20210330204518-mtccvvi"}

4. {: id="20210330204518-a9zisi2"}多个参数，通过name和age查询Account
   {: id="20210330204518-zzj6k8m"}
{: id="20210330204518-m5bgmxh"}

```xml
<select id="findByNameAndAge" resultType="com.southwind.entity.Account"> select * from t_account where username = #{arg0} and age = #{arg1} </select>
```
{: id="20210330204518-f2spm3t"}

5. {: id="20210330204518-tyhdyxt"}Java Bean
   {: id="20210330204518-184ll0u"}
{: id="20210330204518-p5nxesx"}

```xml
<update id="update" parameterType="com.southwind.entity.Account">
    update t_account set username = #{username},password = #{password},age =#{age} where id = #{id}
</update>
```
{: id="20210330204518-ur3y2ie"}

- {: id="20210330204518-4a6cgtq"}resultType :结果类型
  {: id="20210330204518-knchw5y"}

  1. {: id="20210330204518-r5vebzt"}基本数据类型，统计Account总数
     {: id="20210330204518-tl0fr1x"}
  {: id="20210330204518-ohm2aqf"}
{: id="20210330204518-jsf3ijk"}

```xml
<select id="count" resultType="int">
    select count(id) from t_account
</select>
```
{: id="20210330204518-tehikfs"}

2. {: id="20210330204518-shekugv"}装类，统计Account总数
   {: id="20210330204518-6tqrkf6"}
{: id="20210330204518-gq2g0cg"}

```xml
<select id=Hcount2H resultType=Hjava.lang.IntegerH> select count(id) from t_account
</select>
```
{: id="20210330204518-s87m32a"}

3. {: id="20210330204518-lv13tgs"}String 类型，通过 id 查询 Account 的 name
   {: id="20210330204518-mgq29y1"}
{: id="20210330204518-b0h3x2m"}

```xml
<select id="findNameById" resultType=Hjava.lang.StringH> select username from t_account where id = #{id}
</select>
```
{: id="20210330204518-2yh8w6k"}

4. {: id="20210330204518-0dpgziz"}Java Bean
   {: id="20210330204518-pd2ow6y"}
{: id="20210330204518-ylqx544"}

```xml
<select id="findById" parameterType="long" resultType="com.southwind.entity.Account"> select * from t_account where id = #{id}
</select>
```
{: id="20210330204518-biudbtt"}

### 及联查询
{: id="20210330204518-ewdggxk"}

- {: id="20210330204518-wfd0g7d"}—对多
  {: id="20210330204518-xfsatpt"}
{: id="20210330204518-119rg6z"}

Student
{: id="20210330204518-53b6qaw"}

```java
package com.southwind.entity;
import lombok.Data;
@Data
public class Student {
    private long id;
    private String name;
    private Classes classes;
}
Classes
    package com.southwind.entity;
import lombok.Data;
import java.util.List;
@Data
public class Classes {
    private long id;
    private String name;
    private List<Student> students;
}
StudentRepository
    package com.southwind.repository;
import com.southwind.entity.Student;
public interface StudentRepository {
    public Student findById(long id);
}
```
{: id="20210330204518-wzoplnv"}

StudentRepository.xml
{: id="20210330204518-e20oaq9"}

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.southwind.repository.StudentRepository">
    <resultMap id="studentMap" type="com.southwind.entity.Student">
        <id column="id" property="id"></id>
        <result column="name" property="name"></result>
        <association property="classes" javaType="com.southwind.entity.Classes">
            <id column="cid" property="id"></id>
            <result column="cname" property="name"></result>
        </association>
    </resultMap>
    <select id="findById" parameterType="long" resultMap="studentMap">
        select s.id,s.name,c.id as cid,c.name as cname from student s,classes c
        where s.id = #{id} and s.cid = c.id
    </select>
</mapper>
```
{: id="20210330204518-4r9qq95"}

ClassesRepository
{: id="20210330204518-ov7ecik"}

```java
package com.southwind.repository;
import com.southwind.entity.Classes;
public interface ClassesRepository {
    public Classes findById(long id);
}
```
{: id="20210330204518-bbhjqmm"}

ClassesRepository.xml
{: id="20210330204518-a9fvimu"}

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.southwind.repository.ClassesRepository">
    <resultMap id="classesMap" type="com.southwind.entity.Classes">
        <id column="cid" property="id"></id>
        <result column="cname" property="name"></result>
        <collection property="students" ofType="com.southwind.entity.Student">
            <id column="id" property="id"/>
            <result column="name" property="name"/>
        </collection>
    </resultMap>
    <select id="findById" parameterType="long" resultMap="classesMap">
        select s.id,s.name,c.id as cid,c.name as cname from student s,classes c where c.id = #{id} and s.cid = c.id
    </select>
</mapper>
```
{: id="20210330204518-23gcj6r"}

- {: id="20210330204518-jjcskcr"}多对多
  {: id="20210330204518-t4w288s"}
{: id="20210330204518-f1o9t11"}

Customer
{: id="20210330204518-x8zfknt"}

```java
package com.southwind.entity;
import lombok.Data;
import java.util.List;
@Data
public class Customer {
    private long id;
    private String name;
    private List<Goods> goods;
}
Goods
    package com.southwind.entity;
import lombok.Data;
import java.util.List;
@Data
public class Goods {
    private long id;
    private String name;
    private List<Customer> customers;
}
CustomerRepository
    package com.southwind.repository;
import com.southwind.entity.Customer;
public interface CustomerRepository {
    public Customer findById(long id);
}
```
{: id="20210330204518-j4i7bia"}

CustomerRepository.xml
{: id="20210330204518-2az7ze5"}

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.southwind.repository.CustomerRepository">
    <resultMap id="customerMap" type="com.southwind.entity.Customer">
        <id column="cid" property="id"></id>
        <result column="cname" property="name"></result>
        <collection property="goods" ofType="com.southwind.entity.Goods">
            <id column="gid" property="id"/>
            <result column="gname" property="name"/>
        </collection>
    </resultMap>
    <select id="findById" parameterType="long" resultMap="customerMap">
        select c.id cid,c.name cname,g.id gid,g.name gname from customer c,goods
        g,customer_goods cg where c.id = #{id} and cg.cid = c.id and cg.gid = g.id </select>
</mapper>
```
{: id="20210330204518-lpef2p8"}

GoodsRepository
{: id="20210330204518-xxfe4ck"}

```java
package com.southwind.repository;
import com.southwind.entity.Goods;
public interface GoodsRepository {
    public Goods findById(long id);
}
```
{: id="20210330204518-funorma"}

GoodsRepository.xml
{: id="20210330204518-ivcy92e"}

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.southwind.repository.GoodsRepository">
    <resultMap id="goodsMap" type="com.southwind.entity.Goods">
        <id column="gid" property="id"></id>
        <result column="gname" property="name"></result>
        <collection property="customers" ofType="com.southwind.entity.Customer">
            <id column="cid" property="id"/>
            <result column="cname" property="name"/>
        </collection>
    </resultMap>
    <select id="findById" parameterType="long" resultMap="goodsMap">
        select c.id cid,c.name cname,g.id gid,g.name gname from customer c,goods
        g,customer_goods cg where g.id = #{id} and cg.cid = c.id and cg.gid = g.id </select>
</mapper>
```
{: id="20210330204518-ejbwosh"}

## 逆向工程
{: id="20210330204518-1lg6jry"}

MyBatis框架需要：实体类、自定义Mapper接口、Mapper.xml
传统的开发中上述的三个组件需要开发者手动创建，逆向工程可以帮助开发者来自动创建三个组件，减 轻开发者的工作量，提高工作效率。
{: id="20210330204518-7fm95lr"}

### 如何使用
{: id="20210330204518-b88no2o"}

MyBatis Generator,简称MBG,是一个专门为MyBatis框架开发者定制的代码生成器，可自动生成 MyBatis框架所需的实体类、Mapper接口、Mapper.xml,支持基本的CRUD操作，但是一些相对复 杂的SQL需要开发者自己来完成。
{: id="20210330204518-lco09jr"}

- {: id="20210330204518-bn469zy"}新建 Maven 工程，pom.xml
  {: id="20210330204518-34a3syt"}
{: id="20210330204518-1msp3fm"}

```xml
<dependencies>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.4.5</version>
    </dependency>
    <dependency>
        <groupId>mysql</groupId> <artifactId>mysql-connector-java</artifactId> <version>8.0.11</version>
    </dependency>
    <dependency>
        <groupId>org.mybatis.generator</groupId> <artifactId>mybatis-generator-core</artifactId> <version>1.3.2</version>
    </dependency>
</dependencies>
```
{: id="20210330204518-vtffjob"}

- {: id="20210330204518-20oslgz"}创建 MBG 配置文件 generatorConfig.xml
  {: id="20210330204518-ebf6jfc"}

  1. {: id="20210330204518-3e9urdw"}jdbcConnection配置数据库连接信息。
     {: id="20210330204518-xj30mac"}
  2. {: id="20210330204518-nye9zsg"}javaModelGenerator 配置JavaBean 的生成策略。
     {: id="20210330204518-kr79msh"}
  3. {: id="20210330204518-6q1oqw3"}sqlMapGenerator配置SQL映射文件生成策略。
     {: id="20210330204518-2c3rhur"}
  4. {: id="20210330204518-m23v1ph"}javaClientGenerator 配置 Mapper 接口的生成策略。
     {: id="20210330204518-gdhui2o"}
  5. {: id="20210330204518-y3jx38u"}table 配置目标数据表（tableName：表名，domainObjectName： JavaBean 类名）。
     {: id="20210330204518-8vg87l2"}
  {: id="20210330204518-l2sznjf"}
{: id="20210330204518-5am7gf5"}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorconfiguration
PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN" "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd"> <generatorConfiguration>
    <context id="testTables" targetRuntime="MyBatis3">
        <jdbcConnection driverClass="com.mysql.cj.jdbc.Driver" connectionURL="jdbc:mysql://localhost:3306/mybatis?
                                                                              useUnicode=true&characterEncoding=UTF-8"
                        userId="root"
                        password="root"
                        ></jdbcConnection>
        〈javaModelGenerator targetPackage="com.southwind.entity" targetProject="./src/main/java"></javaModelGenerator>
    <sqlMapGenerator targetPackage="com.southwind.repository" targetProject="./src/main/java"></sqlMapGenerator>
    〈javaClientGenerator type="XMLMAPPER" targetPackage="com.southwind.repository" targetProject="./src/main/java"> </javaClientGenerator>
<table tableName="t_user" domainObjectName="User"></table> </context>
</generatorConfiguration>
```
{: id="20210330204518-bc2b11s"}

- {: id="20210330204518-8jdxpxv"}创建Generator执行类。
  {: id="20210330204518-qdryve9"}
{: id="20210330204518-w92l7p7"}

```java
package com.southwind.test;
import org.mybatis.generator.api.MyBatisGenerator;
import org.mybatis.generator.config.Configuration;
import org.mybatis.generator.config.xml.ConfigurationParser;
import org.mybatis.generator.exception.InvalidConfigurationException;
import org.mybatis.generator.exception.XMLParserException;
import org.mybatis.generator.internal.DefaultShellCallback;
import java.io.File;
import java.io.IOException;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;
public class Main {
    public static void main(String[] args) {
        List<String> warings = new ArrayList<String>(); boolean overwrite = true;
        String genCig = "/generatorConfig.xml";
        File configFile = new File(Main.class.getResource(genCig).getFile());
        ConfigurationParser configurationParser = new
            ConfigurationParser(warings);
        Configuration configuration = null;
        try {
            configuration = configurationParser.parseConfiguration(configFile);
        } catch (IOException e) {
            e.printStackTrace();
        } catch (XMLParserException e) {
            e.printStackTrace();
        }
        DefaultShellCallback callback = new DefaultShellCallback(overwrite); MyBatisGenerator myBatisGenerator = null;
        try {
            myBatisGenerator = new MyBatisGenerator(configuration,callback,warings);
        } catch (InvalidConfigurationException e) {
            e.printStackTrace();
        }
        try {
            myBatisGenerator.generate(null);
        } catch (SQLException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```
{: id="20210330204518-f8pa1m8"}

## MyBatis延迟加载
{: id="20210330204518-e2v5i8z"}

- {: id="20210330204518-6ua8rex"}什么是延迟加载？
  {: id="20210330204518-xhvel9q"}
{: id="20210330204518-p7d0cum"}

延迟加载也叫懒加载、惰性加载，使用延迟加载可以提高程序的运行效率，针对于数据持久层的操作， 在某些特定的情况下去访问特定的数据库，在其他情况下可以不访问某些表，从一定程度上减少了 Java 应用与数据库的交互次数。
查询学生和班级的时，学生和班级是两张不同的表，如果当前需求只需要获取学生的信息，那么查询学 生单表即可，如果需要通过学生获取对应的班级信息，则必须查询两张表。
不同的业务需求，需要查询不同的表，根据具体的业务需求来动态减少数据表查询的工作就是延迟加 载。
{: id="20210330204518-kpsu50n"}

- {: id="20210330204518-sk946mt"}在config.xm I中开启延迟加载
  {: id="20210330204518-7ym76cn"}
{: id="20210330204518-pyg93lq"}

```xml
<settings>
    <!--打印SQL-->
    <setting name=HlogImplH value=HSTDOUT_LOGGINGH />
    <!--开启延迟加载-->
    <setting name="lazyLoadingEnabled" value="true"/>
</settings>
```
{: id="20210330204518-1gy6c51"}

- {: id="20210330204518-d2j4sy9"}将多表关联查询拆分成多个单表查询
  {: id="20210330204518-cvx4yay"}
{: id="20210330204518-4d6gdre"}

StudentRepository
{: id="20210330204518-vg559pj"}

```java
public Student findByIdLazy(long id);
```
{: id="20210330204518-jnavsc2"}

StudentRepository.xmI
{: id="20210330204518-j4w9plg"}

```xml
<resultMap id=HstudentMapLazyH type="com.southwind.entity.Student">
    <id column="id" property="id"></id>
    <result column=HnameH property=HnameH></result>
    <association property="classes" javaType=Hcom.southwind.entity.ClassesH
                 select=Hcom.southwind.repository.ClassesRepository.findByIdLazyH column="cid"> </association>
</resultMap>
<select id="findByIdLazy" parameterType=HlongH resultMap=HstudentMapLazyH>
    select * from student where id = #{id}
</select>
CIassesRepository
public Classes findByIdLazy(long id);
ClassesRepository.xml
<select id="findByIdLazy" parameterType="long"
        resultType="com.southwind.entity.Classes">
    select * from classes where id = #{id}
</select>
```
{: id="20210330204518-idvmhms"}

## MyBatis 缓存
{: id="20210330204518-8v1adra"}

- {: id="20210330204518-r7p9xce"}什么是MyBatis缓存
  {: id="20210330204518-404mnzt"}
{: id="20210330204518-3kgwvlr"}

使用缓存可以减少Java应用与数据库的交互次数，从而提升程序的运行效率。比如查询出id = 1的对 象，第一次查询出之后会自动将该对象保存到缓存中，当下一次查询时，直接从缓存中取出对象即可， 无需再次访问数据库。
{: id="20210330204518-hlatfa0"}

- {: id="20210330204518-grh4e7x"}MyBatis缓存分类
  {: id="20210330204518-qn2v6ay"}
{: id="20210330204518-2u39tb0"}

1. {: id="20210330204518-m69lp7o"}一级缓存：SqlSession级别，默认开启，并且不能关闭。
   操作数据库时需要创建SqlSession对象，在对象中有一个HashMap用于存储缓存数据，不同的 SqlSession之间缓存数据区域是互不影响的。
   一级缓存的作用域是SqlSession范围的，当在同一个SqlSession中执行两次相同的SQL语句事，第一 次执行完毕会将结果保存到缓存中，第二次查询时直接从缓存中获取。
   需要注意的是，如果SqlSession执行了 DML操作(insert、update、delete), MyBatis必须将缓存 清空以保证数据的准确性。
   {: id="20210330204518-lp8mrve"}
2. {: id="20210330204518-1atylk1"}二级缓存：Mapper级别，默认关闭，可以开启。
   使用二级缓存时，多个SqlSession使用同一个Mapper的SQL语句操作数据库，得到的数据会存在二 级缓存区，同样是使用HashMap进行数据存储，相比较于一级缓存，二级缓存的范围更大，多个 SqlSession可以共用二级缓存，二级缓存是跨SqlSession的。
   二级缓存是多个SqlSession共享的，其作用域是Mapper的同一个namespace,不同的SqlSession 两次执行相同的namespace下的SQL语句，参数也相等，则第一次执行成功之后会将数据保存到二级 缓存中，第二次可直接从二级缓存中取出数据。
   {: id="20210330204518-4144qoh"}
{: id="20210330204518-p74ftt9"}

> 代码
> {: id="20210330204518-gxype8f"}
{: id="20210330204518-3xxm6jd"}

- {: id="20210330204518-itoa0r0"}—级缓存
  {: id="20210330204518-2i3goas"}
{: id="20210330204518-nc831r0"}

```java
package com.southwind.test;
import com.southwind.entity.Account;
import com.southwind.repository.AccountRepository;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import java.io.InputStream;
public class Test4 {
    public static void main(String[] args) {
        Inputstream inputStream = Test.class.getClassLoader().getResourceAsStream("config.xml");
        SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
        SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(inputStream);
        SqlSession sqlSession = sqlSessionFactory.openSession();
        AccountRepository accountRepository = sqlSession.getMapper(AccountRepository.class);
        Account account = accountRepository.findById(1L);
        System.out.println(account);
        sqlSession.close();
        sqlSession = sqlSessionFactory.openSession();
        accountRepository = sqlSession.getMapper(AccountRepository.class);
        Account account1 = accountRepository.findById(1L);
        System.out.println(account1);
    }
}
```
{: id="20210330204518-xbg1817"}

- {: id="20210330204518-6s4ryu2"}二级缓存
  {: id="20210330204518-o854c0k"}
{: id="20210330204518-mwfu4ku"}

1. {: id="20210330204518-knzjodw"}MyBatis自带的二级缓存
   {: id="20210330204518-a77z9ib"}
{: id="20210330204518-jhktnfr"}

- {: id="20210330204518-5r2mv71"}config.xml配置开启二级缓存
  {: id="20210330204518-b0vzmkq"}
{: id="20210330204518-f2yf7cy"}

```xml
<settings>
    <!-- 打印SQL-->
    <setting name="logImpl" value="STDOUT_LOGGING" />
    <!--开启延迟加载-->
    <setting name="lazyLoadingEnabled" value="true"/>
    <!--开启二级缓存-->
    <setting name="cacheEnabled" value="true"/>
</settings>
```
{: id="20210330204518-2754ssh"}

- {: id="20210330204518-zum2b2k"}Mapper.xml中配置二级缓存
  {: id="20210330204518-nk276l4"}
{: id="20210330204518-qj34bfa"}

```xml
<cache></cache>
```
{: id="20210330204518-nf0supc"}

- {: id="20210330204518-daokbmg"}实体类实现序列化接口
  {: id="20210330204518-ougdnzr"}
{: id="20210330204518-x214uk5"}

```java
package com.southwind.entity;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;
import java.io.Serializable;
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Account implements Serializable {
    private long id;
    private String username;
    private String password;
    private int age;
}
```
{: id="20210330204518-b0lruqy"}

2. {: id="20210330204518-utrnlqq"}ehcache 二级缓存
   {: id="20210330204518-4ry7ymw"}
{: id="20210330204518-nzmttvt"}

- {: id="20210330204518-rbg06kw"}pom.xml添加相关依赖
  {: id="20210330204518-ww35ua2"}
{: id="20210330204518-0hrid9s"}

```xml
<dependency>
    <groupId>org.mybatis</groupId> <artifactId>mybatis-ehcache</artifactId> <version>1.0.0</version>
</dependency>
<dependency>
    <groupId>net.sf.ehcache</groupId> <artifactId>ehcache-core</artifactId> <version>2.4.3</version>
</dependency>
```
{: id="20210330204518-o2h11rq"}

- {: id="20210330204518-4n9kuvi"}添加 ehcache.xml
  {: id="20210330204518-ph80cbh"}
{: id="20210330204518-ablj0mp"}

```xml
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="../config/ehcache.xsd"> <diskStore/>
    <defaultCache
                  maxElementsInMemory="1000"
                  maxElements0nDisk="10000000"
                  eternal="false"
                  overflowToDisk="false"
                  timeToIdleSeconds="120"
                  timeToLiveSeconds="120"
                  diskExpiryThreadIntervalSeconds="120" memoryStoreEvictionPolicy="LRU">
    </defaultCache>
</ehcache>
```
{: id="20210330204518-f23so26"}

- {: id="20210330204518-cjwxt3r"}config.xml配置开启二级缓存
  {: id="20210330204518-13uacnv"}
{: id="20210330204518-vdc1eso"}

```xml
<settings>
    <!-- 打印SQL-->
    <setting name="logImpl" value="STDOUT_LOGGING" /> 
    <!--开启延迟加载-->
    <setting name=HlazyLoadingEnabledH value=HtrueH/>
    <!--开启二级缓存-->
    <setting name="cacheEnabled" value="true"/>
</settings>
```
{: id="20210330204518-khs9bnl"}

- {: id="20210330204518-5lqphmn"}Mapper.xml中配置二级缓存
  {: id="20210330204518-fqi6t2r"}
{: id="20210330204518-xs70j7l"}

```xml
<cache type="org.mybatis.caches.ehcache.EhcacheCache">
    <!--缓存创建之后，最后一次访问缓存的时间至缓存失效的时间间隔-->
    <property name="timeToIdleSeconds" value="3600"/>
    <!--缓存自创建时间起至失效的时间间隔-->
    <property name="timeToLiveSeconds" value="3600"/>
    <!--缓存回收策略，LRU表示移除近期使用最少的对象-->
    <property name="memoryStoreEvictionPolicy" value="LRU"/> 
</cache>
```
{: id="20210330204518-jgxc7fs"}

- {: id="20210330204518-u9vb15o"}实体类不需要实现序列化接口。
  {: id="20210330204518-5vqmsbg"}
{: id="20210330204518-i47vxha"}

```java
package com.southwind.entity;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Account {
    private long id;
    private String username;
    private String password;
    private int age;
}
```
{: id="20210330204518-7wcleku"}

## MyBatis 动态 SQL
{: id="20210330204518-w5b73v6"}

使用动态SQL可简化代码的开发，减少开发者的工作量，程序可以自动根据业务参数来决定SQL的组 成。
{: id="20210330204518-37n6lcj"}

- {: id="20210330204518-2v14eqx"}if标签
  {: id="20210330204518-amfy9eb"}
{: id="20210330204518-7i7kqid"}

```xml
<select id="findByAccount" parameterType="com.southwind.entity.Account" resultType="com.southwind.entity.Account">
    select * from taccount where
    <if test="id!=0"> 
        id = #{id}
    </if>
    <if test="username!=null"> 
        and username = #{username}
    </if>
    <if test="password!=null">
        and password = #{password}
    </if>
    <if test="age!=0">  
        and age = #{age}
    </if>
</select>
```
{: id="20210330204518-sveb7bd"}

if标签可以自动根据表达式的结果来决定是否将对应的语句添加到SQL中，如果条件不成立则不添加， 如果条件成立则添加。
{: id="20210330204518-5u4tajb"}

- {: id="20210330204518-h4psfuh"}where标签
  {: id="20210330204518-oneiegd"}
{: id="20210330204518-7xgzzfn"}

```xml
<select id="findByAccount" parameterType="com.southwind.entity.Account" resultType="com.southwind.entity.Account">
    select * from t_account
    <where>
        <if test="id!=0">
            id = #{id}
        </if>
        <if test="username!=null">
            and username = #{username}
        </if>
        <if test="password!=null">
            and password = #{password}
        </if>
        <if test="age!=0">
            and age = #{age}
        </if>
    </where>
</select>
```
{: id="20210330204518-apxe8q8"}

where标签可以自动判断是否要删除语句块中的and关键字，如果检测到where直接跟and拼接，则 自动删除and,通常情况下if和where结合起来使用。
{: id="20210330204518-o1u39pk"}

- {: id="20210330204518-crq7p8t"}choose 、 when 标签
  {: id="20210330204518-6utrbcx"}
{: id="20210330204518-pa03j7c"}

```xml
<select id="findByAccount" parameterType="com.southwind.entity.Account" resultType="com.southwind.entity.Account">
    select * from t_account
    <where>
        <choose>
            <when test="id!=0">
                id = #{id}
            </when>
            <when test=Husername!=nullH>
                username = #{username}
            </when>
            <when test="password!=null">
                password = #{password}
            </when>
            <when test="age!=0">
                age = #{age}
            </when>
        </choose>
    </where>
</select>
```
{: id="20210330204518-mm2b70a"}

- {: id="20210330204518-aq3mic5"}trim标签
  {: id="20210330204518-qrvpkb2"}
{: id="20210330204518-dwd813h"}

trim标签中的prefix和suffix属性会被用于生成实际的SQL语句，会和标签内部的语句进行拼接，如 果语句前后出现了 prefixOverrides或者suffixOverrides属性中指定的值，MyBatis框架会自动将其删 除。
{: id="20210330204518-k2yplmb"}

```xml
<select id="findByAccount" parameterType="com.southwind.entity.Account" resultType="com.southwind.entity.Account">
    select * from t_account
    <trim prefix="where" prefixOverrides="and">
        <if test="id!=0">
            id = #{id}
        </if>
        <if test="username!=null">
            and username = #{username}
        </if>
        <if test="password!=null">
            and password = #{password}
        </if>
        <if test="age!=0">
            and age = #{age}
        </if>
    </trim>
</select>
```
{: id="20210330204518-rclsb09"}

- {: id="20210330204518-sh96qcw"}set标签
  {: id="20210330204518-0s7eput"}
{: id="20210330204518-9qs2owk"}

set标签用于update操作，会自动根据参数选择生成SQL语句。
{: id="20210330204518-iyapcvy"}

```xml
<update id="update" parameterType="com.southwind.entity.Account">
    update t_account
    <set>
        <if test="username!=null">
            username = #{username},
        </if>
        <if test=Hpassword!=nullH> password = #{password},
        </if>
        <if test=Hage!=0H>
            age = #{age}
        </if>
    </set>
    where id = #{id}
</update>
```
{: id="20210330204518-60939m1"}

- {: id="20210330204518-lr33797"}foreach 标签
  {: id="20210330204518-kezsh3v"}
{: id="20210330204518-4ryrx1g"}

foreach标签可以迭代生成一系列值，这个标签主要用于SQL的in语句。
{: id="20210330204518-y86sv9f"}

```xml
<select id="findByIds" parameterType="com.southwind.entity.Account" resultType="com.southwind.entity.Account"> 
    select * from t_account 
    <where> 
        <foreach collection="ids" open="id in (" close=")" item="id" separator=",">
            #{id} 
        </foreach>
    </where> 
</select>
```
{: id="20210330204518-ohfb7nd"}


{: id="20210330204518-mp2voo5" type="doc"}
