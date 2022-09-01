# Spring整合Mybatis

Spring的核心是IoC，可以帮助我们生成对象，我们可以通过这点将Mybatis的代码进行整合从而达到简化的作用。

## 需要导入的jar包

```xml
   <!--数据库驱动-->
    <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.29</version>
    </dependency>

    <!--数据库链接池-->
    <!-- https://mvnrepository.com/artifact/commons-dbcp/commons-dbcp -->
    <dependency>
      <groupId>commons-dbcp</groupId>
      <artifactId>commons-dbcp</artifactId>
      <version>1.4</version>
    </dependency>

    <!--整合mybatis的spring核心jar包-->
    <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>2.0.7</version>
    </dependency>

    <!--mybatis依赖-->
    <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.5.10</version>
    </dependency>

    <!--spring核心jar包-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>5.3.21</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>5.3.21</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-beans</artifactId>
      <version>5.3.21</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-expression</artifactId>
      <version>5.3.21</version>
    </dependency>
    <!--spring JDBC依赖-->
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>5.3.21</version>
    </dependency>
```

<font color="#F00">**在IDEA中如果需要加载resource目录之外的资源文件则需要在pom.xml文件中的<build>标签中添加如下配置：**</font>

```xml
<resources>
      <resource>
        <directory>src/main/java</directory><!--所在的目录-->
        <includes><!--包括目录下的.properties,.xml文件都会扫描到-->
          <include>**/*.properties</include>
          <include>**/*.xml</include>
        </includes>
        <filtering>false</filtering>
      </resource>
    </resources>
```

## 在Spring中书写相关配置

**Spring整合Mybatis原理**

最核心的是SqlSessionTemplate类，负责管理Mybatis的sqlsession，该类在mybatis-springjar包下。

1. **dataSource：**

   导入数据库需要的数据源，这里使用了`dbcp`数据库链接池，通过spring配置文件进行对象的创建，传入需要信息数据库驱动，数据库链接，用户名和用户密码。

   ```xml
       <!--dbcp数据库连接池-->
       <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource"
             destroy-method="close">
           <!--mysql驱动，数据库链接，用户名和密码-->
           <property name="driverClassName" value="com.mysql.jdbc.Driver" />
           <property name="url" value="jdbc:mysql://localhost:3306/test?characterEncoding=utf8&amp;useSSL=false&amp;serverTimezone=UTC&amp;rewriteBatchedStatements=true&amp;allowPublicKeyRetrieval=True" />
           <property name="username" value="root" />
           <property name="password" value="123456" />
       </bean>
   ```

2. **SqlSessionFactoryBean：**

   SqlSessionFactoryBean类专门用于进行Mybatis中SqlSession所需资源的整合。最核心的是导入数据源，mybatis配置文件，xml映射文件。

   ```xml
       <!--SqlSessionFactoryBean提供sqlsession所需要的资源-->
       <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
           <!--引入数据源-->
           <property name="dataSource" ref="dataSource"/>
           <!--通过路径引入mybatis配置文件中的配置-->
           <property name="configLocation" value="classpath:mybatis-config.xml"/>
           <!--通过路径引入所有映射文件-->
           <property name="mapperLocations">
               <list>
                   <value>classpath:org/dao/**/*.xml</value>
               </list>
           </property>
       </bean>
   ```

   

3. **SqlSessionTemplate：**

   SqlSessionTemplate是核心类它主要是管理SqlSession，我们可以通过构造方法传入SqlSessionFactoryBean通过加载资源来生成sqlsession。

   ```xml
       <!--SqlSessionTemplate，管理SqlSession，整合的核心-->
       <bean id="sqlSessionTemplate" class="org.mybatis.spring.SqlSessionTemplate">
           <!--通过SqlSessionTemplate类的有参构造函数传入需要的SqlSessionFactoryBean对象-->
           <constructor-arg name="sqlSessionFactory" ref="sqlSessionFactory"/>
       </bean>
   ```

**完成以上基本配置的书写之后就需要针对数据库进行类和mapper接口的书写**

## mapper映射

**和我们普通使用mybatis不同我们需要创建mapper接口的实例**

因为需要通过spring进行管理，所以我们通过SqlSessionTemplate类来进行数据库操作，然后将SqlSessionTemplate交由spring进行管理。

```java
package org.dao.user;

import org.mybatis.spring.SqlSessionTemplate;

public class IUserMapperImpl implements IUserMapper {

    public IUserMapperImpl() {
    }

    public IUserMapperImpl(SqlSessionTemplate sqlSessionTemplate) {
        this.sqlSessionTemplate = sqlSessionTemplate;
    }

    //通过spring注入SqlSessionTemplate对象
    private SqlSessionTemplate sqlSessionTemplate;


    public void setSqlSessionTemplate(SqlSessionTemplate sqlSessionTemplate) {
        this.sqlSessionTemplate = sqlSessionTemplate;
    }

    @Override
    public Integer count() {
        //查询单个信息
        return sqlSessionTemplate.selectOne("org.dao.user.IUserMapper.count");
    }
}

```

**完成实体类之后就可以交由spring进行对象创建的管理了**