# Thymeleaf使用
使用Thymeleaf需要在html头部进行引入并声明命名空间

[Thymeleaf常规使用技巧](https://www.jianshu.com/p/d3e0b003aa34)
>xmlns:th="http://www.thymeleaf.org

```
  <html lang="en" xmlns:th="http://www.thymeleaf.org">
```

只有声明Themeleaf命名空间之后才可以正常使用。


## Thymeleaf语法规则

- **表达式语法：**

  - 变量表达式：${...}

      使用 ${} 包裹的表达式被称为变量表达式，该表达式可以获取对象的属性和方法 `${person.lastName}`，使用内置的基本对象，使用内置的工具对象。


  - 选择变量表达式：*{...}
  - 链接表达式：@{...}
  - 国际化表达式：#{...}
  - 片段引用表达式：~{...}

## 引入外部css文件

```
<link href="../static/nav.css" th:href="@{nav.css}" rel="stylesheet" />
```

- **href：**   需要引入css文件的路径位置，这里使用的是相对路径。
- **th：**:href   通过Thymeleaf替换链接位置。
- **rel：**   表示引入的是css文本样式


## 引用公共页面
**公共页面内容：**
该页面在public包下
```
<div th:fragment="name" id="id">
    <span>公共页面片段</span>
</div>
```
`th:fragment`属性为这些抽取出来的公共页面片段命名。


**引入公共页面中片段的方式：**
在 Thymeleaf 中，我们可以使用以下 3 个属性，将公共页面片段引入到当前页面中。
- th:insert：将代码块片段整个插入到使用了 th:insert 属性的 HTML 标签中。
- th:replace：将代码块片段整个替换使用了 th:replace 属性的 HTML 标签中。
- th:include：将代码块片段包含的内容插入到使用了 th:include 属性的 HTML 标签中。
```
<!--th:insert 片段名引入-->
<div th:insert="commons::fragment-name"></div>
<!--th:insert id 选择器引入-->
<div th:insert="commons::#fragment-id"></div>
------------------------------------------------
<!--th:replace 片段名引入-->
<div th:replace="commons::fragment-name"></div>
<!--th:replace id 选择器引入-->
<div th:replace="commons::#fragment-id"></div>
------------------------------------------------
<!--th:include 片段名引入-->
<div th:include="commons::fragment-name"></div>
<!--th:include id 选择器引入-->
<div th:include="commons::#fragment-id"></div>
```

>引入公共页面的格式为：**路径名::#片段id**

> 以上三种方式都能以**模板名::片段名**和**模板名::选择器**的形式进行插入或覆盖
**<font color="red">需要注意，模板名必须是完整的路径名，例如`public/nav`
选择器只支持id选择器，不支持class选择器
</font>**


## SpringBoot整合Thymeleaf向前端传递数据

**传递数据分为三步：**
  1. 控制器添加model参数
  ```
  @RequestMapping("student/findall")
public String findAll(Model model,HttpSession session) {
  List<Student> list = service.findAll();

  //将后端数据发送给页面
  model.addAttribute("studentList", list);

  return "student/studentList";
}
  ```



  2. 通过addAttribute方法传递参数并命名。

  ```
   //将后端数据发送给页面
    model.addAttribute("studentList", list);
  ```


此处会传递两个参数，一个是变量名，一个是变量本身，前端可以通过变量名来调用该变量。


  3. 通过变量名来获取数据。
  ```
  <div th:each="list,listStat:${studentList}" >
    <p th:text="${list.id}">
    <p th:text="${list.name}">
</div>
  ```

  通过后端传递的变量名来获得变量本身的内容。

## 使用Thymeleaf遍历集合

```
<div th:each="list,listStat:${studentList}" >
  <p th:text="${listStat.current}"></p>
  <p th:text="${list.id}">
  <p th:text="${list.name}">
</div>

```
首先获得了后端传递过来的集合，之后通过`th:each`进行集合的遍历。

- **list:** 是当前循环中的变量名称。
- **listStat**userStat指当前循环对象状态的变量(可选，默认就是你第一步设置的对象变量名称+ Stat)
- **${studentList}:** 是当前循环的集合


>遍历集合，Map，数组的方式基本相同。


## Thymeleaf获得后端数据
获取后端数据主要依靠框架提供的Model类，通过该类将数据传输给前端，在前端由Thymeleaf以变量的形式进行接收。

1. **在元素中接收后端数据:**
    直接使用表达式式获得后端数据
    ```
    <p th:text="${token_json}"></p>
    ```

2. **在js中获取后端数据:**
    首先在script中通过`th:inline="javascript"`来声这是需要特殊处理的js脚本。
    ```
    <script type="text/javascript" th:inline="javascript">
    ```
    之后通过`[[${表达式}]]`来获取后端传来的参数。
    ```
    <script type="text/javascript" th:inline="javascript">
    	//获取token数据
    	var json = [[${token_json}]];
    	console.log(json);
    </script>
    ```

## Thymeleaf获取参数的两种方式

在需要通过Thymeleaf获得后台数据库进行字符串拼接时，使用`th`命名空间之后字符串乱码，或者不被检测。

**thymeleaf中获得变量的两种方式：**

**1. 使用`[[${变量}]]`的方式进行变量的获得：**

    ```
    <a  title="编辑">
      <i class="icon-edit icon-large" th:onclick="admin_edit('编辑学生信息','[[@{/student/goto_update?id=}+${student.id}]]','2','800','500')"></i>
      //th:onclick="admin_edit('编辑学生信息','[[@{/student/goto_update?id=}+${student.id}]]','2','800','500')"
    </a>
    ```

  浏览器中的链接：

      > \\ /student\\ /goto_update?id=4

  在浏览器中确实可以获得到我们想要的变量，也能正常的进行字符串的拼接，但是反斜杠会出现异常。*这是因为使用`[[]]` 的方式html会自动进行转义，往往转义之后的结果并不是我们需要的。* **所以我们一般使用第二种方式**


**2. 使用`[(${变量名})]`的方式进行变量的获得：**

    ```
    <a  title="编辑">
      <i class="icon-edit icon-large" th:onclick="admin_edit('编辑学生信息','[(@{/student/goto_update?id=}+${student.id})]','2','800','500')"></i>
      //th:onclick="admin_edit('编辑学生信息','[(@{/student/goto_update?id=}+${student.id})]','2','800','500')"
    </a>
    ```

  浏览器中的链接：

      /student/goto_update?id=4

  这样浏览器就不会进行自动转义的操作，我们在填的是什么，浏览器就会显示什么。

  **原因：**
      [[]]或[()]在Thymeleaf中被认为是 text inlined expressions 文本内联表达式，用于在纯文本中输出表达式值。在它们内部，我们可以使用任何类型的表达式，这些表达式在 th:text 或 th:utext 属性中也是有效的。
      注意：

      [[${}]] 对应于 th:text 即结果将被HTML转义
      [(${})] 对应于 th:utext 即结果不转义

## a链接拼接方式

代码：
```
  <a th:href="@{/student/delete_studentbyid?id=}+${student.id}"></a>
```
>通过 **@{/url?id=}+${key.value}**的方式进行连接的拼接，过程类似java字符串拼接。
需要注意的是，只有使用 **th:href**之后链接才有效果。

## th:attr属性
