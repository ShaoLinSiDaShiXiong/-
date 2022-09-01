# MyBatis

MyBatis 是一个开源、轻量级的数据持久化框架，是 JDBC 和 Hibernate 的替代方案。

**MyBatis是一个开源的，轻量级的数据持久化框架，MyBatis内部封装了JDBC操作，简化了加载驱动，创建连接，创建statement等过程。**

MyBatis 支持定制化 SQL、存储过程以及高级映射，可以在实体类和 SQL 语句之间建立映射关系，是一种半自动化的 ORM 实现。其封装性低于 Hibernate，但性能优秀、小巧、简单易学、应用广泛。

> ORM（Object Relational Mapping，对象关系映射）是一种数据持久化技术，它在对象模型和关系型数据库之间建立起对应关系，并且提供了一种机制，通过 JavaBean 对象去操作数据库表中的数据。

## Eclipse使用MyBatis

### 在项目中导入相应的jar包

想要使用MyBatis首先需要下载MyBatis和MySql的jar包。

```xml
    <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.29</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.5.10</version>
    </dependency>
```



****



### 编写Mybatis配置文件

在eclipse中需要在src/main/java目录下进行mybatis-config.xml文件的编写，其代码如下：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-config.dtd">

<!-- 通过这个配置文件完成mybatis与数据库的连接 -->
<configuration>

	<!-- 引入 database.properties 文件 -->
	<properties resource="database.properties" />

    <!-- 进行日志的设置 -->
	<settings>
		<setting name="logImpl" value="STDOUT_LOGGING" />
	</settings>

	<environments default="development">
		<environment id="development">
			<!--配置事务管理，采用JDBC的事务管理 -->
			<transactionManager type="JDBC"></transactionManager>
			<!-- POOLED:mybatis自带的数据源，JNDI:基于tomcat的数据源 -->
			<dataSource type="POOLED">
				<property name="driver" value="${driver}" />
				<property name="url" value="${url}" />
				<property name="username" value="${user}" />
				<property name="password" value="${password}" />
			</dataSource>
		</environment>
	</environments>
	<!-- 将mapper文件加入到配置文件中 -->
	<mappers>
		<mapper resource="com/MybatisTest/dao/mapper/MyBatisTestMapper.xml" />
		<mapper resource="com/MybatisTest/dao/mapper/MBMapper.xml" />
	</mappers>
</configuration>

```

**jdbc:mysql://localhost:3306/（数据库名）?allowPublicKeyRetrieval=true&serverTimezone=UTC&useSSL=false&useUnicode=true&characterEncoding=UTF-8**

<font color="#F00">配置数据库信息的properties文件的检测是从resource文件开始检测的</font>

#### mapper绑定的四种方式

在进行mapper文件绑定的时候，有四种方式，一种是通过mapper接口，一种是直接加载mapper.xml文件，一种是通过绝对路径进行加载和扫描加载包内所有的mapper.xml文件。

1. **resource：**

   通过resource属性进行xml文件加载的时候是通过maven项目中的resource文件夹开始寻找的，我们可以将相关的所有mapper.xml文件全部直接放在resource文件夹中，或者通过maven项目加载后的相对路径来寻找需要的文件。**需要注意的是，maven项目只会加载resource文件夹中的资源文件。**

   ```xml
       <!-- 将mapper文件加入到配置文件中 -->
       <mappers>
           <!--通过resource文件夹进行加载-->
           <mapper resource="dao/mapper/UserMapper.xml"/>
   
       </mappers>
   ```

2. **class：**

   通过class进行xml文件加载的时候加载的是mapper接口，而不是xml文件，所以我们需要保证xml文件和mapper接口在一个包内，且名字一样，这样mybatis-config文件才会找到相应的mapper.xml文件，否则就会爆出找不到相关方法的错误。**注意sqlsession加载时不会报错，方法可以正常调用，但是使用时会报错。**

   ```xml
       <!-- 将mapper文件加入到配置文件中 -->
       <mappers>
           <!--通过映射接口的全限定类名加载-->
           <mapper class="dao.mapper.IUserMapper"/>
       </mappers>
   ```

   

3. **url：**

   通过url时，是通过绝对路径来对mapper.xml文件进行查找的，这里需要在绝对路径前面加上`file:///`，这里的file必须有三个斜线。

   ```xml
       <!-- 将mapper文件加入到配置文件中 -->
       <mappers>
           <!--使用完全限定资源定位符url-->
           <mapper url="file:///E:\文件\IDEAfile\SpringMybatisDemo\src\main\java\dao\mapper\UserMapper.xml"/>
       </mappers>
   ```

