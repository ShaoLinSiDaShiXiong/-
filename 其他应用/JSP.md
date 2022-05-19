# JSP

**什么是JSP：**

JSP（Java Server Pages）是一种动态网页开发技术。JSP 文件就是在传统的 HTML 文件中插入 Java 代码和 JSP 标签，后缀名为`.jsp`。

JSP 与 PHP、ASP、ASP.NET 等语言类似，都运行在服务端。通常返回给客户端的就是一个 HTML 文件，因此只要有浏览器就能查看 JSP 页面。

JSP 使用 JSP 标签在 HTML 网页中插入 Java 代码，标签通常以`<%`开头，以`%>`结束。JSP 标签有多种功能，比如访问数据库和 JavaBean 组件等，还可以在不同的网页之间传递和共享信息。

JSP 是 Servlet 的扩展，我们可以在 JSP 中使用 Servlet 的所有功能。另外，JSP 还提供了一些其他功能，例如 EL 表达式、自定义标签等。

JSP 依赖于 Servlet，用户访问 JSP 页面时，JSP 代码会被翻译成 Servlet 代码，最终，以字符串的形式向外输出 HTML 代码。所以，JSP 只是在 Servlet 的基础上做了进一步封装。

JSP 通过表单获取用户输入的数据、访问数据库或其它数据源生成动态的 Web 内容。



****

## jsp四大作用域







****



## 使用jsp脚本动作和指令



### jsp指令



****



### jsp动作



****



### jsp脚本





****



## EL表达式

[EL表达式详细教程](https://www.ktanx.com/blog/p/1084)

在jsp中要使用EL表达式首先要开启EL表达式的使用通过在page指令中添加 `<%@page isELIgnored="false" %>`指令来实现开启EL表达式的使用。

**EL表达式的语法规范：**`${表达式}`



## EL判断

#### 字符串比较

==  eq 等于
!=  ne 不等于
\>   gt  大于
<   lt  小于
\>= ge  大于等于
<= le  小于等于

**非空判断关键字 empty**

${empty String}

empyt关键字用来判断字符串是否是null或者是“ ”，只要是两者之间的任意一个都会返回true



## 标签库

### c标签库(核心标签库)

#### 转换输出特殊字符

<c:out value="${msg}">&< /c:out>



****