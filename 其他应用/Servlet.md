

# Servlet

**Servlet是Server Applet的简称，译作“服务器端小程序”。它是一种基于Java技术的Web组件，运行在服务器端，由Servlet容器管理，用来生成动态Web内容。**

## 动态Web内容

想要了解什么是动态Web内容，首先要知道静态Web内容指的是什么。

​	静态Web内容指的是只有页面单方面的显示信息给用户，意思就是页面没有和用户产生信息的交互，很多人会把链接的跳转，很多人可能认为是动态的，但是只是多个页面之间进行跳转并不能和用户之间产生信息的交互。

​	动态Web可以通过页面和用户产生信息的交互，比如用户在页面上输入了一串信息，这时我们的Web网页就会返回给用户需要的得到的结果。这就是动态Web。

## 认识Servlet

Servlet程序其实就是一个按照Servlet规范编写的Java类。它具有平台独立性，可以被编译成字节码，移植到任何支持jacaranda技术的服务器运行。

*换句话说，就是Servlet可以使用所有的Java API，Java能做的所有事情，Servlet都能做。*

Java 是一种功能强大的通用型编程语言，可以处理 HTTP 请求，可以访问数据库，可以生成 HTML 代码，您完全可以使用原生 Java 来开发动态网站。但是，使用原生 Java 开发动态网站非常麻烦，需要自己解析 HTTP 请求的报头，需要自己分析用户的请求参数，需要自己加载数据库组件……种种原因导致使用原生 Java 开发动态网站几乎是一件不能被接受的事情。正是基于这种原因，Java 官方后来推出了 Servlet 技术，它对开发动态网站需要使用的原生 Java API 进行了封装，形成了一套新的 API，称为 Servlet API。

可以这样理解，Servlet 是 Sun 公司推出的一种基于 Java 的动态网站开发技术。编写 Servlet 代码需要遵循 Java 语法，一个 Servlet 程序其实就是一个按照 Servlet 规范编写的 Java 类。Servlet 程序需要先编译成字节码文件（`.class`文件），然后再部署到服务器运行。

**严格来说，Servlet 只是一套 Java Web 开发的规范，或者说是一套 Java Web 开发的技术标准。**

<font color="#900">**Servlet是一套JavaWeb开发的规范，或者说是一套JavaWev开发的技术标准。Servlet 规范是开放的，除了 Sun 公司，其它公司也可以实现 Servlet 规范，目前常见的实现了 Servlet 规范的产品包括 Tomcat、Weblogic、Jetty、Jboss、WebSphere 等，它们都被称为“Servlet 容器”。Servlet 容器用来管理程序员编写的 Servlet 类。**</font>

## Eclipse使用Servlet

在Eclipse中使用Servlet需要下载TomCat，tomcat包含了servlet，所以我们在Eclipse中使用Servlet需要导入Tomcat的依赖。

### Eclipse配置Tomcat

![image-20220317163538137](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220317163538137.png)

在Window选项中找到Preferences

![image-20220317163702031](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220317163702031.png)

在Server目录下找到Runtime Environments，进入点击add添加

![image-20220317163721774](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220317163721774.png)

这里选择安装号的Tomcat的版本，因为Tomcat是Apache下的软件，所以在Apache文件下寻找。

![image-20220317163747814](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220317163747814.png)

这一步在电脑上找到下载好的Tomcat位置，之后点FInish。最后保存并应用即可

### Eclipse使用Servlet进行动态网站开发

![image-20220317165125273](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220317165125273.png)

首先新建一个动态Web项目

![image-20220317165501465](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220317165501465.png)

之后选择自己Tomcat的版本，和动态Web模块的版本（这边选择5）。

![image-20220317165642086](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220317165642086.png)

之后删除掉项目本身自带的web.xml文件，因为这个自带的版本比较低，所以需要从新下载。

![image-20220317165748999](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220317165748999.png)

在项目文件上右键点击Java EE Tools 在点击Generate Deployment Descriptor Stub就可以生成新的web.xml文件了。

### web.xml文件的配置

![image-20220317170617800](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220317170617800.png)

这里可以看到web文件本身自带的配置，<welcom_file>标签中的内容就是运行项目之后自动打开的文件名。**这些都可以进行修改**

### 配置Servlet

**配置Servlet有两种方式，第一种是在web.xml文件中进行Servlet的配置，第二种就是通过@WebServlet注释进行配置**



#### **通过XML文件进行Servlet配置：**

```xml

<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" version="4.0">
  <display-name>Demo</display-name>
  <welcome-file-list>
      <!--这里声明开启项目时打开的默认页面-->
    <welcome-file>index.html</welcome-file>
  </welcome-file-list>
    
    <!--这里是通过context-param来设置全局参数，在这里设置的全局参数可以被context类检测到，所有的Servlet都可以调用-->
    <context-param>
    	<context-name>name</context-name>
        <context-value>Demo</context-value>
    </context-param>
    
  <servlet>
        <!-- servlet的内部名称，叫什么都可以。尽量有意义 -->
  	<servlet-name>MyServlet</servlet-name>
      <!-- servlet的类全名（全限定类名）： 包名+简单类名 -->
  	<servlet-class>MyServlet</servlet-class>
      <!--这里声明的是局部的参数，此参数只能在该servlet中被调用-->
      <init-param>
      	<param-name>name</param-name>
        <param-value>Myservlet1</param-value>
      </init-param>
      <!--此标签表示该servlet被初始化的先后顺序，小于0，只有被调用的时候才会被初始化，大于等于0时会在项目启动的时候被调用，数字越小，优先级越高。-->
      <load-on-startup>1</load-on-startup>
  </servlet>

  <servlet-mapping>
      <!-- servlet的内部名称，一定要和上面的内部名称保持一致！！ -->
 	 <servlet-name>MyServlet</servlet-name>
      <!--访问路径  http://localhost:8080/a-->
        <!--这里和@Webservlet路径一个道理 -->
 	 <url-pattern>/a</url-pattern>
  </servlet-mapping>
    <!--设置sission的过期时间-->
    <session-config>
    	<session-timeout>10</session-timeout>
    </session-config>
</web-app>
```

这里的配置分为三个部分，第一个部分是**“servlet”**标签的内容，这里面的内容是Servlet的配置<font  color="#900">一个servlet标签对应一个servlet，即不可以在一个servlet标签内指向多个servlet</font>，第二个部分是**”servlet -mapping“**标签。这里面的内容是Servlet的映射配置。

<font color="#900">需要注意的是，映射路径一定要带上**“/”**,否则就会出错。</font>

- **<context-parm>:全局参数**

  设置好的全局参数会被保存到ServletContext类中所有Servlet都可以调用。该标签内包含两个标签，一个是<param-name>该标签指定参数值的名字</param-name>

  <parame-value>该标签指定参数值</param-value>

- **<inti-param>:局部参数**

  该标签用来设置局部参数，此标签只能在<servlet>标签内声明，局部变量只能在该servlet内被使用。
  
- <session-fconfid>:**session配置：**

  其中<session-timeout>元素用来指定session的过期时间，以**分钟**为单位，该元素值必须为整数，呀v你素质为零或负数时，表示Session永远不会过期。

****

#### **@WebServlet：**

![image-20220317173115645](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220317173115645.png)

在注释后面的括号内可以对Servlet进行一些配置，其中urlPatterns后面跟的就是映射路径。

<font color="#900">使用注释进行Servlet的配置时，需要导入**jakarta.servlet.annotation.WebServlet**包否则就不会运行。</font>



****

## Servlet类

![](C:\Users\SaoLinSiDaShiXiong\Pictures\笔记图片\R-C.png)

所有的Servlet功能都是通过名为Servlet的接口向外暴露的，可以通过直接实现Servlet接口来完成Servlet规范，直接实现 Servlet 接口比较麻烦，需要实现很多方法，所以 Servlet 规范又提供了两个抽象类，分别是 GenericServlet 类和 HttpServlet 类，它们都实现了 Servlet 接口的很多常用功能。

### Servlet接口

javax.servlet.Servlet是Servlet API的核心接口，所有的Servlet接口都直接或间接的实现了这一接口

**Serrvlet方法介绍：**

| 返回值        | 方法                                            | 备注                                                         |
| ------------- | ----------------------------------------------- | ------------------------------------------------------------ |
| void          | init(ServletConfig config)                      | Servlet实例化之后，由Servlet容器调用，用来初始化Servlet对象。该方法只能被调用一次，参数config用来向Servlet传递配置信息。 |
| void          | service(ServletRequst req,ServletResponse  res) | Servlet容器调用该方法处理客户端请求。                        |
| void          | destroy()                                       | 服务器关闭，重启或者Servlet对象被移除时，由Servlet容器嗲用，负责释放Servlet独享占用的资源。 |
| ServletConfig | getServlsetConfig()                             | 该方法用来获取SevletConfig对象，该对象中包含了Servlet的初始化参数。 |
| String        | getServletInfo()                                | 该方法用于获取Servlet的信息，例如作者，版本，版权等。        |

