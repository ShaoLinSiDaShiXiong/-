# JSON，实现前后端数据传递

**JOSON全称为：”JavaScript Object Notation“，译为”JavaScript 对象简谱“或”javaScript对象表示法”。是一种轻量级的，基于文本的，开放的数据交换格式。**

**数据交换是指，两个设备之间建立连接并互相传递数据的过程。**

****

## 什么是JSON

JSON 是一种纯字符串形式的数据，它本身不提供任何方法（函数），非常适合在网络中进行传输。JavaScript、PHP、Java、Python、C++ 等编程语言中都内置了处理 JSON 数据的方法。

JSON 是基于 JavaScript（Standard ECMA-262 3rd Edition - December 1999）的一个子集，是一种开放的、轻量级的数据交换格式，采用独立于编程语言的文本格式来存储和表示数据，易于程序员阅读与编写，同时也易于计算机解析和生成，通常用于在 Web 客户端（浏览器）与 Web 服务器端之间传递数据。

在 JSON 中，使用以下两种方式来表示数据：

- Object（对象）：键/值对（名称/值）的集合，使用花括号`{ }`定义。在每个键/值对中，以键开头，后跟一个冒号`:`，最后是值。多个键/值对之间使用逗号`,`分隔，例如`{"name":"百度","url":"http://baidu.com"}`；
- Array（数组）：值的有序集合，使用方括号`[ ]`定义，数组中每个值之间使用逗号`,`进行分隔。

**下面展示了一个简单的JSON数据：**

```json
{
    "name":"李赞洋",
    "gender":"男",
    "skill":[
        "Java",
        "HTML",
        "css",
        "JavaScript",
        "MySQL",
        "JSON",
        "Servlet"
    ]
}
```



****

## JSON的存储

JSON 数据可以存储在 .json 格式的文件中（与 .txt 格式类似，都属于纯文本文件），也可以将 JSON 数据以字符串的形式存储在数据库、Cookie、Session 中。

要使用存储好的 JSON 数据也非常简单，不同的编程语言中提供了不同的方法来检索和解析 JSON 数据，例如 JavaScript 中的 JSON.parse() 和 JSON.stringify()、PHP 中的 json_decode() 和 json_encode()。



****

## JACKSON

**Jackson的核心模块由三部分组成：**

- jackson-core：核心包。提供基于"流模式"解析的相关 API，它包括 JsonPaser 和 JsonGenerator。 Jackson 内部实现正是通过高性能的流模式 API 的 JsonGenerator 和 JsonParser 来生成和解析 json。
- jackson-annotations：注解包，提供标准注解功能。
- jackson-databind：数据保定包 提供基于"对象绑定" 解析的相关 API （ ObjectMapper ） 和"树模型" 解析的相关 API （JsonNode）；基于"对象绑定" 解析的 API 和"树模型"解析的 API 依赖基于"流模式"解析的 API。

### ObjectMapper

Jackson最常用的API就是基于“对象绑定”的ObjectMapper：

- ObjectMapper可以从字符串，流或文件中解析JSON，并创建表示已解析的JSON的Java对象。 将JSON解析为Java对象也称为从JSON反序列化Java对象。
- ObjectMapper也可以从Java对象创建JSON。 从Java对象生成JSON也称为将Java对象序列化为JSON。
- Object映射器可以将JSON解析为自定义的类的对象，也可以解析置JSON树模型的对象。

之所以称为ObjectMapper是因为它将JSON映射到Java对象（反序列化），或者将Java对象映射到JSON（序列化）。

## Java使用JACKSON
```

<!--Jackson包-->
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-core</artifactId>
  <version>2.9.0</version>
</dependency>
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-databind</artifactId>
  <version>2.9.0</version>
</dependency>
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-annotations</artifactId>
  <version>2.9.0</version>
</dependenc

```


#### ajax请求Json数据undefined
