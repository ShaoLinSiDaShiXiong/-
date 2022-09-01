# SrpingMVC使用


## Thymeleaf
**为了实现前后端分离，Thymeleaf是我们需要的依赖**
```
    <dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-thymeleaf</artifactId>
		</dependency>
```
当在项目中引入了该依赖，那么该项目就会自动使用检测动态页面。
使用控制器进行页面跳转的时候会自动检测`templates`目录中的内容