```java
package net.biancheng.www;
import javax.servlet.*;
import java.io.IOException;
import java.io.PrintWriter;
public class MyServlet implements Servlet {
    //Servlet 实例被创建后，调用 init() 方法进行初始化，该方法只能被调用一次
    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
    }
    //返回 ServletConfig 对象，该对象包含了 Servlet 的初始化参数
    @Override
    public ServletConfig getServletConfig() {
        return null;
    }
    //每次请求，都会调用一次 service() 方法
    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        //设置字符集
        servletResponse.setContentType("text/html;charset=UTF-8");
        //使用PrintWriter.write()方法向前台页面输出内容
        PrintWriter writer = servletResponse.getWriter();
        writer.write("编程帮欢迎您的到来，网址: www.biancheng.net");
        writer.close();
    }
    //返回关于 Servlet 的信息，例如作者、版本、版权等
    @Override
    public String getServletInfo() {
        return null;
    }
    //Servelet 被销毁时调用
    @Override
    public void destroy() {
    }
}
```



### GenericServlet抽象类

javax.servlet.GenericServlet 实现了 Servlet 接口，并提供了除 service() 方法以外的其他四个方法的简单实现。通过继承 GenericServlet 类创建 Servlet ，只需要重写 service() 方法即可，大大减少了创建 Servlet 的工作量。

**GenericServlet类还提供了一下方法：**

| 返回值                | 方法                             | 备注                                                         |
| --------------------- | -------------------------------- | ------------------------------------------------------------ |
| String                | **getIntParameter(String name)** | 返回名字为name的初始化参数的值，初始化参数在web.xml中进行配置。如果参数不存在，则返回null。 |
| Enumeration< String > | **getInitParameterNames()**      | 返回Servlet所有初始化参数的名字的美剧集合，若Servlet没有初始化参数，返回一个空的枚举集合。 |
| ServletContext        | **getServletContext()**          | 返回Servlet上下文对象的引用。                                |
| String                | **getServletName()**             | 返回此Servlet实例的名称。                                    |

```java
package net.biancheng.www;
import javax.servlet.*;
import java.io.IOException;
import java.io.PrintWriter;
public class MyServlet extends GenericServlet {
    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        //设置字符集
        servletResponse.setContentType("text/html;charset=UTF-8");
        //使用PrintWriter.write()方法向前台页面输出内容
        PrintWriter writer = servletResponse.getWriter();
        writer.write("编程帮欢迎您的到来，网址: www.biancheng.net");
        writer.close();
    }
}
```

### HttpServlet 抽象类

一般情况下，浏览器（客户端）通过 HTTP 协议来访问服务器的资源，Servlet 主要用来处理 HTTP 请求。

Servlet 处理 HTTP 请求的流程如下：![](C:\Users\SaoLinSiDaShiXiong\Pictures\笔记图片\HttpServeltRequest.png)

1. Servlet 容器接收到来自客户端的 HTTP 请求后，容器会针对该请求分别创建一个 HttpServletRequest 对象和 HttpServletReponse 对象。
2. 容器将 HttpServletRequest 对象和 HttpServletReponse 对象以参数的形式传入 service() 方法内，并调用该方法。
3. 在 service() 方法中 Servlet 通过 HttpServletRequest 对象获取客户端信息以及请求的相关信息。
4. 对 HTTP 请求进行处理。
5. 请求处理完成后，将响应信息封装到 HttpServletReponse 对象中。
6. Servlet 容器将响应信息返回给客户端。
7. 当 Servlet 容器将响应信息返回给客户端后，HttpServletRequest 对象和 HttpServletReponse 对象被销毁。



javax.servlet.http.HttpServlet 继承了 GenericServlet 抽象类，用于开发基于 HTTP 协议的 Servlet 程序。由于 Servlet 主要用来处理 HTTP 的请求和响应，所以通常情况下，编写的 Servlet 类都继承自 HttpServlet。

在 HTTP/1.1 协议中共定义了 7 种请求方式，即 GET、POST、HEAD、PUT、DELETE、TRACE 和 OPTIONS。

HttpServlet 针对这 7 种请求方式分别定义了 7 种方法，即 doGet()、doPost()、doHead()、doPut()、doDelete()、doTrace() 和 doOptions()。

HttpServlet 重写了 service() 方法，该方法会先获取客户端的请求方式，然后根据请求方式调用对应 doXxx 方法。





**HttpServletRequst对象的数据处理方法有：**

| 返回值      | 方法                          | 备注                                 |
| ----------- | ----------------------------- | ------------------------------------ |
| String      | **getParameter(String name)** | 返回由name指定的用户请求参数的值     |
| String[]    | **getParameterValues()**      | 返回由name指定的一组用户请求参数的值 |
| Enumeration | **getparmater()**             | 返回所有客户请求的参数               |



```java
package net.biancheng.www;
import javax.servlet.*;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
public class MyServlet extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //使用PrintWriter.write()方法向前台页面输出内容
        resp.setContentType("text/html;charset=UTF-8");
        PrintWriter writer = resp.getWriter();
        writer.write("编程帮欢迎您的到来，网址: www.biancheng.net");
        writer.close();
    }
    public void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //使用PrintWriter.write()方法gaifang向前台页面输出内容
        PrintWriter writer = resp.getWriter();
        writer.write("编程帮欢迎您的到来，网址: www.biancheng.net");
        writer.close();
        doGet(req, resp);
    }
}
```

#### HttpServletRequest接口详解

在 Servlet API 中，定义了一个 HttpServletRequest 接口，它继承自 ServletRequest 接口。HttpServletRequest 对象专门用于封装 HTTP 请求消息，简称 request 对象。

**HTTP 请求消息分为请求行、请求消息头和请求消息体三部分，所以 HttpServletRequest 接口中定义了获取请求行、请求头和请求消息体的相关方法。**

HTTP 请求的请求行中包含请求方法、请求资源名、请求路径等信息.

HttpServletRequest 接口定义了一系列获取请求行信息的方法，如下表:

#### 获取请求行信息:

| 返回值类型 | 方法声明         | 描述                                                         |
| ---------- | ---------------- | ------------------------------------------------------------ |
| String     | getMethod()      | 该方法用于获取 HTTP 请求方式（如 GET、POST 等）。            |
| String     | getRequestURI()  | 该方法用于获取请求行中的资源名称部分，即位于 URL 的主机和端口之后，参数部分之前的部分。 |
| String     | getQueryString() | 该方法用于获取请求行中的参数部分，也就是 URL 中“?”以后的所有内容。 |
| String     | getContextPath() | 返回当前 Servlet 所在的应用的名字（上下文）。对于默认（ROOT）上下文中的 Servlet，此方法返回空字符串""。 |
| String     | getServletPath() | 该方法用于获取 Servlet 所映射的路径。                        |
| String     | getRemoteAddr()  | 该方法用于获取客户端的 IP 地址。                             |
| String     | getRemoteHost()  | 该方法用于获取客户端的完整主机名，如果无法解析出客户机的完整主机名，则该方法将会返回客户端的 IP 地址。 |

#### 获取请求头信息

当浏览器发送请求时，需要通过请求头向服务器传递一些附加信息，例如客户端可以接收的数据类型、压缩方式、语言等。为了获取请求头中的信息， HttpServletRequest 接口定义了一系列用于获取 HTTP 请求头字段的方法，如下表所示。



| 返回值类型  | 方法声明                | 描述                                                         |
| ----------- | ----------------------- | ------------------------------------------------------------ |
| String      | getHeader(String name)  | 该方法用于获取一个指定头字段的值。 如果请求消息中包含多个指定名称的头字段，则该方法返回其中第一个头字段的值。 |
| Enumeration | getHeaders(String name) | 该方法返回指定头字段的所有值的枚举集合， 在多数情况下，一个头字段名在请求消息中只出现一次，但有时可能会出现多次。 |
| Enumeration | getHeaderNames()        | 该方法返回请求头中所有头字段的枚举集合。                     |
| String      | getContentType()        | 该方法用于获取 Content-Type 头字段的值。                     |
| int         | getContentLength()      | 该方法用于获取 Content-Length 头字段的值 。                  |
| String      | getCharacterEncoding()  | 该方法用于返回请求消息的字符集编码 。                        |



#### 获取 form 表单的数据

在实际开发中，我们经常需要获取用户提交的表单数据，例如用户名和密码等。为了方便获取表单中的请求参数，ServletRequest 定义了一系列获取请求参数的方法，如下表所示。



| 返回值类型  | 方法声明                         | 功能描述                                                     |
| ----------- | -------------------------------- | ------------------------------------------------------------ |
| String      | getParameter(String name)        | 返回指定参数名的参数值。                                     |
| String [ ]  | getParameterValues (String name) | 以字符串数组的形式返回指定参数名的所有参数值（HTTP 请求中可以有多个相同参数名的参数）。 |
| Enumeration | getParameterNames()              | 以枚举集合的形式返回请求中所有参数名。                       |
| Map         | getParameterMap()                | 用于将请求中的所有参数名和参数值装入一个 Map 对象中返回。    |



****

## Servlet容器（Web容器）

### Web服务器

Web 服务器是一种对外提供 Web 服务的软件，它可以接收浏览器的 HTTP 请求，并将处理结果返回给浏览器。

我们通常所说的 Web 服务器，比如 Apache、Nginx、IIS 等，它们的功能往往都比较单一，只能提供 http(s) 服务，让用户访问静态资源（HTML 文档、图片、CSS 文件、JavaScript 文件等），它们不能执行任何编程语言，也不能访问数据库，更不能让用户注册和登录。

也就是说，如果只有Web网站那么你只能访问静态网站，不能部署动态网站。**要想部署动态网站，必须要有编程语言运行环境（运行时，Runtime）的和数据库管理系统的支持。**

#### 运行环境（运行时环境）