4. **< package name="">**

   这种方式是通过包来查找mapper文件，mybatis会自动扫描所有的mapper接口和mapper.xml文件，并通过文件名来进行匹配。**注意mapper接口和xml文件必须要在一个包内才可以成功被检测到，否则会报出找不到相应方法的错误。**

   ```xml
       <mappers>
           <!--通过扫描包来进行xml和接口的加载-->
           <package name="dao.mapper"/>
   	</mappers>
   ```

##### 让maven加载所有的xml文件

**在pom.xml文件中进行配置**

```xml
<!-- 项目打包时会将java目录中的*.xml文件也进行打包 -->
<build>
    <resources>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.xml</include>
            </includes>
            <filtering>false</filtering>
        </resource>
    </resources>
</build>
```

**在application.properties中进行配置**

```properties
#配置mapper xml文件的路径
mybatis-plus.mapper-locations=classpath:com/yz/eduservice/mapper/xml/*.xml
```

****





#### 关于propertise文件

在上边的代码中可以看见有关于数据库创建链接的信息是通过一个已经写好的propertise文件进行配置的。这样做的好处是，如果后面我们想修改相关的数据库链接的信息，操作的只是propertise文件，而不是在xml文件内修改相关配置。相当于我们不用对源码做出改变，减少了我们思考的工作量，增加了代码的原子性，使得代码更加简单，易懂。

下面列出对应上方代码的propertise文件信息。

```
driver=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306/test?allowPublicKeyRetrieval=true&serverTimezone=UTC&useSSL=false&useUnicode=true&characterEncoding=UTF-8
user=root
password=123456
```

这里分别是MySql的驱动，数据库连接，用户名和用户密码，propertise文件都是以**key/value**的形式存在的当该配置文件被解析的时候会通过“=”进分割，从而通过key拿到相应value的内容。

****

### 创建实体类pojo

因为Mybatis也是对数据库进行操作，所以对应相应的表就应该有相应的实体类。该实体类必须要与数据库中表的各个字段一一对应。

此处创建一个最简单的实体类。

```java
package com.MybatisTest.pojo;

public class MB {
	private Integer id;
	private String name;
	public Integer getId() {
		return id;
	}
	public void setId(Integer id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	@Override
	public String toString() {
		return "MB [id=" + id + ", name=" + name + "]";
	}
}
```



![image-20220426220407678](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220426220407678.png)



****



### 编写映射文件（Mapper）

这一步是最重要的一步，Mybatis是ORM实现的框架。其中最核心的代码就是Mapper.xml文件，该文件内可以进行sql语句的编写，通过mybatis-config.xml文件中的<mapper>标签进行关联。代码如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.MybatisTest.dao.mapper.MBMapper">
	<!-- 通过id查询用户 -->
	<select id="findUserById" parameterType="int"  resultType="com.MybatisTest.pojo.MB">
		select * from mb where id = #{id}
	</select>
</mapper>
```

<mapper> 元素是配置文件的根元素，它包含了 namespace 属性，该属性值通常设置为“包名+SQL映射文件名”，用于指定唯一的命名空间。

子元素 <select>、<insert> 中的信息用于执行查询、添加操作。在定义的 SQL 语句中，“#{}”表示一个占位符，相当于“?”，而“#{name}”表示该占位符待接收参数的名称为 name。

这里只写了一个简单的通过id查询用户名的sql。其中<select>标签内的parameterType属性是用来指定传入参数的类型为int或Integer，resultType属性是指返回的数据类型。标签内是对应的select sql语句



****



### 创建测试类

前面已经做好了最基本的准备工作，接下来就是mybatis的简单使用。代码如下：

```java
package com.MybatisTest;

import java.io.IOException;
import java.io.InputStream;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import com.MybatisTest.pojo.MB;


