# Java注解(java.Annotation)

## 注解的定义

注解是我们在编程的过程中最常见到的东西，和注释不同，注解的内容是专门给程序看的。

注解是jdk5.0之后引入的，注解本身不是程序，，可以对程序做出解释，也可以被其程序读取（编译器）。

**注解的格式是以@开头以：“@注释名”的形式在代码中存在，还可以添加一些参数，例如SuppressWarnigs(value="unchecked")**

**注解可以附加在package，class，mathod，filed上面，相当于给他们添加了额外的辅助信息，我们可以通过反射机制变成实现对这些元素的访问。**

**注解是是通过反射机制编程实现对元数据的访问。**

## 内置注解

Java中有很多内置注解，内置注解就是已经被提前写好的注解，我们可以直接使用这些注解，我们最常见的就是标识方法已被重写的注解。**@Overrid**。**@Deprecated，此注解可以修饰方法，属性和类，表示不鼓励程序员使用这样的元素。**  

**@SuppressWamings()**该注解用来抑制编译时的警告信息，通过传入不同的参数来选择镇压警告的范围。

****

## 元注解

元注解的作用就是负责注解其他注解的，Java定义了4个标准的meta-annotation类型，他们被用来提供对其他annotation类型做说明。

这些类型和他们所支持的类都子啊java.lang.annotation包中找到。

- **@Target：**

  用于描述注解的使用范围，即：被描述的注解可以用在什么地方。

  @Target(ElementType.TYPE)——接口、类、枚举、注解
  @Target(ElementType.FIELD)——字段、枚举的常量
  @Target(ElementType.METHOD)——方法
  @Target(ElementType.PARAMETER)——方法参数
  @Target(ElementType.CONSTRUCTOR) ——构造函数
  @Target(ElementType.LOCAL_VARIABLE)——局部变量
  @Target(ElementType.ANNOTATION_TYPE)——注解
  @Target(ElementType.PACKAGE)——包

- **@Retention：**

  表示需要在什么级别保存该注解信息，用于描述注解的生命周期。（SOURCE < CLASS < **RUNTIME**）

- **Document:**

  说明该注解被包含在javadoc中，即在生成文档的时候显示该注解。

- **@Inherited：**

  说明子类可以继承父类中的该注解。

****

## 自定义注解

想要自定义注解，**必须要使用@interface**来自定义注解，表示自动继承了java.lang.Annotation接口。

```java
@interface MyAnnotation(){
    //自定义内容
}
```

**注解可以进行参数的定义，想要给注解定义参数，就需要在注解内设置参数类型。和参数名，格式如下：**

**参数类型+参数名() [default];**

<font color="#f00">**如果在定义注解参数的时候没有加default默认值的话，那么在使用该注解的时候必须进行参数的传入，否则就会报错。**</font>

**当参数名为value的时候，使用该注解传入参数的时候可以不用生命key的值。**

```java
@MyAnnotation("value")
```



****