开发网站使用的编程语言一般都是脚本语言（比如 PHP、ASP、Python），部署网站时都是将源代码直接扔到服务器上，然而源代码自己并不能运行，必须要有解释器的支持；当用户访问动态页面时，解释器负责分析、编译和执行源代码，然后得到处理结果。

部署动态网站一般至少需要三个组件，分别是 Web 服务器、脚本语言运行时和数据库，例如，部署 PHP 网站一般选择「Apache + PHP 运行时 + MySQL」的组合。****

![](C:\Users\SaoLinSiDaShiXiong\Pictures\笔记图片\135I02Q1-0.jpg)

### Web容器

Servlet 容器就是 Servlet 代码的运行环境（运行时），它除了实现 Servlet 规范定义的各种接口和类，为 Servlet 的运行提供底层支持，还需要管理由用户编写的 Servlet 类，比如实例化类（创建对象）、调用方法、销毁类等。

Servlet是基于Java语言的，运行Servlet必须要有jre的支持，然而jre只包含了Java虚拟机，Java核心类库和一些辅助性文件并不支持Servlet规范，因此想要运行Servlet代码，还需要额外的部件，该部件必须支持Servlert规范，实现了Servlet接口和一些基础类，这种不见就是Servlet容器。

常用的 Web 容器有 Tomcat、Jboss、Jetty、WebLogic 等，其中 Tomcat 由 Java 官方提供，是初学者最常使用的。

<font color="#900">**一个动态页面对应一个Servlet类，开发一个动态页面就是编写一个Servlet类，当用户亲求到达时，Servlet容器会根据配置文件web.xml来决定调用那个类。**</font>

**下面演示了Servlet容器在整个HTTP请求流程中的位置：**

![](C:\Users\SaoLinSiDaShiXiong\Pictures\笔记图片\135I031T-1.jpg)

**总结：**

Servlet容器就是Servlet程序的运行环境，他住嗨哟啊半酣以下几个功能：

- 实现Servlet规范定义的各种接口和类，为Servlet的运行提供底层支持。
- 管理用户编写Servlet类，以及实例化以后的对象。
- 提供HTTP服务，相当于一个简化的服务器。

## Servlet的三种创建方式

1. 实现javax.servlet.Servlet接口，实现其全部方法。
2. 继承javax.servlet.GenericServleta抽象类，重写servle()方法。
3. 继承javax.servlet.http.HttpServlet抽象类，重写doGet()或doPost()方法。



****

## Servlet访问路径

访问路径：http://localhost:8080/TestWeb/a1中，各部分的包含含义如下：

- http://表示HTTP协议。
- localhost：表示服务器IP、
- 8080表示的端口号。
- /TestWeb表示Webi应用的上下文路径。
- /a1表示资源路径，就是映射的URL路径，即 web.xml 中 <url-pattern> 元素的取值。。

****

## Servlet虚拟路径映射

客户端通过 URL 地址来访问 Web 服务器中的资源，Servlet 程序若想被外界访问，就必须被映射到一个 URL 地址上。很多时候，该 URL 地址和 Servlet 程序的物理路径（在硬盘上的存储位置）并不一致，因此它被称为虚拟路径。Servlet 与虚拟路径的对应关系就叫做 Servlet 虚拟路径映射。

**Servlet虚拟路径映射可以被分为两类：单一映射和多重映射。**

### Servlet单一映射

Servlet单一映射是指一个Servlet制备映射到一个虚拟路径上。

可以通过使用web.xml和使用@WebServlet来实现单一映射。

**web.xml实现单一映射:**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         id="WebApp_ID" metadata-complete="false" version="4.0">

    <servlet>
        <servlet-name>MyServlet</servlet-name>
        <servlet-class>net.biancheng.www.MyServlet</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>MyServlet</servlet-name>
        <url-pattern>/myServlet</url-pattern>
    </servlet-mapping>

</web-app>
```

标签说明:

- <servlet> 元素用于注册 Servlet，即给 Servlet 起一个独一无二的名字。
- <servlet> 包含两个主要的子元素 <servlet-name> 和 <servlet-class>，分别用于指定 Servlet 的名称和 Servlet 的完整限定名（包名+类名）。
- <servlet-mapping> 元素用于定义 Servlet 与虚拟路径之间的映射。
- <servlet-mapping> 包含两个子元素 <servlet-name> 和 <url-pattern>，分别用于指定 Servlet 的名称和虚拟路径。

**@WebServlet实现单一映射:**

```Java
package net.biancheng.www;
import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
@WebServlet("/MyServlet")
public class MyServlet extends HttpServlet {
}
```

<font color="#900">**这里注释内的映射路径可以加上urlPatterns = "/MyServlet"这两种方式能达成的效果是一样的．**</font>

****

### Servlet实现多重映射

<font color="#900">Servlet的多重映射是指一个Servlet可以被映射到多个虚拟路径上.此时客户端可以通过多个路径实现对同一个Servlet的访问.</font>

**和实现单一映射一样,实现多重映射的方法也是通过配置xml文件和使用@webServlet注解来完成的,唯一不同的是书写方式.**

Servlet 多重映射的实现方式有 3 种：

1. 配置多个 <servlet-mapping> 元素。
2. 配置多个 <url-pattern> 子元素。
3. 在 @WebServlet 的 urlPatterns 属性中使用字符串数组

#### 1. 配置多个 <servlet-mapping> 元素

Servlet 2.5 规范之前，<servlet-mapping> 元素只允许包含一个 <url-pattern> 子元素，若要实现 Servet 的多重映射，只能通过配置多个 <servlet-mapping> 元素实现。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns="http://xmlns.jcp.org/xml/ns/javaee"
    xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
    id="WebApp_ID" metadata-complete="false" version="4.0">

    <servlet>
        <servlet-name>MyServlet</servlet-name>
        <servlet-class>net.biancheng.www.MyServlet</servlet-class>
        <load-on-startup>1</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>MyServlet</servlet-name>
        <url-pattern>/myServlet</url-pattern>
    </servlet-mapping>

    <servlet-mapping>
        <servlet-name>MyServlet</servlet-name>
        <url-pattern>/myServlet2</url-pattern>
    </servlet-mapping>

</web-app>
```

#### 2. 配置多个 <url-pattern> 子元素

从 Servlet 2.5 开始，<servlet-mapping> 元素可以包含多个 <url-pattern> 子元素，每个 <url-pattern> 代表一个虚拟路径的映射规则。因此，通过在一个 <servlet-mapping> 元素中配置多个 <url-pattern> 子元素，也可以实现 Servlet 的多重映射。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns="http://xmlns.jcp.org/xml/ns/javaee"
    xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
    id="WebApp_ID" metadata-complete="false" version="4.0">

    <servlet>
        <servlet-name>MyServlet</servlet-name>
        <servlet-class>net.biancheng.www.MyServlet</servlet-class>
        <load-on-startup>1</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>MyServlet</servlet-name>
        <url-pattern>/myServlet</url-pattern>
        <url-pattern>/myServlet3</url-pattern>
    </servlet-mapping>

</web-app>
```

#### 3. @WebServlet 实现多重映射

Servlet 3.0 增加了对 @WebServlet 注解的支持，我们可以在 urlPatterns 属性中，以字符串数组的形式指定一组映射规则来实现 Servlet 的多重映射。

```JAVA
package net.biancheng.www;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebInitParam;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(
        urlPatterns = { "/myServlet", "/myServlet4" })