public class MyBatisTest {
	public static void main(String[] args) {
		SqlSession sqlsession = null;
		InputStream is = null;
		String config = "mybatis-config.xml";
//		
//		try {
//			is = Resources.getResourceAsStream(config);
//			SqlSessionFactory factory = new SqlSessionFactoryBuilder().build(is);
//			sqlsession = factory.openSession();
//			int i = sqlsession.selectOne("com.MybatisTest.dao.mapper.MyBatisTestMapper.conunt");
//			String name = sqlsession.selectOne("com.MybatisTest.dao.mapper.MyBatisTestMapper.getname");
//			sqlsession.commit();
//			sqlsession.close();
//			System.out.println(i);
//			System.out.println(name);
//			
//		} catch (IOException e) {
//			// TODO Auto-generated catch block
//			e.printStackTrace();
//		}
		
		try {
            //通过Resouerces类的getResourceAsStream来获取mybatis-config.xml文件的输入流
			is = Resources.getResourceAsStream(config);
			
            //通过SqlSessionFactoryBuilder().build(is)方法来获得SqllSessionFactory对象
            //通过SqllSessionFactory对象来获得SqlSession。
			sqlsession = new SqlSessionFactoryBuilder().build(is).openSession();
            
            //执行映射文件中的select方法，并且传入参数。
			MB mb = (MB) sqlsession.selectOne("com.MybatisTest.dao.mapper.MBMapper.findUserById", 1);
            
            //打印输出
			System.out.println(mb);
			
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
}

```

![image-20220426221623218](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220426221623218.png)

<font color="#f00">**需要注意的是，在使用Mybatis进行添加删除，修改等操作的时候需要手动的进行事务提交，否则sql不会被执行，因为MyBatis事务处理是默认开启的，也就是需要手动进行事务提交。代码如下：**</font>

```java
	MB mb1 = new MB();
	mb1.setName("张三");
	int i = sqlsession.insert("add",mb1);
	System.out.println("成功向数据库中添加了"+i+"条数据");
	sqlsession.commit();
	sqlsession.close();
```

![image-20220426223914724](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220426223914724.png)

![image-20220426224000322](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220426224000322.png)



****

### 使用映射实现SQL语句

想要实现通过.xml文件进行映射Java接口，首先要进行相应xml文件的编写，其中最重要的就是命名空间的编写。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!-- 这里的namepace属性需要填入Mapper文件对应的Mapper接口的全限定类名 -->
<mapper namespace="com.MybatisTest.dao.mapper.MBMapper">
	<!-- 通过id查询用户 -->
	<select id="findUserById" parameterType="int"  resultType="com.MybatisTest.pojo.MB">
		select * from mb where id = #{id}
	</select>
	<insert id="add" parameterType="com.MybatisTest.pojo.MB" >
		INSERT INTO mb (name) VALUES(#{name})
	</insert>
</mapper>
```

**提示** **对命名空间的一点补充**

在之前版本的 MyBatis 中，**命名空间（Namespaces）**的作用并不大，是可选的。 但现在，随着命名空间越发重要，你必须指定命名空间。

命名空间的作用有两个，一个是利用更长的全限定名来将不同的语句隔离开来，同时也实现了你上面见到的接口绑定。就算你觉得暂时用不到接口绑定，你也应该遵循这里的规定，以防哪天你改变了主意。 长远来看，只要将命名空间置于合适的 Java 包命名空间之中，你的代码会变得更加整洁，也有利于你更方便地使用 MyBatis。

**命名解析：**为了减少输入量，MyBatis 对所有具有名称的配置元素（包括语句，结果映射，缓存等）使用了如下的命名解析规则。

- 全限定名（比如 “com.mypackage.MyMapper.selectAllThings）将被直接用于查找及使用。
- 短名称（比如 “selectAllThings”）如果全局唯一也可以作为一个单独的引用。 如果不唯一，有两个或两个以上的相同名称（比如 “com.foo.selectAllThings” 和 “com.bar.selectAllThings”），那么使用时就会产生“短名称不唯一”的错误，这种情况下就必须使用全限定名。

**当完成了xml文件的基本编写之后，就需要完成Mapper接口的编写，上面可以看到命名空间指定了一个全限定类名为com.MybatisTest.dao.mapper.MBMapper的MBMapper类。**<font color="#f00">**需要注意，这里指定的应该是一个接口。书写格式如下**</font>

```java
package com.MybatisTest.dao.mapper;

import java.util.ArrayList;

import com.MybatisTest.pojo.MB;

public interface MBMapper {

	//@Select("SELECT * FROM blog WHERE id = #{id}")当使用文档注释给接口添加sql的时候就可以不需要<select>标签了
	public ArrayList<MB> findUserById(int id);
}

```

**该接口的方法就会映射到xml文件中的同名的标签，当通过SqlSession来获得Mapper的时候，就可以通过MyBatis给创建的Mapper对象的对应方法来传入参数。**

```java
try(SqlSession sqlsession = MyBatisUtil.createSqlSession()){
		MBMapper mb = sqlsession.getMapper(MBMapper.class);
		ArrayList<MB> m = mb.findUserById(1);
		for(MB a: m) {
		System.out.println(a);
	}
}
```



****

## MyBatis三个核心类的作用域（Scope）和生命周期

**不同作用域和生命周期类别是至关重要的，因为错误的使用会导致非常严重的并发问题。**

### SqlSessionFactoryBuilder

这个类可以被实例化、使用和丢弃，一旦创建了 SqlSessionFactory，就不再需要它了。 因此 SqlSessionFactoryBuilder 实例的最佳作用域是方法作用域（也就是局部方法变量）。 你可以重用 SqlSessionFactoryBuilder 来创建多个 SqlSessionFactory 实例，但最好还是不要一直保留着它，以保证所有的 XML 解析资源可以被释放给更重要的事情。



****

### SqlSessionFactory

SqlSessionFactory 一旦被创建就应该在应用的运行期间一直存在，没有任何理由丢弃它或重新创建另一个实例。 使用 SqlSessionFactory 的最佳实践是在应用运行期间不要重复创建多次，多次重建 SqlSessionFactory 被视为一种代码“坏习惯”。因此 SqlSessionFactory 的最佳作用域是应用作用域。 有很多方法可以做到，最简单的就是使用单例模式或者静态单例模式。



****

### SqlSession

每个线程都应该有它自己的 SqlSession 实例。SqlSession 的实例不是线程安全的，因此是不能被共享的，所以它的最佳的作用域是请求或方法作用域。 绝对不能将 SqlSession 实例的引用放在一个类的静态域，甚至一个类的实例变量也不行。 也绝不能将 SqlSession 实例的引用放在任何类型的托管作用域中，比如 Servlet 框架中的 HttpSession。 如果你现在正在使用一种 Web 框架，考虑将 SqlSession 放在一个和 HTTP 请求相似的作用域中。 换句话说，每次收到 HTTP 请求，就可以打开一个 SqlSession，返回一个响应后，就关闭它。 这个关闭操作很重要，为了确保每次都能执行关闭操作，你应该把这个关闭操作放到 finally 块中。 下面的示例就是一个确保 SqlSession 关闭的标准模式：

```java
try (SqlSession session = sqlSessionFactory.openSession()) {
  // 你的应用逻辑代码
}
```



****

### 映射器实例

映射器是一些绑定映射语句的接口。映射器接口的实例是从 SqlSession 中获得的。虽然从技术层面上来讲，任何映射器实例的最大作用域与请求它们的 SqlSession 相同。但方法作用域才是映射器实例的最合适的作用域。 也就是说，映射器实例应该在调用它们的方法中被获取，使用完毕之后即可丢弃。 映射器实例并不需要被显式地关闭。尽管在整个请求作用域保留映射器实例不会有什么问题，但是你很快会发现，在这个作用域上管理太多像 SqlSession 的资源会让你忙不过来。 因此，最好将映射器放在方法作用域内。就像下面的例子一样：

```
try (SqlSession session = sqlSessionFactory.openSession()) {
  BlogMapper mapper = session.getMapper(BlogMapper.class);
  // 你的应用逻辑代码
}
```



****

## ${}和#{}的区别

当我们使用Mapper.xml文件进行sql语句编写的时候，经常会通过${}和#{}来获取传需要放进sql语句的参数值，在大多数情况下，两种方式都可以使用，但是他们的本身代表的含义和正规的使用方式却大不相同。

- **${value}**：

  这种是以字符串拼接的方式将数据放入SQL语句中，类似于JDBC操作中使用Statement对象来进行SQL语句的操作；

  SELECT * FROM user WHERE id=’${id}‘ == 

  SELECT * FROM user WHERE id='id'

  <font color="#F00">**这里需要特别注意，使用${}只是字符串的拼接，所以需要我们特别注意单引号的问题。**</font>

- **#{value}**:

  SELECT * FROM user WHERE id=#{id} == 
  
  SELECT * FROM user WHERE id=?

****

### 使用#{}需要应对的情况

从上面的代码中我们可以看到，${}是字符串的拼接，在大部分sql中使用，十分的方便，但是这样使用的安全性又不能得到保障，因此在面对需要字符串拼接且需要使用#{}的时候，可以使用**CONCAT函数**来进行字符串的拼接。

**代码如下：**

```xml
<!-- 通过模糊查询来通过性别和姓名来查询用户 -->
	<select id="findUserByGender" resultType="dao.pojo.User" parameterType="Map">
		SELECT * FROM user WHERE gender=${gender} AND username LIKE CONCAT('%',#{name},'%')
	</select>
```

这样就可以使用#{}来完成字符串的拼接，且不用担心sql注入的问题。<font color="#F00">👍</font>

****

## MyBatis获取参数值的几种情况

我们在配置好Mapper.xml文件之后，在通过MyBatis来执行sql时，我们一般会通过映射来放入参数，然后MyBatis来解析我们传入的参数，再将解析好的参数放入SQL中，最后在执行，返回对应的结果。

**需要注意的有MyBatis传入参数的几种情况。**

1. **映射只传入一个参数：**

   当我们写好的sql只需要传入一个参数的时候，我们可以以任意的字面量来访问我们传入的参数，且`#${}`都可以使用，唯一需要注意的点只有使用${}的时候需要考虑单引号问题。

   **映射接口代码：**

   ```java
   public User findUserByName(Strign name);
   ```

   **xml文件代码：**

   ```xml
   <select id="findUserByName" resultType="User">
   	<!--SELECT * FROM user WHERE name='${name}'-->
       SELECT * FROM user WHERE name=#{name}
   </select>
   ```

   <font color="#F00">**这里我们通过{}来获取传入参数的时候里面的字面量可以是任意值，即使叫age，他也会获取我们传入的参数。**</font>

2. **映射传入多个参数：**

   如果我们的写好的sql执行需要多个参数，那么我们获取参数的方式就没有只获取一个参数那么简单了。

   **当我们通过接口映射来传入多个参数的时候，MyBatis会将我们传入的所有参数放入一个已经定义好的Map集合中，并且以两种key来存储我们传入的值。**

   - 以arg0，arg1key的形式，将我们传入的参数放如集合中。
   - 以param1，parame2的key的形式，将我们传入的参数放入集合中。

   **映射接口代码：**

   ```java
   public User findUserByName(Integer gender,Strign name);
   ```

   **xml文件代码：**

   ```xml
   <select id="findUserByName" resultType="User">
   	<!--SELECT * FROM user WHERE username='${arg0}' AND password='${arg1}'-->
       <!--SELECT * FROM user WHERE username='${param1}' AND password='${param2}'-->
       SELECT * FROM user WHERE username='${arg0}' AND password=${param2}
   </select>
   ```

   **我们就可以通过键来访问对应的值，该值和传入参数的顺序有关。**

   <font color="#F00">当然只要我们可以清晰的记住我们需要传入参数的标准，那么我们可以采用上面的混合方式来传入参数，但是并不建议这样做，因为一旦数据较多就会代码就会变得很混乱。</font>

3. **映射直接传入Map集合：**

   上面我们可以看到获取多个参数可以使用的时MyBatis来给我们提供的Map和规定的key来获多个不同参数，虽然够用，但是不够见名知意，因此我们也可以自己来规定我们自己的key，这样我们就可以通过key来访问value，且不用考虑顺序的问题。

   <font color="#f00">这样做和好处是我们可以自定义键名</font>

   **Mapper接口的代码：**

   ```java
   	/**
   	 * 通过性别和姓名进行模糊查询
   	 * 
   	 * @param map 包含用户输入的姓名和性别
   	 * @return 返回对应的User对象集合
   	 */
   	public ArrayList<User> findUserByGender(Map<String,Object> map);
   ```

   **测试类对应代码：**

   ```java
   	@Test
   	public void findUserByGender() {
   		//首先拆创建一个Map集合
   		Map<String,Object> map = new HashMap<>();
   		//在集合中放入我们需要的键值对
   		map.put("gender", 1);
   		map.put("name", "l");
   		//将map放入映射中
   		com.mapper.user.UserMapper mapper = MyBatisUtil.createSqlSession().getMapper(com.mapper.user.UserMapper.class);
   		mapper.findUserByGender(map);
   	}
   ```

   **Mapper.xml文件对应代码：**

   ```xml
   <!-- 通过模糊查询来通过性别和姓名来查询用户 -->
   	<select id="findUserByGender" resultType="com.pojo.User" parameterType="Map">
   		SELECT * FROM user WHERE gender=${gender} AND username LIKE '%${name}%'
   	</select>
   ```

    **执行成功：**

   ```
   Opening JDBC Connection
   Created connection 1408974251.
   Setting autocommit to false on JDBC Connection [com.mysql.cj.jdbc.ConnectionImpl@53fb3dab]
   ==>  Preparing: SELECT * FROM user WHERE gender=1 AND username LIKE '%l%'
   ==> Parameters: 
   <==    Columns: id, sum_id, user_code, username, userpassword, gender, birthday, phone, address, userrole, createby, creationdate, modifyby, modifydate
   <==        Row: 2, 2, lzy666, lzy, 111, 1, 2022-05-05, 15165346874651, 云南, 1, 1, 2022-05-05 15:48:38, 1, 2022-05-05 15:48:41
   <==      Total: 1
   ```

4. **映射传入一个pojo实例对象：**

   在正常的网页中，如果我们需要针对数据库来进行数据处理，我们最常用的就是在映射接口中传入一个对应的实体类，我么在xml文件中想要获取实体类中的属性，**只需要通过以`$#{}`内加上属性名来获取属性值即可**，他的原理类似于在Map中获取值。

   **映射接口代码：**

   ```java
   public Integer insertUser(User user);
   ```

   **xml文件代码：**

   ```xml
   <insert id="insertUser" parameterType="com.pojo.User">
   		<!-- INSERT INTO user(sum_id,user_code,username,userpassword,gender,birthday,phone,address,userrole,createby,creationdate,modifyby,modifydate) VALUES(#{sum_id},${user_code},${username},${userpassword},#{gender},${birthday},${phone},${address},#{userrole},#{createby},${creationdate},#{modifyby},${modifydate}) -->
   		INSERT INTO user(sum_id,user_code,username,userpassword,gender,phone,address,userrole,createby) VALUES(#{sum_id},#{user_code},#{username},#{userpassword},#{gender},#{phone},#{address},#{userrole},#{createby})
   	</insert>
   ```

5. **使用@Param注解：**

   MyBatis提供了一个@Param的注解，他可以在MyBatis原有的Map基础上来提供给我们自定key的方法。简单来说就是我们可以通过@Param注解来自定以多个参数的key且不用我们手动创建Map。

   **映射接口代码：**

   ```java
   public User checkLoginByParam(@Param("username") Strign username,@Param("passwored"));
   ```

   **xml文件代码：**

   ```xml
   <select id="checkLoginByParam" resultType="User">
   	SELECT * FROM user WHERE usernaem=#{usernaem} AND password=#{passwoed}
   </select>
   ```

   通过以上的方式，我们就可以通过我们自定以的参数来获取对应的value。

   **当我们使用@Param注解来自定以key的时候，注解传入的value就是key，后面的属性就是我们的值，MyBatis会将我们自定义的注解放入MyBatis自己的Map中。当我们使用@Param注解来自定义key的时候，有两种方式通过key来获取我们的参数值：**

   - 以@Param中值为key的形式，将我们传入的参数放如集合中。
   - 以param1，parame2的key的形式，将我们传入的参数放入集合中。

****

## MyBatis起别名typeAliases

我们在编写Mapper.xml文件的时候，在填写resultType返回类型的时候，需要填入全限定类名，如果包过多的话，需要填入的内容就会很多，这样无疑增加了我们编写代码的时间。

**使用别名可以减少我们书写那些大量重复且没有太大用处包名**

**代码如下：**

```xml
<typeAliases>
		<!-- <typeAlias alias="User" type="dao.pojo.User"/> -->
		<package name="dao.pojo"/>
	</typeAliases>
```

- **typeAilases：**

  该标签的

****

## resultMap

**resultmap是mybatis中最复杂的元素之一，它描述如何从结果集中加载对象，主要作用是定义映射规则、级联的更新、定制类型转化器。**

#### resultmap构成元素

| 元素          | 子元素     | 作用                                                     |
| ------------- | ---------- | -------------------------------------------------------- |
| constructor   | idArg，arg | 用于配置构造器方法                                       |
| id            |            | 将结果集标记为id，以方便全局调用。                       |
| result        |            | 配置POJO到数据库列表映射关系                             |
| association   | 级联使用   | 表示一对一关系                                           |
| collection    | 级联使用   | 表示一对多关系                                           |
| discriminator | 级联使用   | 鉴别器，根据实际选择实例，可以通过特定的条件确定结果集。 |

#### resultMap使用方法：

#### Mapper.xml配置

想要使用resultMap来从结果集中加载对象，首先要进行mapper文件的配置：

```xml
<mapper namespace="dao.mapper.bill.BillMapper">

	<resultMap type="dao.pojo.Bill" id="Bill_t">
		<id property="id" column="id"/>
		<result property="id" column="id"/>
		<result property="billcode" column="billcode"/>
		<result property="porductname" column="porductname"/>
		<result property="porductunit" column="porductunit"/>
		<result property="productcount" column="productcount"/>
		<result property="totalprice" column="totalprice"/>
		<result property="ispayment" column="ispayment"/>
		<result property="createdby" column="createdby"/>
		<result property="creationdate" column="creationdate"/>
		<result property="modifyby" column="modifyby"/>
		<result property="modifydate" column="modifydate"/>
		<result property="providerId" column="providerId"/>
		
		<association property="provider" javaType="dao.pojo.Provider">
			<id property="id" column="id"/>
			<result property="porcode" column="porcode"/>
			<result property="porname" column="porname"/>
			<result property="porcontact" column="porcontact"/>
			<result property="porphone" column="porphone"/>
			<result property="poraddress" column="poraddress"/>
			<result property="profax" column="profax"/>
			<result property="createby" column="createby"/>
			<result property="creationdate" column="creationdate"/>
			<result property="modifyby" column="modifyby"/>
			<result property="modifydate" column="modifydate"/>
		</association>
	</resultMap>
```

这里是简单的映射了一个Java对象，表示的是一对一关系，其中需要注意的是`javaType`是Java类的指定，这里必须填写全限定类名，使

##### namespace：

该属性是指定实体类全限定类名。用别名会报错。

### result元素

##### 字段中属性的作用：

###### property：

该属性是指定实体类中的属性。

###### column：

该属性是指定数据库的字段名。

```xml
		<id property="id" column="id"/>
		<result property="id" column="id"/>
		<result property="billcode" column="billcode"/>
```



### constructor元素

**当使用了该元素就不必在添加result元素。**

**该元素的作用是通过构造函数来在类初始化的时候注入属性的值，这样做的好处是不用暴露出共有方法。**

<font color="#F00">**当该元素指定的类中的属性，有继承关系存在时，在指定类的有参构造函数中，必须要调用父类的有参构造函数，否则就会爆出参数错误**</font>

###### idArg：

指定id，ID 参数；标记出作为 ID 的结果可以帮助提高整体性能

###### arg：

将被注入到构造方法的一个普通结果

```xml
	<resultMap type="user" id="_User">
		<constructor>
			<idArg name="id" column="id" javaType="int" />
			<arg name="sum_id" column="sum_id" javaType="int" />
			<arg name="user_code" column="user_code" javaType="String" />
			<arg name="username" column="username" javaType="String" />
			<arg name="userpassword" column="userpassword" javaType="String" />
			<arg name="gender" column="gender" javaType="int" />
			<arg name="birthday" column="birthday" javaType="String" />
		</constructor>
	</resultMap> 
```



### Association元素

**该元素用于映射数据库一对一关系，**

****

#### 在select元素中使用resultMap：

如果要使用resultMap我们就需要在select元素中声明resultMap属性：

```xml
 	<select id="findBillAndProvider" resultMap="Bill_t">
		SELECT b.billcode,b.porductname,p.porname,b.totalprice,b.creationdate FROM bill AS b JOIN provider AS p ON b.porductname LIKE '%${name}%' AND b.providerId=p.id
	</select> 
```

这样当我们调用该元素的时候就会使用我们配置好的resultMap了。

##### 执行结果

```
*********开始*********
Opening JDBC Connection
Created connection 1973256691.
Setting autocommit to false on JDBC Connection [com.mysql.cj.jdbc.ConnectionImpl@759d81f3]
==>  Preparing: SELECT b.billcode,b.porductname,p.porname,b.totalprice,b.creationdate FROM bill AS b JOIN provider AS p ON b.porductname LIKE '%键盘%' AND b.providerId=p.id
==> Parameters: 
<==    Columns: billcode, porductname, porname, totalprice, creationdate
<==        Row: 213, 惠普背光124键键盘, lzy, 20000, 2022-05-06 21:14:31
<==      Total: 1
Bill [id=null, billcode=213, porductname=惠普背光124键键盘, porductunit=null, productcount=null, totalprice=20000, ispayment=null, createdby=null, creationdate=2022-05-06 21:14:31, modifyby=null, modifydate=null, providerId=null, provider=Provider [id=null, porcode=null, porname=lzy, porcontact=null, porphone=null, poraddress=null, profax=null, createby=null, creationdate=2022-05-06 21:14:31, modifyby=null, modifydate=null]]
*********结束*********
```

可以看到这里成功的返回了一个Bill订单对象，我们可以用该对象中的信息，来做我们想要的操作了。

****

### Collection元素

**该元素用于映射数据库一对多关系**

#### 具体使用方式

想要使用collection来进行一对多的映射关系，首先要在对应表的实体类里面添加一个需要被映射关系的实体类且类型为集合的属性。

**实体类：**

```java
public class Role extends POJOBase{
	private Integer Id;
	private String rolecode;
	private String rolename;
	private Integer creatby;
	private String creationdate;
	private Integer modifyby;
	private String modifydate;
	private Integer status;
	
	private List<User> user;
}
```

**数据库结构：**

![image-20220520103742144](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220520103742144.png)

*这里可以看到，数据库中是没有user字段的，确实因为mybatis对于一对多关系，是通过我们自己来定义的，这里在数据库中也没有设置主外键关系，我们主要通过mybatis和sql语句来进行一对多的映射。*

**mapper文件：**

```xml
	<!-- 该resultMap用来映射role表和user表的一对多关系 -->
	<resultMap type="role" id="Role_User">
		<id property="Id" column="id"/>
		<result property="rolecode" column="rolecode"/>
		<result property="creatby" column="creatby"/>
		<result property="creationdate" column="creationdate"/>
		<result property="modifyby" column="modifyby"/>
		<result property="modifydate" column="modifydate"/>
		<collection property="user" javaType="ArrayList" ofType="com.dao.pojo.user.User">
			<id property="id" column="id" javaType="int"/>
			<result property="sum_id" column="sum_id" javaType="int"/>
			<result property="user_code" column="user_code" javaType="String"/>
			<result property="username" column="username" javaType="String"/>
			<result property="userpassword" column="userpassword" javaType="String"/>
			<result property="gender" column="gender" javaType="int"/>
			<result property="birthday" column="birthday" javaType="String"/>
			<result property="phone" column="phone" javaType="String"/>
			<result property="address" column="address" javaType="String"/>
			<!-- <result property="userrole" column="userrole" javaType="int"/> -->
			<result property="createby" column="createby" javaType="int"/>
			<result property="creationdate" column="creationdate" javaType="String"/>
			<result property="modifyby" column="modifyby" javaType="int"/>
			<result property="modifydate" column="modifydate" javaType="String"/>
			<result property="status" column="status" javaType="int"/>
		</collection>
	</resultMap>
```

###### property：

该属性是指定实体类中的属性。

###### javaType：

该属性是指定返回对象的类型，这里返回的是集合。**当然这里也可以填写返回的类型，mybatis回自动进行转换，将对象放入集合中，所以，即使不写该属性，也是成立的**

###### ofType：

用来指定集合中的数据类型，它用来将 JavaBean（或字段）属性的类型和集合存储的类型区分开来。

**`<collection property="user" javaType="ArrayList" ofType="com.dao.pojo.user.User">`读作：**

user是一个存储com.dao.pojo.user.User的ArrayList集合

###### 在select元素中使用resultMap：

```xml
	<!-- 通过id查询role信息和所有对应的user信息 -->
	<select id="findRoleAndUserByid" resultMap="Role_User">
		SELECT r.*,u.username,u.user_code,u.gender,u.phone,u.address
		FROM role r,user u
		
		WHERE r.status != 1 
		AND u.userrole = r.id
	</select>
```

###### 执行结果

```java
[
	Id=1, 
	rolecode=1234, 
	rolename=普通员工, 
	creatby=1, 
	creationdate=2022-05-05 15:22:36, 
	modifyby=null, 
	modifydate=null, 
	status=null, 
	user=[
		User [
			id=null, 
			sum_id=null, 
			user_code=lzy123as, 
			username=123, 
			userpassword=null, 
			gender=1, 
			birthday=null, 
			phone=15538902565, 
			address=商洛, 
			userrole=null, 
			createby=null, 
			creationdate=null, 
			modifyby=null, 
			modifydate=null
		], User [
			id=null, 
			sum_id=null, 
			user_code=lzy666, 
			username=lzy, 
			userpassword=null, 
			gender=1, 
			birthday=null,
       		phone=15165346874651, 
       		address=云南, 
        	userrole=null, 
        	createby=null, 
        	creationdate=null, 
        	modifyby=null, 
        	modifydate=null
        ], User [
        	id=null, 
        	sum_id=null, 
        	user_code=123123, 
        	username=zhangsan, 
        	userpassword=null,
          	gender=1, 
          	birthday=null, 
          	phone=12312412312, 
          	address=陕西, 
          	userrole=null, 
          	createby=null, 
          	creationdate=null, 
          	modifyby=null, 
          	modifydate=null
          ]
	]
]

```

###### <font color="#F00">**注意事项**</font>

**mybatis内部是通过主键id来识别多条数据是否是重复的，如果主键相同，它就会自动帮你过滤掉相同的记录，映射成一个一对多的实体，但如果你没有查询主键，那么mybatis就会视为你的所有数据都是不重复的，因此映射成多个一对多的实体，这个时候就会爆出`Expected one result (or null) to be returned by selectOne()，but found:`错误**

这个时候我们只需要通过指定mybatis的id字段就可以解决该问题了。

**报错代码：**

```xml
	<!-- 通过id查询role信息和所有对应的user信息 -->
	<select id="findRoleAndUserByid" resultMap="Role_User">
		SELECT 		r.rolecode,r.rolename,r.creatby,r.creationdate,u.username,
        			u.user_code,u.gender,u.phone,u.address
		FROM role r,user u
		
		WHERE r.status != 1 
		AND u.userrole = #{id}
	</select>
```

**修改后：**

```xml
	<!-- 通过id查询role信息和所有对应的user信息 -->
	<select id="findRoleAndUserByid" resultMap="Role_User">
		SELECT 		r.id,r.rolecode,r.rolename,r.creatby,r.creationdate,u.username,
					u.user_code,u.gender,u.phone,u.address
		FROM role r,user u
		
		WHERE r.status != 1 
		AND u.userrole = #{id}
	</select>
```

这里的sql加上了配置了主键信息的字段之后，就不会报错了。
