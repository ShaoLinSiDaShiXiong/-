# SpringBoot使用MyBatisPlus

## 在IDEA中构建Spring项目

**首先新建项目，然后勾选spring，修改项目名和Java版本，最后导入相关jar包：**

![image-20220627102752730](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220627102752730.png)

**选择SpringBoot版本，导入需要的jar包，后边在pom中也可以导入jar包：**

![image-20220627102913382](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220627102913382.png)

之后就会自动生成SpringBoot项目了。

## 在SpringBoot中使用MyBatisPlus注意事项

### 测试类

在使用单元测试的时候首先需要注意启动类是否正常，测试类的路径是否和项目本身路径相同。

![image-20220627103233237](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220627103233237.png)

![image-20220627103243652](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220627103243652.png)

## 数据源配置文件

**数据源最基本的配置就是数据源驱动，数据源链接，用户名和密码这四项。**

这里采用了yml文件进行数据源的配置

```properties
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/test?allowPublicKeyRetrieval=true&serverTimezone=UTC&useSSL=false&useUnicode=true&characterEncoding=UTF-8
    username: root
    password: 123456

```

## MyBatis架构相关配置

如果只是使用MyBatis进行数据库操作的话，最核心的就数据库表的映射类，和mapper接口以及mapper配置文件。其实使用MyBatisPlus的原理也是一样的，只不过操作的过程不一样，使用MyBatisPlus更的方式更简洁，只需要进行表实体类的映射，不需要进行mapper接口和mapper.xml文件的书写。

**MyBatisPlus中Mapper接口的书写：**

```java
package com.example.springbootdemo;

import com.baomidou.mybatisplus.core.mapper.BaseMapper;
import com.example.springbootdemo.entity.User;
import org.apache.ibatis.annotations.Mapper;
import org.apache.ibatis.annotations.Select;

@Mapper
public interface IUserDao extends BaseMapper<User> {

    @Select("SELECT id,name,age FROM user WHERE ${column} = #{condition}")
    User findUserByCondition(String column, String condition);
}


```

*这里只用声明一个接口，然后该接口继承自BaseMapper接口，这个时候该接口就拥有了所有基本的数据库操作方法，之后在添加泛型，该泛型是需要操作的数据库表的实体类。*

**这里使用了@Mapper注解，添加该注解的意思是该接口的实现类由mybatis底层进行创建，然后交给Spring进行管理，这样我们就可以通过Spring来进行实体类的调用了。**

<font color="#F00">这里需要注意，必须使用@Mapper注解进行spring的注入，因为我们需要使用的是MyBatis提供的实现接口的类。</font>

## 使用单元测试进行代码测试

这里使用了Spring中的依赖注入，获得了接口的实现类，并通过实现类的方法来进行相关操作。

```java
package com.example.springbootdemo;

import com.example.springbootdemo.entity.User;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.boot.test.context.SpringBootTest;

import javax.annotation.Resource;

@SpringBootTest
class SpringBootDemoApplicationTests {

    @Autowired
    private IUserDao iUserDao;

    @Test
    void contextLoads() {
        User user = iUserDao.findUserByCondition("id","1");
        System.out.println(user);
    }

}

```