public class MyServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;
    private int initCount = 0;
    private int httpCount = 0;
    private int destoryCount = 0;

    @Override
    public void destroy() {
        destoryCount++;
        super.destroy();
        // 向控制台输出destory方法被调用次数
        System.out.println(
                "**********************************destroy方法：" + destoryCount + "*******************************");
    }

    @Override
    public void init() throws ServletException {
        initCount++;
        super.init();
        // 向控制台输出init方法被调用次数
        System.out.println("init方法：" + initCount);
    }

    public void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        httpCount++;
        // 控制台输出doGet方法次数
        System.out.println("doGet方法：" + httpCount);
        // 设置返回页面格式与字符集
        resp.setContentType("text/html;charset=UTF-8");
        PrintWriter writer = resp.getWriter();
        // 向页面输出
        writer.write("初始化次数:" + initCount + "<br/>" + "处理请求次数:" + httpCount + "<br/>" + "销毁次数:" + destoryCount);
        writer.close();
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
    }
}
```

****

## Servlet虚拟路径匹配规则

当 Servlet 容器接收到请求后，容器会将请求的 URL 减去当前应用的上下文路径，使用剩余的字符串作为映射 URL 与 Servelt 虚拟路径进行匹配，匹配成功后将请求交给相应的 Servlet 进行处理。

以 servletDemo 为例，若 URL 为“http://localhost:8080/servletDemo/myServlet”，其应用上下文是 servletDemo，容器会将“http://localhost:8080/servletDemo”去掉，使用剩余的“/myServlet”与 Servlet 虚拟路径进行匹配。

ervlet 虚拟路径匹配规则有以下 4 种：

1. 完全路径匹配

   以/开始不能包含通配符*   必须完全匹配.例如:**/myServlet或/user/myservlet**

   http://localhost:8080/servletDemo/myServlet
   http://localhost:8080/servletDemo/user/myServlet
   http://localhost:8080/servletDemo/product/index.action

2. 目录匹配

   以/字符开头并以/*结尾的字符串,用于路径匹配.例如:**`/user/* `**

   http://localhost:8080/servletDemo/user/aaa
   http://localhost:8080/servletDemo/aa

3. 扩展名匹配

   以通配符`*.`开头的字符串,用于扩展名匹配.例如:**`*do *action *jsp`**

   http://localhost:8080/servletDemo/user.do
   http://localhost:8080/servletDemo/myServlet.action
   http://localhost:8080/servletDemo/bb.jsp

4. 缺省匹配（默认匹配）

   映射路径为`/`表示这个servelt为当前引用的缺省Servelt或默认Servelt无法匹配到虚拟路径的请求.可以匹配任意亲求URL.

<font color="#900">Servlet虚拟路径的匹配规则优先级顺序为:**全路径匹配（精确匹配）> 目录匹配 > 扩展名匹配 > 缺省匹配（默认匹配）**</font>



## Servlet请求响应

### 连接请求请求响应

**超链接形式的数据请求语法格式：**

<font color="#900"><a href="URLdizhi" ? 参数=参数值[&参数=参数值]></font>



****

### from表单请求相应

**from表单的请求数据语法格式：**

<font color="#900"><from type="类型" name="参数” method=“请求方式默认是GET请求” enctype="application/x-www-form-urlencoded"></font>

**这里面的enctype属性不是必须的，一般form表单都会自带默认值，如果想要进行文件传递就需要更改此属性的内容。**

<font color="#900">**from表单在enctype属性缺省或取值为application/x-www-fom-urlencoded情况下，无论是Get请求类型还是Post请求类型，均通过HttpServletRequest对象来获取请求数据。**</font>

#### from表单属性及作用

- **action：**此属性填入URL映射路径，不同的映射URL路径指定不同的Servlet。
- **method：**可以不添加此属性，此属性填入请求方式，默认值是GET请求。
- **enctype：**可以不添加此属性，默认是“application/x-www-form-urlencoded”，<font color="#900">如果要进行文件传输需要更改此属性。</font>

#### input标签属性及作用

- **type：**此属性用来指定input的状态（输入元素），不一样的状态获取的方式都不一样。

  | type     | 获取方式            | 备注                                                         |
  | -------- | ------------------- | ------------------------------------------------------------ |
  | text     | getParameter()      | text类型是文本域，在浏览器的显示下是普通的输入框。           |
  | password | getParameter()      | password类型是密码字段，在浏览器的显示也是普通的输入框，和text不同的是，输入的字符会被掩饰。 |
  | radio    | getParameter()      | radio是单选按钮，radio在多个name属性一致的时候，getParameter()方法只会获得被选取的唯一一个信息。 |
  | checkbox | getParameterValue() | checkbox类型是复选框，在浏览器中显示为多个选项框，因为可以返回多个值，所以使用getParameterValue()，使用getParameter()方法不会报错，但是只会返回第一个值。 |
  | submit   | getParameter()      | submit类型是提交按钮，在浏览器显示为一个提交按钮，点击此按钮可以提交from表单中的信息。 |
  | reset    | getParameter()      | reset是重置按钮，在浏览器中显示的样子和提交按钮类似，点击此按钮可以重置form表单中的内容。 |
  | file     | IO流                | file是上传文件类型，在浏览器显示为上传文件。想要获取上传的文件需要使用IO流进行接收。<font color="#900">Servlet提供了**ServletInputStream类和BufferedReader类**专门获取文件的字节输入流和字符输入流</font> |

- **name:**此属性用来声明input标签的名字，可以通过name来获取input中的值。

- **value:**此属性用来声明input标签的属性，通过getParameter()方法来获取到的就是此属性中的值。<font color="#900">text类型的input中可以不添加此属性，text中value可以被删除掉重新输入，一般只用作与提示。</font>

  

****



## HttpServletRequest获取上传文件

#### 想要使用Servlet进行文件的上传与获取，需要注意一下几点：

- form表单的属性更改：

  **文件上传只能以POST形式接收，因为GET请求会有传递上限的限制。**<font color="#900">**enctype属性的值需要进行更改为“multipart/form-data”**</font>

- input标签的设置：

  上传文件的input标签类型为type="file",为了允许多个文件的山上传，就需要多个name属性值不同的input标签。



****

### Servlet进行文件上传的几种种方式

Servlet3.0之后可以使用@MultipatrConfig标注来辅助HttpServlet来进行文件上传的处理。使用Patr类来进行文件上传到的处理比使用ServletFileUplaod类要方便许多。

#### 使用ServletFileUpload



```java
/DownLoadjava为下载文件的Servlet类*/
package javaee.servlet;
import …………
@WebServlet("/DownLoad")
public class DownLoad extends HttpServlet{
	private static final long serialVersionUID = 1L;
	public DownLoad(){
		super();
	}
	protected void doGet(HttpServletRequest request ,HttpServletResponse response)
			throws ServletException,IOException{
		this.doPost(request, response);
	}
	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException,IOException{
		try{
			//服务器相对路径
			String filepath = "WEB-INF/web.xml";
			//服务器绝对路径
			String fullFilePath = getServletContext().getRealPath(filepath);
			System.out.println(fullFilePath);
			/*打开文件，创建File类型的文件对象*/
			File file = new File(fullFilePath);
			/*如果文件存在*/
			if(file.exists()){
				System.out.println("文件存在");
				/*获得文件名，并采用UTF-8编码方式进行编码，以解决中文问题*/
				String filename = URLEncoder.encode(file.getName(), "UTF-8");
				System.out.println(filename);
				/*重置response对象*/
				response.reset();
				//设置文件的类型，xml文件采用text/xml类型，详见MIME类型的说明
				response.setContentType("text/xml");
				//设置HTTP头信息中内容
				response.addHeader("Content-Disposition","attachment:filename=\"" + filename + "\"" );
				//设置文件的长度
				int fileLength = (int)file.length();
				System.out.println(fileLength);
				response.setContentLength(fileLength);
				/*如果文件长度大于0*/
				if(fileLength!=0){
					//创建输入流
					InputStream inStream = new FileInputStream(file);
					byte[] buf = new byte[4096];
					//创建输出流
					ServletOutputStream servletOS = response.getOutputStream();
					int readLength;
					//读取文件内容并写到response的输出流当中
					while(((readLength = inStream.read(buf))!=-1)){
						servletOS.write(buf, 0, readLength);
					}
					//关闭输入流
					inStream.close();
					//刷新输出缓冲
					servletOS.flush();
					//关闭输出流
					servletOS.close();
				}
			}else {
				System.out.println("文件不存在~！");
				PrintWriter out = response.getWriter();
				out.println("文件 \"" + fullFilePath + "\" 不存在");
			}
		}catch(Exception e){
			System.out.println(e);
		}
	}
}
```



****





#### 使用@MultPartConfig

**如果要使用Part类来进行文件的上传处理，就必须要添加@MultPartConfig**

在Servlet3.0之前，处理上传文件的操作一直是让开发者头疼的问题，因为Servlet本身没有对此提供直接的支持，需要使用第三方框架来实现，而且使用起来也不够简单。
Servlet3.0提供了对文件上传的支持，通过@MultipartConfig标注和HttpServletRequest的两个新方法getPart()和getParts()，开发者能够很容易实现文件的上传操作。
@MultipartConfig标注主要是为了辅助Servlet3.0中HttpServletRequest提供的对上传文件的支持。该标注写在Servlet类的声明之前，一表示该Servlet希望处理的请求时multipart/form-data类型的。另外，该标注还提供了若干属性用于简化对上传文件的处理。

<font color="#900">@MultipartConfig标注属性</font>

fileSizeThershold         int型				是（可选）    		 描述：当前数据量大于该值时，内容将被写入文件。

location            			 String型			是（可选）    		 描述：存放生成文件的地址

maxFileSize    	   		long型       	   是（可选） 		    描述：允许上传的文件最大值，默认为-1，表示没有限制

maxRequestSize  		long型      		是（可选）		     描述：针对 multipart/form-data 请求的最大数量，默认为-1，表示没有限制

```java

/*UpLoad.java为上传文件的Servlet类*/
package javaee.servlet;
import …………
//设置访问活着调用这个Servlet的路径
@WebServlet("/UpLoad")
//说明该Servlet处理的是multipart/form-data类型的请求
@MultipartConfig
public class UpLoad extends HttpServlet{
	private static final long serialVersionUID = 1L;
	public UpLoad(){
		super();
	}
	protected void doGet(HttpServletRequest request,HttpServletResponse response)
		throws ServletException,IOException{
		this.doPost(request, response);
	}
	protected void doPost(HttpServletRequest request,HttpServletResponse response)
			throws ServletException,IOException{
		//说明输入的请求信息采用UTF-8编码方式
		request.setCharacterEncoding("utf-8");
		response.setContentType("text/html; charset=UTF-8");
		PrintWriter out = response.getWriter();
		//Servlet3.0中新引入的方法，用来处理multipart/form-data类型编码的表单
		Part part = request.getPart("file");
		//获取HTTP头信息headerInfo=（form-data; name="file" filename="文件名"）
		String headerInfo = part.getHeader("content-disposition");
		//从HTTP头信息中获取文件名fileName=（文件名）
		String fileName = headerInfo.substring(headerInfo.lastIndexOf("=") + 2, headerInfo.length() - 1);
		//获得存储上传文件的文件夹路径
		String fileSavingFolder = this.getServletContext().getRealPath("/UpLoad");
		//获得存储上传文件的完整路径（文件夹路径+文件名）
		//文件夹位置固定，文件夹采用与上传文件的原始名字相同
		String fileSavingPath = fileSavingFolder + File.separator + fileName;
		//如果存储上传文件的文件夹不存在，则创建文件夹
		File f = new File(fileSavingFolder + File.separator);
		if(!f.exists()){
			f.mkdirs();
		}
		//将上传的文件内容写入服务器文件中
		part.write(fileSavingPath);
		//输出上传成功信息
		out.println("文件上传成功~！");
	}
}


