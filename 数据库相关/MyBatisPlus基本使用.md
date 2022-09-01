# MyBatisPlus 基本使用

## 1、构建 Spring Boot 项目

依赖 jar 包：
spring-boot-starter（构建时自带的）
spring-boot-starter-test（构建时自带的）
mybatis-plus-boot-starter（自己添加--重要--必须）
mysql-connector-java（自己添加--重要--必须）
lombok（自己添加--简化开发--非必须）

2、配置 SpringBoot 数据源（DataSource）

配置位置：application.yml(/resources)

```yml
spring:
  datasource:
    driver-class-name: 驱动名
    url: 链接地址
    username: 用户名
    password: 密码
```

`application.properties`

```properties
    spring.datasource.driver-class-name: 驱动名
    spring.datasource.url: 链接地址
    spring.datasource.username: 用户名
    spring.datasource.password: 密码
```

3、构建映射实体（User 类----user 表）

@Data
public class User {
private Integer id;
private String name;
private String sex;
}

id int
name varchar(255)
sex varchar(255)

4、UserMapper 接口
注意：需要继承自 BaseMapper 接口

@Mapper
public interface UserMapper extends BaseMapper<User> {}

5、使用（在需要使用的地方，注入 UserMapper 即可）

@SpringBootTest
class SpringBootMyBatisPlusDemoTest{
@Autowired
UserMapper userMapper;

    @Test
    void contextLoads() {
        User u = userMapper.selectById(2);
        System.out.println(u);
    }

}