```



****

## Servlet获取上传文件

**ServletInputStream getInputStream():**该方法用于获取上传文件的二进制输入流

```java
	protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		ServletInputStream input = req.getInputStream();
		int i = 0;
		String s = "";
		while(i != -1) {
			i = input.read();
			char c = (char) i;
			s = s+s.valueOf(c);
		}
		System.out.println(s);
    }
```

![image-20220324120228557](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220324120228557.png)**因为使用的是是字节流，所以输出中文会乱码，这里可以使用转换流，将字节流转换为字符流。**

<font color="#900">通过这种方式获得的输入流会显示整个输入流的结构</font>



**Bufferdereader getReader():**该方法用于获取上传文件的字符缓冲输入流。



****

## ServletConfig对象

<font color="#900">ServletConfig类是被GenencServlet类继承的，所以在使用HttpServlet类的时候可以直接调用他的方法。</font>

**每个Servlet容器在被初始化的时候，容器都会为Servelt创建一个ServletConfig对象，并将 ServletConfig 对象作为参数传递给 Servlet 。通过 ServletConfig 对象即可获得当前 Servlet 的初始化参数信息。**

**一个 Web 应用中可以存在多个 ServletConfig 对象，一个 Servlet 只能对应一个 ServletConfig 对象，即 Servlet 的初始化参数仅对当前 Servlet 有效。**

### ServletConfig对象的两种调用方法：

1. 通过Servlet类自带的带参init()方法

   ```java
       public void init(ServletConfig config) throws ServletException {
           //从带参init方法中，提取ServletConfig对象
           this.servletConfig = config;
       }
   ```

2. 调用GenericServlet提供的getServletConfig()方法

   ```java
   ServletConfig servletconfig = this.getSErvletConfig();
   ```

**ServletConfig接口自带方法**

| 返回值类型          | 方法                          | 功能描述                                                     |
| ------------------- | ----------------------------- | ------------------------------------------------------------ |
| String              | getInitParameter(String name) | 根据初始话参数名name，返回对应的初始化参数值。               |
| Enumeration<String> | getIntparameterNames()        | 返回Servelt所有的初始化参数名的枚举集合，如果该Servlet没有初始化参数，则返回一个空的集合。 |
| ServletCotext       | getServeltContext()           | 返回一代表当前Web应用的ServletContext对象。                  |
| String              | getServletName()              | 返回Servlet的名字，即web.xml中<servelt-name>元素的值。       |



****

## ServletContext对象

<font color="#900">ServletContext对象是提前写好的类，他被ServeltConfig类继承，所以所有的Servlet对象都可以调用他的方法。</font>

**Servlet 容器启动时，会为每个 Web 应用（webapps 下的每个目录都是一个 Web 应用）创建一个唯一的 ServletContext 对象，该对象一般被称为“Servlet 上下文”。**

**ServletContext 对象的生命周期从 Servlet 容器启动时开始，到容器关闭或应用被卸载时结束。**

**Web 应用中的所有 Servlet 共享同一个 ServletContext 对象，不同 Servlet 之间可以通过 ServletContext 对象实现数据通讯，因此 ServletContext 对象也被称为 Context 域对象。**

<font color="#900">**获得ServletConfig对象的四种方法:**</font>

#### 1. 通过 GenericServlet 提供的 getServletContext() 方法

```java 
//通过 GenericServlet的getServletContext方法获取ServletContext对象
ServletContext servletContext = this.getServletContext();
```

#### 2. 通过 ServletConfig 提供的 getServletContext() 方法

```java
//通过 ServletConfig的 getServletContext方法获取ServletContext对象
ServletContext servletContext = this.getServletConfig().getServletContext();
```

#### 3. 通过 HttpSession 提供的 getServletContext() 方法

```java
//通过 HttpSession的 getServletContext方法获取ServletContext对象
ServletContext servletContext = req.getSession().getServletContext();
```

#### 4. 通过 HttpServletRequest 提供的 getServletContext() 方法

```java
//通过 HttpServletRequest的 getServletContext方法获取ServletContext对象
ServletContext servletContext = req.getServletContext();
```

#### ServletContext的常用方法：

| 返回值类型       | 方法                                    | 描述                                                         |
| ---------------- | --------------------------------------- | ------------------------------------------------------------ |
| String           | getContextPath()                        | 返回当前Web应用的根路径（此根路径指的是以项目为标准的绝对路径，在我们自己的电脑中就是以项目名开始的相对路径） |
| String           | getServletContextName()                 | 返回web应用的名字，即<web-app>元素中的<dispaly-name>元素的值 |
| RequstDispatcher | getRquestDispatcher(String path)        | 返回一个用于向其他web组件转发请求的RequstDispatcher对象      |
| void             | setAttribute(String name,Object object) | 把一个Java对象与一个属性名绑定，并将他作为一个属性存放到ServletContext对象中。参数name为属性名，参数object为属性值。 |
| void             | removeAttribute(String name)            | 从ServletContext中移除属性名为name的属性                     |
| Object           | getAttribute(String name)               | 根据指定的属性名name，返回ServletContext中对应的属性值。     |
| Set              | getResourcePaths(String path)           | 返回一个人Set集合，该集合中包含资源目录中的子目录和文件名称。 |
| String           | getRealPath(String path)                | 返回资源文件的真实路径（文件在电脑中的绝对路径）             |
| URL              | getResource(String path)                | 返回映射到资源文件的URl对象                                  |
| InputStream      | getResourceAsStream(String path)        | 返回映射到资源文件的InputStream输入流对象。                  |



****

## 请求转发和重定向

### 请求转发

**请求转发是属于服务器行为。容器接受请求之后，Servlet会先对请求做一些预处理，然后将请求传递给其他Web资源，来完成包括生成相应在内的后续工作。**

<font color="#900">请求转发使用RequestDispatcher接口中的forward()方法来实现，该方法可以把请求转发给另外一个资源，并让该资源对此请求做出反应。**请求转发是一个Servlet将接收到的数据请求直接转发给另外一个Servlet，所以请求转发可以资源共享。进行请求转发之后页面的路径不会发生变化**</font>

*Servlet可以通过两种方式获得RequestDispatcher对象*

- 调用ServletContext的getRequesDispacher(String path)方法，参数path指定目标资源的路径，必须为绝对路径。
- 调用ServletRequest的getRequesDispatcher(String path)方法，参数怕path指定目标资源的路径，可以为绝对路径，也可为为相对路径。

`绝对路径是指以“/”开头的路径，“/”表示但钱Web应用的根目录。相对路径是指相对当前Web资源的路径，不已“/”开头。`

**RequestDispatcher接口有两个方法：**

| 返回值 | 方法                                                    | 备注                                                         |
| ------ | ------------------------------------------------------- | ------------------------------------------------------------ |
| void   | forward(ServletRequest request,ServletRespose response) | 用于将请求转发给其他资源，该方法必须在响应提交给客户端之前被调用，否则将抛出异常。 |
| void   | include(ServletRequest request,SerlvetRespose response) | 将其他资源并入到当前的请求中。                               |

<font color="#900">forward 先处理后包含</font>

<font color="#900">include 先包含后处理</font>



**请求转发的工作原理：**

![](C:\Users\SaoLinSiDaShiXiong\Pictures\笔记图片\请求转发.png)

#### 请求转发的特点：

1. 亲求转发不支持跨领域访问，只能跳转到当前引用中的资源。
2. 请求转发之后，浏览器地址栏中的URL不会发生变化，因此浏览器不知道服务器内部发生了转发行为，更无法得知转发的次数。
3. 参与请求转发的Web资源之家共享同一request对象和response对象。
4. 由于forward()方法会先清空respose缓冲区，因此只有转发到最后一个Wev资源时，生成的相应才会被发送到客户端。



****

### 重定向：

**重定向的工作原理**

![](C:\Users\SaoLinSiDaShiXiong\Pictures\笔记图片\重定向.png)

1. 用户在浏览器中输入 URL，请求访问服务器端的 Web 资源。
2. 服务器端的 Web 资源返回一个状态码为 302 的响应信息，该响应的含义为：通知浏览器再次发送请求，访问另一个 Web 资源（在响应信息中提供了另一个资源的 URL）。
3. 当浏览器接收到响应后，立即自动访问另一个指定的 Web 资源。
4. 另一 Web 资源将请求处理完成后，由容器把响应信息返回给浏览器进行展示。

#### 转发和重定向的区别

转发和重定向都能实现页面的跳转，但是两者也存在以下区别。



| 区别                                  | 转发               | 重定向             |
| ------------------------------------- | ------------------ | ------------------ |
| 浏览器地址栏 URL 是否发生改变         | 否                 | 是                 |
| 是否支持跨域跳转                      | 否                 | 是                 |
| 请求与响应的次数                      | 一次请求和一次响应 | 两次请求和两次响应 |
| 是否共享 request 对象和 response 对象 | 是                 | 否                 |
| 是否能通过 request 域对象传递数据     | 是                 | 否                 |
| 速度                                  | 相对要快           | 相对要慢           |
| 行为类型                              | 服务器行为         | 客户端行为         |

#### response.sendRedirect()

HttpServletResponse 接口中的 sendRedirect() 方法用于实现重定向。



| 返回值类型 | 方法                          | 描述                                                         |
| ---------- | ----------------------------- | ------------------------------------------------------------ |
| void       | sendRedirect(String location) | 向浏览器返回状态码为 302 的响应结果，让浏览器访问新的 URL。若指定的 URL 是相对路径，Servlet 容器会将相对路径转换为绝对路径。参数 location 表示重定向的URL。 |



****

## Session会话技术

Sessiion是一种服务端技术，因为服务器和浏览器本身并不会记住浏览的用户是谁，所以Session和Cookie技术可以帮助浏览器和服务器来记住用户是谁。

#### 会话技术：

**从打开浏览器访问某个网站，到关闭浏览器的过程，就被称之为一次会话。会话技术就是指在会话中，帮助服务器记录用户状态和数据的技术。**

- Cookie：客户端会话技术。因为Cookie是客户端的会话技术，会话产生的数据被存储到本地，这些记录和信息，可以被修改，所以安全性不是很高，现在一般都不使用。

  ![](C:\Users\SaoLinSiDaShiXiong\Pictures\笔记图片\Cookie.png)

- Session：客户端会话技术。

  ![](C:\Users\SaoLinSiDaShiXiong\Pictures\笔记图片\Session.jpg)

1. 当客户端第一次请求会话对象时，服务器会创建一个 Session 对象，并为该 Session 对象分配一个唯一的 SessionID（用来标识这个 Session 对象）；
2. 服务器将 SessionID 以 Cookie（Cookie 名称为：“JSESSIONID”，值为 SessionID 的值）的形式发送给客户端浏览器；
3. 客户端浏览器再次发送 HTTP 请求时，会将携带 SessionID 的 Cookie 随请求一起发送给服务器；
4. 服务器从请求中读取 SessionID，然后根据 SessionID 找到对应的 Session 对象。

**注意：**

- 流程中的 Cookie 是容器自动生成的，它的 maxAge 属性取值为 -1，表示仅当前浏览器有效。
- 浏览器关闭时，对应的 Session 并没有失效，但此时与此 Session 对应的 Cookie 已失效，导致浏览器无法再通过 Cookie 获取服务器端的 Session 对象。
- 同一浏览器的不同窗口共享同一 Session 对象，但不同浏览器窗口之间不能共享 Session 对象。



#### 创建Session对象：

Session对象由服务器进行创建，通过HttpServletResquset.getSession()方法可以获得HttpSession对象：

```java
HttpSession session1 = req.getSession();
HttpSession session2 = req.getSession(false);
```

<font color="#900">创建Session的时候，通过request对象来调用getSession来获得Session对象的时候，可以传入一个boolean值，</font>

#### Session常用方法：

| 返回值类型     | 方法                                 | 描述                                                         |
| -------------- | ------------------------------------ | ------------------------------------------------------------ |
| long           | getCreationTime()                    | 返回创建 Session 的时间。                                    |
| String         | getId()                              | 返回获取 Seesion 的唯一的 ID。                               |
| long           | getLastAccessedTime()                | 返回客户端上一次发送与此 Session 关联的请求的时间。          |
| int            | getMaxInactiveInterval()             | 返回在无任何操作的情况下，Session 失效的时间，以秒为单位。   |
| ServletContext | getServletContext()                  | 返回 Session 所属的 ServletContext 对象。                    |
| void           | invalidate()                         | 使 Session 失效。                                            |
| void           | setMaxInactiveInterval(int interval) | 指定在无任何操作的情况下，Session 失效的时间，以秒为单位。负数和零表示 Session 永远不会失效。 |

## Session 的生命周期

#### Session 对象创建

Session 对象在容器第一次调用 request.getSession() 方法时创建。每个用户对应一个session。

> 值得注意的是，当客户端访问的 Web 资源是 HTML，CSS，图片等静态资源时，服务器不会创建 Session 对象。

#### Session 对象销毁

Session 对象在如下 3 种情况下会被销毁：

- Session 过期；
- 调用 session.invalidate() 方法，手动销毁 Session；
- 服务器关闭或者应用被卸载。

## Session 域对象

Session 对象也是一种域对象，它可以对属性进行操作，进而实现会话中请求之间的数据通讯和数据共享。

在 javax.servlet.http.HttpSession 接口中定义了一系列操作属性的方法，如下表。



| 返回值类型  | 方法                                | 描述                                                         |
| ----------- | ----------------------------------- | ------------------------------------------------------------ |
| void        | setAttribute(String name, Object o) | 把一个 Java 对象与一个属性名绑定，并将它作为一个属性存放到 Session 对象中。 参数 name 为属性名，参数 object 为属性值。 |
| Object      | getAttribute(String name)           | 根据指定的属性名 name，返回 Session 对象中对应的属性值。     |
| void        | removeAttribute(String name)        | 从 Session 对象中移除属性名为 name 的属性。                  |
| Enumeration | getAttributeNames()                 | 用于返回 Session 对象中的所有属性名的枚举集合。              |





****

## Filter拦截

ServletFilter是Servlert过滤器，他能够对Servlet容器传给Web资源的request对象和response对象进行见擦汗和修改。

Filter 不是 Servlet，不能直接访问，它本身也不能生成 request 对象和 response 对象，它只能为 Web 资源提供以下过滤功能：

- 在 Web 资源被访问前，检查 request 对象，修改请求头和请求正文，或对请求进行预处理操作。
- 将请求传递到下一个过滤器或目标资源。
- 在 Web 资源被访问后，检查 response 对象，修改响应头和响应正文。

> 注意：过滤器并不是必须要将请求传递到下一个过滤器或目标资源，它可以自行对请求进行处理，并发送响应给客户端，也可以将请求转发或重定向到其他的 Web 资源。

## Filter 接口

与开发 Servlet 需要实现 javax.servlet.Servlet 接口类似，开发过滤器要实现 javax.servlet.Filter 接口，并提供一个公开的不带参的构造方法。在 Filter 接口中，定义了 3 个方法，如下表所示。



| 返回值类型 | 方法                                                         | 功能描述                                                     |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| void       | init (FilterConfig filterConfig)                             | 该方法用于初始化过滤器。                                     |
| void       | doFilter(ServletRequest request,SeivletResponse response, FilterChain chain) | 该方法完成实际的过滤操作，当客户端请求的 URL 与过滤器映射的 URL 匹配时，容器会先调用该方法对请求进行拦截。 参数 request 和 response 表示请求和响应对象。 参数 chain 代表当前 Filter 链对象，在该方法内部，调用 chain.doFilter() 方法，才能把请求交付给 Filter 链中的下一个 Filter 或者 Web 资源。 |
| void       | destroy()                                                    | 该方法在销毁 Filter 对象之前被调用，用于释放被 Filter 对象占用的资源。 |

### File的工作流程

![](C:\Users\SaoLinSiDaShiXiong\Pictures\笔记图片\filter运行过程.png)

1. 客户端请求访问容器内的 Web 资源。
2. Servlet 容器接收请求，并针对本次请求分别创建一个 request 对象和 response 对象。
3. 请求到达 Web 资源之前，先调用 Filter 的 doFilter() 方法，检查 request 对象，修改请求头和请求正文，或对请求进行预处理操作。
4. 在 Filter 的 doFilter() 方法内，调用 FilterChain.doFilter() 方法，将请求传递给下一个过滤器或目标资源。
5. 目标资源生成响应信息返回客户端之前，处理控制权会再次回到 Filter 的 doFilter() 方法，执行 FilterChain.doFilter() 后的语句，检查 response 对象，修改响应头和响应正文。
6. 响应信息返回客户端。

### Filter 的生命周期

Filter 的生命周期分为 3 个阶段：

1. 初始化阶段
2. 拦截和过滤阶段
3. 销毁阶段

#### 1. 初始化阶段

Servlet 容器负责加载和实例化 Filter。容器启动时，读取 web.xml 或 @WebFilter 的配置信息对所有的过滤器进行加载和实例化。

加载和实例化完成后，Servlet 容器调用 init() 方法初始化 Filter 实例。在 Filter 的生命周期内， init() 方法只执行一次。

#### 2. 拦截和过滤阶段

该阶段是 Filter 生命周期中最重要的阶段。当客户端请求访问 Web 资源时，Servlet 容器会根据 web.xml 或 @WebFilter 的过滤规则进行检查。当客户端请求的 URL 与过滤器映射匹配时，容器将该请求的 request 对象、response 对象以及 FilterChain 对象以参数的形式传递给 Filter 的 doFilter() 方法，并调用该方法对请求/响应进行拦截和过滤。

#### 3. 销毁阶段

Filter 对象创建后会驻留在内存中，直到容器关闭或应用被移除时销毁。销毁 Filter 对象之前，容器会先调用 destory() 方法，释放过滤器占用的资源。在 Filter 的生命周期内，destory() 只执行一次。



## 注册与映射 Filter

注册和映射 Filter 有 2 种方式：

1. 通过 web.xml 配置
2. 通过 @WebFilter 注解配置

#### 1. 通过web.xml配置

在 web.xml 中，通过 <filter> 及其子元素注册 Filter，代码如下。

```
<filter>    <filter-name>myFilter</filter-name>    <filter-class>net.biancheng.www.MyFilter</filter-class>    <init-param>        <param-name>name</param-name>        <param-value>编程帮</param-value>    </init-param>    <init-param>        <param-name>URL</param-name>        <param-value>www.biancheng.net</param-value>    </init-param></filter>
```


以上元素说明如下：

- <filter> 用于注册过滤器
- <filter-name> 是<filter> 元素的子元素， 用于指定过滤器的注册名，该元素的内容不能为空。
- <filter-class> 是<filter> 元素的子元素，用于指定过滤器的完整限定名（包名+类名）。
- <init-param> 是<filter> 元素的子元素，用于为过滤器指定初始化参数，它的子元素 <param-name> 指定参数的名称，<param-value> 指定参数的值。


在 web.xml 中，通过使用 <filter-mapping> 及其子元素映射 Filter，代码如下。

```
<filter-mapping>    <filter-name>myFilter</filter-name>    <url-pattern>/login</url-pattern>    <dispatcher>REQUEST</dispatcher>    <dispatcher>FORWARD</dispatcher></filter-mapping><filter-mapping>    <filter-name>myFilter</filter-name>    <servlet-name>ServletDemo</servlet-name></filter-mapping>
```


以上元素说明如下：

- <filter-mapping> 元素用于设置 Filter 负责拦截的资源。
- <filter-name> 是<filter-mapping> 元素的子元素，用于设置 Filter 的注册名，该值必须在 <filter>元素的子元素 <filter-name> 中声明过。
- <url-pattern> 是<filter-mapping> 元素的子元素，用于设置 Filter 拦截的请求路径。
- <servlet-name> 是<filter-mapping> 元素的子元素，用于设置 Filter 拦截的 Servlet 名称。
- <dispatcher> 是<filter-mapping> 元素的子元素，用于指定 Filter 拦截的资源被 Servlet 容器调用的方式，可以是 REQUEST、INCLUDE、FORWARD 和 ERROR 之一，默认 REQUEST。用户可以设置多个 <dispatcher> 子元素指定 Filter 对资源的多种调用方式进行拦截。


<dispatcher> 元素的取值及其意义：

- REQUEST：当用户直接访问页面时，容器将会调用过滤器。如果目标资源是通过 RequestDispatcher 的 include() 或 forward() 方法访问，则该过滤器就不会被调用。
- INCLUDE：如果目标资源通过 RequestDispatcher 的 include() 方法访问，则该过滤器将被调用。除此之外，该过滤器不会被调用。
- FORWARD：如果目标资源通过 RequestDispatcher 的 forward() 方法访问，则该过滤器将被调用，除此之外，该过滤器不会被调用。
- ERROR：如果目标资源通过声明式异常处理机制访问，则该过滤器将被调用。除此之外，过滤器不会被调用。

#### 2. 使用 @WebFilter 注解进行配置

@WebFilter 注解也可以对过滤器进行配置，容器在部署应用时，会根据其具体属性配置将相应的类部署为过滤器。

@WebFilter 注解具有下表给出的一些常用属性。以下所有属性均为可选属性，但 value、urlPatterns、servletNames 三者必需至少包含一个，且 value 和 urlPatterns 不能共存，如果同时指定，通常忽略 value 的取值。



| 属性名          | 类型           | 描述                                                         |
| --------------- | -------------- | ------------------------------------------------------------ |
| filterName      | String         | 指定过滤器的 name 属性，等价于 <filter-name>。               |
| urlPatterns     | String[]       | 指定过滤器的 URL 匹配模式。等价于 <url-pattern> 标签。       |
| value           | String[]       | 该属性等价于 urlPatterns 属性，但是两者不能同时使用。        |
| servletNames    | String[]       | 指定过滤器将应用于哪些 Servlet。取值是 @WebServlet 中 filterName 属性的取值，或者 web.xml 中 <servlet-name> 的取值。 |
| dispatcherTypes | DispatcherType | 指定过滤器拦截的资源被 Servlet 容器调用的方式。具体取值包括： ASYNC、ERROR、FORWARD、INCLUDE、REQUEST。 |
| initParams      | WebInitParam[] | 指定一组过滤器初始化参数，等价于 <init-param> 标签。         |
| asyncSupported  | boolean        | 声明过滤器是否支持异步操作模式，等价于 <async-supported> 标签。 |
| description     | String         | 指定过滤器的描述信息，等价于 <description> 标签。            |
| displayName     | String         | 指定过滤器的显示名，等价于 <display-name> 标签。             |



****

### FilterChain过滤器链（Servlet）

在 Web 应用中，可以部署多个 Filter，若这些 Filter 都拦截同一目标资源，则它们就组成了一个 Filter 链（也称过滤器链）。过滤器链中的每个过滤器负责特定的操作和任务，客户端的请求在这些过滤器之间传递，直到传递给目标资源。

#### FilterChain 接口

javax.servlet 包中提供了一个 FilterChain 接口，该接口由容器实现。容器将其实例对象作为参数传入 Filter 对象的 doFilter() 方法中。Filter 对象可以使用 FilterChain 对象调用链中下一个 Filter 的 doFilter() 方法，若该 Filter 是链中最后一个过滤器，则调用目标资源的 service() 方法。FilterChain 接口中只有一个方法，如下表。



| 返回值类型 | 方法                                                       | 描述                                                         |
| ---------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| void       | doFilter(ServletRequest request ,ServletResponse response) | 使用该方法可以调用过滤器链中的下一个 Filter 的 doFilter() 方法，若该 Filter 是链中最后一个过滤器，则调用目标资源的 service() 方法。 |

> 在 Filter.doFilter() 方法中调用 FilterChain.doFilter() 方法的语句前后增加某些程序代码，就可以在 Servlet 进行响应前后实现某些特殊功能，例如权限控制、过滤敏感词、设置统一编码格式等。

#### Filter 链的拦截过程

![](C:\Users\SaoLinSiDaShiXiong\Pictures\笔记图片\Filter链接.png)

请求资源时，过滤器链中的过滤器依次对请求进行处理，并将请求传递给下一个过滤器，直到最后将请求传递给目标资源。发送响应信息时，则按照相反的顺序对响应进行处理，直到将响应返回给客户端。

过滤器并不是必须要将请求传递到下一个过滤器或目标资源，它可以自行对请求进行处理，并发送响应给客户端，也可以将请求转发给其他的目标资源。

> 过滤器链中的任何一个 Filter 没有调用 FilterChain.doFilter() 方法，请求都不会到达目标资源。

## Filter 链中 Filter 的执行顺序

通过 web.xml 配置的 Filter 过滤器，执行顺序由 <filter-mapping> 标签的配置顺序决定。<filter-mapping> 靠前，则 Filter 先执行，靠后则后执行。通过修改 <filter-mapping> 的顺序便可以修改 Filter 的执行顺序。

通过 @WebFilter 注解配置的 Filter 过滤器，无法进行排序，若需要对 Filter 过滤器进行排序，建议使用 web.xml 进行配置。



****



## url重写







****

## 报错记录

### 获得context对象报错

![image-20220323101055787](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220323101055787.png)

![image-20220323101117604](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220323101117604.png)

**经过排查，出错原因应该是config对象为空，虽然context对象是公用的，但是需用通过config对象来获得context对象，所以通过init自带参数的config生成context对象就不会报错。**

![image-20220323101401357](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220323101401357.png)

![image-20220323101426580](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220323101426580.png)



****

### 中文乱码问题

<font color="#900">**其实不管是什么情况引发的乱码，都是因为字符集不一致而导致的乱码，我们可以同将字符集都设置成UTF-8(万国码)来解决这些问题。**</font>

<font color="#900">在创建html页面的时候，需要将<meta>标签的属性及逆行声明，如下：**<meta http-equir="Context-Type" content="text/html;cha rset=UTF-8">**</font>

### Request中文乱码问题

**根据请求方式的不同，请求一般可以被分为两种：GET 请求和 POST 请求。这两种请求方式都可能会产生中文乱码问题。**



##### Request接口POST请求中文乱码

乱码的原因：POST 提交的数据在请求体中，其所使用的编码格式时页面一致（即 utf-8）。request 对象接收到数据之后，会将数据放到 request 缓冲区，缓冲区的默认字符集是 ISO-8859-1（该字符集不支持中文），两者使用的字符集不一致导致乱码。

**想要解决此问题需要将resquest缓冲区的字符集手动设置为urf-8**

```java
//修改request缓冲区的字符集
requset.setCharacterEncoding("utf-8");
//获取用户名
String name = requset.getParameter("name");
```



##### Response接口GET请求中文乱码

乱码的原因：Get 请求将请求数据附加到 URL 后面作为参数，浏览器发送文字时采用的编码格式与页面编码保持一致（utf-8）。如果 Tomcat 没有设置字符集，接收 URL 时默认使用 ISO-8859-1 进行解码，ISO-8859-1 不兼容中文，无法正确解码，导致出现乱码。

> 需要注意的是，在 Tomcat 8 中已解决了 get 方式提交请求中文乱码的问题，使用 Tomcat 8 及以上版本的同学不必再考虑此问题了，如果您使用的是 Tomcat 7 或更早的版本，出现乱码问题可以使用如下的方案解决。


解决方案：解决 GET 请求中文乱码问题，有以下 3 种解决方案。

\1. 修改 tomcat/conf/server.xml 中的配置，代码如下。

```xml
<Connector port="80" protocol="HTTP/1.1"         connectionTimeout="20000"           redirectPort="8443" URIEncoding="UTF-8"/>
```

\2. 使用 URLEncoder 和 URLDecoder 进行编码和解码的操作（逆向编解码）。 

```java
//得到TOMCAT通过ISO8859-1解码的字符串
String username = request.getParameter("username");
//对字符串使用ISO8859-1进行编码，得到最初浏览器使用UTF-8编码的字符串
username = URLEncoder.encode(username, "ISO8859-1");
//将使用UTF-8编码的字符串使用UTF-8进行解码，得到正确的字符串
username = URLDecoder.decode(username, "UTF-8");
```


\3. 使用 String 的构造方法：String(byte[] bytes, String charset) ，对字节数组（bytes）按照指定的字符集（charset）进行解码，返回解码后的字符串，解决乱码问题（推荐使用）。

```java
纯文本复制
 //获取姓名
    String username = request.getParameter("username");
//使用String的构造方法解决乱码的问题
username = new String(username.getBytes("ISO-8859-1"),"UTF-8");
```

### Response中文乱码问题

response对象向页面输出时有两种方式：字节流，字符流，这两中方式输出中文都有可能会出现乱码。

#### 使用字节流输出中文

使用字节流不一定会出现乱码。

##### 乱码原因：

字节流输出中文是否出现乱码，取决于中文转成字节数组时与浏览器打开时采用的字符集是否一致。若两者保持一致，则不会出现乱码问题，若不一致就会出现乱码问题。

##### 解决方案：

将中文转成字节数组时和浏览器默认采用的字符集保持一致即可，代码如下。

```java
纯文本复制
response.setHeader("Content-Type", "text/html;charset=UTF-8");// 获取字节输出流OutputStream os = response.getOutputStream();byte[] str = "编程帮 www.biancheng.net".getBytes("UTF-8");// 输出中文os.write(str);
```



****

#### 使用字符流输出中文

使用字节流输出中文一定会出现乱码。



##### 乱码原因：

通过字符流输出的内容是存放在 response 缓冲区的，response 缓冲区的默认字符集是 ISO-8859-1，该字符集不支持中文。

##### 解决方案：

将 response 缓冲区和浏览器采用的字符集保持一致即可，有如下 2 种的方式。

第一种方式：

```java
// 设置response缓冲区的编码
response.setCharacterEncoding("UTF-8");
// 设置浏览器打开文件所采用的编码
response.setHeader("Content-Type", "text/html;charset=UTF-8");
// 输出中文
response.getWriter().write("编程帮 www.biancheng.net");
```


第二种方式：

```java
//设置html页面字符格式
response.setContentType("text/html;charset=UTF-8");
//输出中文
response.getWriter().write("编程帮 www.biancheng.net");
```

****





****

### Servlet中使用context.getResourceAsStream(String path)方法报错获取输入流报错

这里使用的Web容器是Tomcat，因为Tomcat的项目结构原因，我们想要被检测到的文件需要放到src/main/webapp/WEB-INF文件中。如果直接放到项目中，是无法被检测的

**书写格式如下**

```java
		InputStream input = context.getResourceAsStream("WEB-INF/img/luori.jpeg");
```

**项目结构如下：**

![image-20220324182919476](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220324182919476.png)







****

### 使用请求转发html页面报错

*这个html页面本身是进行拼接的，头和脚两部分都是以链接的形式获取并显示的。*

![image-20220325102912318](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220325102912318.png)

![image-20220325102925463](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220325102925463.png)

但是在使用请求转发进行页面跳转的时候，头部和脚部的html页面会显示404.但是使用重定向就不会出现这样的问题。

**这里使用的是请求转发：**

![image-20220325103536371](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220325103536371.png)

**这里使用的是重定向：**

![image-20220325103105850](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220325103105850.png)

**这里总结可能是因为请求转发和重定向，对页面的加载过程不一致所导致的。因为这里的html页面是通过拼接来加载出来的，使用亲请求转发的时候页面的链接不会发生改变，这个时候html页面就会找不到头部和脚部的页面信息，所以就会爆出404错误（页面资源获取失败）。而使用重定向的时候页面的url链接会发生改变，这个时候html页面就可以通过相对路径来找到头部和脚部的页面信息了，也就不会爆出404异常。**

<font color="#900"><iframe>标签的问题</font>



****

## EclipseTomcat端口被占用解决方法：

1. win+r 输入cmd 进入dos界面。
2. 输入netstat -ano|findstr 8080  通过此命令来查占用8080端口的进程。
3. 输入taskkill pid/12424 /f 将显示的进程号（PID，在这里是12424）结束掉。
4. 重启Tomcat

```
C:\Users\SaoLinSiDaShiXiong>netstat -aon|findstr 8080
  TCP    0.0.0.0:8080           0.0.0.0:0              LISTENING       12424
  TCP    [::]:8080              [::]:0                 LISTENING       12424
  
C:\Users\SaoLinSiDaShiXiong>taskkill/pid 12424 /F
成功: 已终止 PID 为 12424 的进程。
```

<font color="#900">**这里需要注意在/F的前面要加一个空格，不然命令不会执行成功。**</font>

[解决方案地址](https://www.somode.com/jiaocheng/3241.html)



****

## 超链接显示找到无效字符串

![image-20220407161218549](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220407161218549.png)

**在请求目标中找到无效字符。有效字符在RFC 7230和RFC 3986中定义**指的就是超链接中含有中文导致的乱码问题



这里的主要原因是因为超链接后跟的参数带有中文，就会报错。

解决方法就是通过js将get请求改为post请求

**首先添加script代码**

```javascript
 <script>
    function linkClick(linkObject) {  
    	     var formObject = document.createElement('form');  
    	      document.body.appendChild(formObject);  
    	       formObject.setAttribute('method', 'post');  
    	       var url = linkObject.href;  
    	       var uri = '';  
    	       var i = url.indexOf('?');      	               
    	      if(i == -1) {  
    	        formObject.action = url;  
    	      } else {  
    	         formObject.action = url.substring(0, i);  
    	      }      	               
    	      if( i >= 0 && url.length >= i + 1) {  
    	         uri = url.substring(i + 1, url.length);  
    	      }      	   
          var sa = uri.split('&');      
    	      for(var i = 0; i < sa.length; i++) {  
    	        var isa = sa[i].split('=');        
    	        var inputObject = document.createElement('input');  
    	        inputObject.setAttribute('type', 'hidden');  
    	        inputObject.setAttribute('name', isa[0]);  
    	        inputObject.setAttribute('value', isa[1]);  
    	        formObject.appendChild(inputObject);  
    	      }       
    	      formObject.submit();      
    	      return false;  
    	 }  
    </script>
```

**之后在向需要发送请求的超链接添加点击事件，并且调用js代码：**

```html
<a href='${pageContext.request.contextPath }/TestServlet?name=世界&id=1' onclick="return linkClick(this)">click me</a>
```

通过以上方式就可以 解决中文报错的问题了。

第二部分 超链接参数带特殊字符而报错
参数中可能包含了 |{}[],% 等一些特殊字符

修改Tomcat的server.xml文件



向server.xml 中Connector添加

relaxedPathChars="|{}[],%" relaxedQueryChars="|{}[],%"

例如：（参数里有哪些特殊字符，就加哪些）

```xml
<Connector port="80" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" 
           relaxedPathChars="|{}[],%" relaxedQueryChars="|{}[],%"
    />
```



****





## 当前响应已经调用了方法getOutputStream()

getOutputStream() has already been called for this response 当前响应已经调用了方法getOutputStream()
如果遇到这个问题，一般是将图片输出代码直接下载jsp中，而没有写在Java类中，解决办法：

session.setAttribute("random",sRand); 
g.dispose(); 
ImageIO.write(image, "JPEG", response.getOutputStream()); 

```java
session.setAttribute("random",sRand); 
g.dispose(); 
ImageIO.write(image, "JPEG", response.getOutputStream()); 

```

在上述代码下加上：

out.clear();//清除缓冲区里的数据，但不把数据写到客户端里去
out = pageContext.pushBody();// 重新得到out对象  

```java
out.clear();//清除缓冲区里的数据，但不把数据写到客户端里去
out = pageContext.pushBody();// 重新得到out对象  

```

即可



****

## eclipse导入jstl报错

在eclipse中导入jstl的jar包之后一直报错**java.lang.NoClassDefFoundError: javax/[servlet](https://so.csdn.net/so/search?q=servlet&spm=1001.2101.3001.7020)/jsp/tagext/TagLibraryValidator，**

经过多番努力后才发现是因为我用的Tomcat10.0，用的jakarta.*软件包而不是javax.*软件包，故类似下图的jstl包是用不了的，下面的包是javax，用Tomcat10.0服务器运行的话，就会显示找不到包

![img](https://img-blog.csdnimg.cn/20210511232824348.jpg)

 要用下图的包才有效

![img](https://img-blog.csdnimg.cn/20210511233142944.jpg)



或者用maven依赖：

```xml
<dependency>
    <groupId>org.glassfish.web</groupId>
    <artifactId>jakarta.servlet.jsp.jstl</artifactId>
    <version>2.0.0</version>
</dependency>
```


原文链接：https://blog.csdn.net/RonaldMH/article/details/116675297
