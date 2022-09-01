# Spring

**Spring是一门JavaEE编程领域轻量级的开源框架。**

## Spring配置文件头部

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:c="http://www.springframework.org/schema/c"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/aop https://www.springframework.org/schema/aop/spring-aop.xsd">
    
<beans>

```

这里面总共进行了beans，XMLSchema-instance，aop和c，p短命名空间的配置，每一个相关的配置都会在xsi:schemaLocation属性中进行添加相关的链接，之后会在官网进行下载。

## Spring核心jar包

```xml
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
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-aop -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>5.3.20</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
	<!--该包主要用于进行aop操作时使用JoinPoint类-->
    <dependency>
      <groupId>org.aspectj</groupId>
      <artifactId>aspectjweaver</artifactId>
      <version>1.9.1</version>
    </dependency>
```



## 通过IoC进行Bean注入

### 什么是IoC

IoC 是 Inversion of Control 的简写，译为“控制反转”，它不是一门技术，而是一种设计思想，是一个重要的面向对象编程法则，能够指导我们如何设计出松耦合、更优良的程序。

**IoC（控制反转）和DI（依赖注入Denpendency Injection）：**

他们两个都是一个东西，只是在不同的角度来解读，IoC表达的意思就是Java对象生成的控制权是掌握在Sprin的IoC容器中的，IoC会根据我们的注释，配置文件、xml了解我们对一个类的定义，当Spring启动的时候IoC会根据我们对对象的定义将这些对象管理起来，当我们需要使用某个Bean的时候，就可以直接从IoC容器中获取。

而DI表达的意思是Spring会将自己创建的对象跟据类的依赖关系注入到当前对象中。

****

**IoC底层就是一个Bean工厂**

#### BeanFactory

**该接口是Spring的内部接口，通常情况下不对开发人员提供**

BeanFactory 是 IoC 容器的基本实现，也是 Spring 提供的最简单的 IoC 容器，它提供了 IoC 容器最基本的功能，由 org.springframework.beans.factory.BeanFactory 接口定义。

BeanFactory 采用懒加载（lazy-load）机制，容器在加载配置文件时并不会立刻创建 Java 对象，只有程序中获取（使用）这个对对象时才会创建。

#### ApplicationContext

ApplicationContext 是 BeanFactory 接口的子接口，是对 BeanFactory 的扩展。ApplicationContext 在 BeanFactory 的基础上增加了许多企业级的功能，例如 AOP（面向切面编程）、国际化、事务支持等。

ApplicationContext 接口有两个常用的实现类，具体如下表。



| 实现类                          | 描述                                                         | 示例代码                                                     |
| ------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ClassPathXmlApplicationContext  | 加载类路径 ClassPath 下指定的 XML 配置文件，并完成 ApplicationContext 的实例化工作 | ApplicationContext applicationContext = new ClassPathXmlApplicationContext(String configLocation); |
| FileSystemXmlApplicationContext | 加载指定的文件系统路径中指定的 XML 配置文件，并完成 ApplicationContext 的实例化工作 | ApplicationContext applicationContext = new FileSystemXmlApplicationContext(String configLocation); |

如果是在服务器上，我们最好是使用ClassPathXmlApplicationContext来进行xml文件的加载，因为服务器上是没有绝对路径的，如果用此方法，我们只需要将xml文件放置在resource目录中，需要的时候直接通过文件名获取相应的Bean就可以了。

****

## Spring Bean的定义

由 Spring IoC 容器管理的对象称为 Bean，Bean 根据 Spring 配置文件中的信息创建。

我们可以把 Spring IoC 容器看作是一个大工厂，Bean 相当于工厂的产品。如果希望这个大工厂生产和管理 Bean，就需要告诉容器需要哪些 Bean，以哪种方式装配。

Spring 配置文件支持两种格式，即 XML 文件格式和 Properties 文件格式。相对来说使用Properities比较简单，但是有局限性，在大型项目中我们最常使用的还是XML。

**XML文件的书写规范：**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
   http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
    <bean id="mySpring" class="com.MySpring">
        <property name="value" value="Hello Spring!"/>
    </bean>
</beans>
```

在 XML 配置的<beans> 元素中可以包含多个属性或子元素，常用的属性或子元素如下表所示。IoC就是通过解读bean中的属性来创建对象的。



| 属性名称        | 描述                                                         |
| --------------- | ------------------------------------------------------------ |
| id              | Bean 的唯一标识符，Spring IoC 容器对 Bean 的配置和管理都通过该属性完成。id 的值必须以字母开始，可以使用字母、数字、下划线等符号。 |
| name            | 该属性表示 Bean 的名称，我们可以通过 name 属性为同一个 Bean 同时指定多个名称，每个名称之间用逗号或分号隔开。Spring 容器可以通过 name 属性配置和管理容器中的 Bean。 |
| class           | 该属性指定了 Bean 的具体实现类，它必须是一个完整的类名，即类的全限定名。 |
| scope           | 表示 Bean 的作用域，属性值可以为 singleton（单例）、prototype（原型）、request、session 和 global Session。默认值是 singleton。 |
| constructor-arg | <bean> 元素的子元素，我们可以通过该元素，将构造参数传入，以实现 Bean 的实例化。该元素的 index 属性指定构造参数的序号（从 0 开始），type 属性指定构造参数的类型。 |
| property        | <bean>元素的子元素，用于调用 Bean 实例中的 setter 方法对属性进行赋值，从而完成属性的注入。该元素的 name 属性用于指定 Bean 实例中相应的属性名。 |
| ref             | <property> 和 <constructor-arg> 等元素的子元索，用于指定对某个 Bean 实例的引用，即 <bean> 元素中的 id 或 name 属性。 |
| value           | <property> 和 <constractor-arg> 等元素的子元素，用于直接指定一个常量值。 |
| list            | 用于封装 List 或数组类型的属性注入。                         |
| set             | 用于封装 Set 类型的属性注入。                                |
| map             | 用于封装 Map 类型的属性注入。                                |
| entry           | <map> 元素的子元素，用于设置一个键值对。其 key 属性指定字符串类型的键值，ref 或 value 子元素指定其值。 |
| init-method     | 容器加载 Bean 时调用该方法，类似于 Servlet 中的 init() 方法  |
| destroy-method  | 容器删除 Bean 时调用该方法，类似于 Servlet 中的 destroy() 方法。该方法只在 scope=singleton 时有效 |
| lazy-init       | 懒加载，值为 true，容器在首次请求时才会创建 Bean 实例；值为 false，容器在启动时创建 Bean 实例。该方法只在 scope=singleton 时有效 |

### Spring的Bean注入

Bean注入分为两种，一种是通过set方法来对属性进行注入这个称为setter注入，还有一种是通过构造函数进行注入。

#### 构造函数注入

我们可以通过 Bean 的带参构造函数，以实现 Bean 的属性注入。

**使用构造函数注入需要注意：**

- Bena中必须包含有参构造函数
- 在xml文件中的bean元素中使用construcotr-arg子元素来对有参构造中的参数进行赋值。<font color="#f00">一个construcotr-arg元素只能指定一个参数，如果有参构造中有多个参数，那么xml中就需要有多个construcotr-arg元素。**且！IoC容器会自动寻找对应参数的有参构造，如果找不到，就视为没有有参构造函数，此时运行就会爆出错误**</font>

**代码实例如下：**

**JavaBean：**

```java
package org.example;

public class MySpring {

    //声明需要打印的数据
    private String name = null;
    private String value = null;
	//提供有参构造和无参构造
    public MySpring(String value, String name){
        this.name = name;
        this.value = value;
    }

    public MySpring(String name){
        this.name = name;
    }
    public MySpring(){

    }
    //打印输出属性
    public void print(){
        System.out.println("Hello"+this.name+value+"!");
    }

    //提供get和set

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getValue() {
        return value;
    }

    public void setValue(String value) {
        this.value = value;
    }
}

```

**xml文件：**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="mySpring" class="org.example.MySpring">
        <!--此处指定两个参数，对应Java类中的有参构造函数-->
        <constructor-arg type="java.lang.String" name="name" value="Spring"></constructor-arg>
        <constructor-arg name="value" value="!!" ></constructor-arg>
    </bean>
</beans>
```

#### setter注入

我们可以通过 Bean 的 setter 方法，将属性值注入到 Bean 的属性中。

在 Spring 实例化 Bean 的过程中，IoC 容器首先会调用默认的构造方法（无参构造方法）实例化 Bean（Java 对象），然后通过 Java 的反射机制调用这个 Bean 的 setXxx() 方法，将属性值注入到 Bean 中。

使用setter注入的注意事项和使用构造函数注入类似

- 提供一个无参构造函数，并为需要注入的属性提供setter方法
- 在xml的bean元素中使用propery子元素来进行属性的注入

**代码实例如下**

**xml：**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="mySpring" class="org.example.MySpring">
        <property name="name" value="Spring"></property>
        <property name="value" value="!!!"></property>
    </bean>
</beans>
```

#### 短命名空间注入

我们在通过构造函数或 setter 方法进行属性注入时，通常是在 <bean> 元素中嵌套 <property> 和 <constructor-arg> 元素来实现的。这种方式虽然结构清晰，但书写较繁琐。

Spring 框架提供了 2 种短命名空间，可以简化 Spring 的 XML 配置，如下表。



| 短命名空间 | 简化的 XML 配置                        | 说明                                     |
| ---------- | -------------------------------------- | ---------------------------------------- |
| p 命名空间 | <bean> 元素中嵌套的 <property> 元素    | 是 setter 方式属性注入的一种快捷实现方式 |
| c 命名空间 | <bean> 元素中嵌套的 <constructor> 元素 | 是构造函数属性注入的一种快捷实现方式     |

**我们如果要使用短命名空间，首先需要添加相应的XML约束**

**p命名空间约束：**

```xml
xmlns:p="http://www.springframework.org/schema/p"
```

**实现代码：**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

     <bean id="mySpring" class="org.example.MySpring">
        <property name="name" value="Spring"></property>
        <property name="value" value="!!!"></property>
    </bean>
    
    <bean id="app" class="org.example.App" p:value="app" p:srping-ref="mySpring"></bean>
</beans>
```

**c命名空间约束：**

```
xmlns:c="http://www.springframework.org/schema/c"
```

**实现代码：**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

     <bean id="mySpring" class="org.example.MySpring">
        <property name="name" value="Spring"></property>
        <property name="value" value="!!!"></property>
    </bean>
    
    <bean id="app" class="org.example.App" c:value="app" c:srping-ref="mySpring"></bean>
</beans>
```

**这里需要注意，如果是注入对象的话需要在属名后加上`-ref`指定该属性需要注入的是一个Java对象，且此处可以通过id来填入已经声明好的JavaBean。**

**类似的如果不是使用短命名空间注入的话，需要指定的就是`ref`属性**

****

#### 注入内部bean

**我们将定义在 <bean> 元素的 <property> 或 <constructor-arg> 元素内部的 Bean，称为“内部 Bean”。**

我们可以在配置文件中的property属性或constructor-arg属性中再次定义bean属性，这样做可以理解为在类中对一个已经声明过的对象进行赋值。

- Java类和测试方法：

  ```java
  //------------------java类
  public class Speak {
      private MySpring mySpring = null;
      private String name = null;
      private String sentence = null;
  
      public Speak(){
  
      }
  
      /**
       * 通过构造函数来进行内容赋值
       *
       * @param mySpring
       * @param name
       * @param sentence
       */
      public Speak(MySpring mySpring, String name, String sentence) {
          super();
          System.out.println("通过有参构造进行赋值，该有参赋值了所有参数");
          this.mySpring = mySpring;
          this.name = name;
          this.sentence = sentence;
      }
  
      /**
       * 通过有参构造函数来进行内容的赋值
       *
       * @param name
       * @param sentence
       */
      public Speak(String name, String sentence) {
          this.name = name;
          this.sentence = sentence;
      }
  
      public void talk(){
          if(mySpring == null){
              System.out.println(name+"说:\""+sentence+"\"");
          }else{
              mySpring.print();
              mySpring.toString();
              System.out.println(name+"说:\""+sentence+"\"");
          }
      }
  
      //书写get和set
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public String getSentence() {
          return sentence;
      }
  
      public void setSentence(String sentence) {
          this.sentence = sentence;
      }
  
      public MySpring getMySpring() {
          return mySpring;
      }
  
      public void setMySpring(MySpring mySpring) {
          this.mySpring = mySpring;
      }
  
      @Override
      public String toString() {
          return "Speak{" +
                  "mySpring=" + mySpring +
                  ", name='" + name + '\'' +
                  ", sentence='" + sentence + '\'' +
                  '}';
      }
  }
  
  
  ```

- 通过setter进行内部bean注入

  xml文件：

  ```xml
   <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
     http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
   <!--通过匿名内部注入-->
      <bean id="personZ" class="a.Person">
          <property name="name"><value>张无忌</value></property>
          <property name="tool">
              <bean class="a.Tool">
                  <property name="name"><value>乾坤大挪移</value></property>
                  <property name="role"><value>一统光明顶</value></property>
              </bean>
          </property>
      </bean>
  </beans>
  ```

  java测试代码：

  ```java
  //------------------测试方法
  public class SpeakTest {
  
      @Test
      public void testTalk() {
          //获得spring容器
          Person person = GetBeanFactory.getContext().getBean("personZ",Person.class);//这里通过
          person.print();
          System.out.println(rTalk.toString());
      }
  
  ```

  **通过构造函数进行注入**

  xml文件：

  ```xml
      <bean id="personZ2" class="a.Person">
          <constructor-arg name="name" value="张无忌"></constructor-arg>
          <constructor-arg name="tool">
              <bean class="a.Tool">
                  <constructor-arg name="name" value="九阳神功"></constructor-arg>
                  <constructor-arg name="role" value="百毒不侵"></constructor-arg>
              </bean>
          </constructor-arg>
      </bean>
  ```

  java测试代码：

  ```java
  public class PersonTest {
  
      @Test
      public void testPrint() {
          Person zwj = GetBeanFactory.getContext().getBean("personZ2", Person.class);
          zwj.print();
      }
  }
  ```

**其实使用内部类注入很简单，而且通过xml看起来也可以很好的理解其代表的意思。**

##### 注意事项：

- 不管是property元素还是constrructor-arg元素，都需要指定Java类中的类名，他们包含的bean只指定class就可以执行。
- 关于内部bean属性其实他的赋值方式和普通的没有什么区别。

#### 注入集合，数组

我们还可以在 Bean 标签下的 <property> 元素中，使用以下元素配置 Java 集合类型的属性和参数，例如 List、Set、Map 以及 Properties 等。



| 标签    | 说明                                                         |
| ------- | ------------------------------------------------------------ |
| <list>  | 用于注入 list 类型的值，允许重复                             |
| <set>   | 用于注入 set 类型的值，不允许重复                            |
| <map>   | 用于注入 key-value 的集合，其中 key 和 value 都可以是任意类型 |
| <props> | 用于注入 key-value 的集合，其中 key 和 value 都是字符串类型  |

**在使用xml进行集合和数组的注入时，在property元素中需要使用符合类型的元素，比如数组就是用array元素来进行赋值**

java类：

```java
package a;

import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.Set;

public class Array {
    private String[] school = null;
    private List<String> classRome = null;
    private Map<String, String> student = null;
    private Set<String> teacher = null;

    public Array(String[] school, List<String> classRome, Map<String, String> student, Set<String> teacher) {
        this.school = school;
        this.classRome = classRome;
        this.student = student;
        this.teacher = teacher;
    }

    public Array() {
        System.out.println("使用Array类的无参");
    }

    public String[] getSchool() {
        return school;
    }

    public void setSchool(String[] school) {
        this.school = school;
    }

    public List<String> getClassRome() {
        return classRome;
    }

    public void setClassRome(List<String> classRome) {
        this.classRome = classRome;
    }

    public Map<String, String> getStudent() {
        return student;
    }

    public void setStudent(Map<String, String> student) {
        this.student = student;
    }

    public Set<String> getTeacher() {
        return teacher;
    }

    public void setTeacher(Set<String> teacher) {
        this.teacher = teacher;
    }

    @Override
    public String toString() {
        return "Array{" +
                "school=" + Arrays.toString(school) +
                ", classRome=" + classRome +
                ", student=" + student +
                ", teacher=" + teacher +
                '}';
    }
}
```

xml：

```xml
    <bean id="array" class="a.Array">
        <property name="school">
            <array>
                <value>陕西新华</value>
                <value>重庆新华</value>
                <value>火星新华</value>
            </array>
        </property>
        <property name="classRome">
            <list>
                <value>软件2101</value>
                <value>电商2102</value>
            </list>
        </property>
        <property name="student">
            <map>
                <entry key="张三" value="男"></entry>
                <entry key="李四" value="男"></entry>

            </map>
        </property>
        <property name="teacher">
            <set>
                <value>张三丰</value>
            </set>
        </property>
    </bean>
```

#### Bean声明周期





### 通过注解进行IoC操作

我们可以通过注解来进行JavaBean的创建，他的效果和在Spring的xml配置文件中进行Bean配置是一样的。

#### 声明Bean的注解

1. **@Component：**该注解用于组件的注解
2. **@Repository：**该注解用于进行dao类的注解
3. **@Service：**该注解用进行业务层的注解
4. **@Controller：**该注解用于进行控制器的注解

| 注解        | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| @Component  | 该注解用于描述 Spring 中的 Bean，它是一个泛化的概念，仅仅表示容器中的一个组件（Bean），并且可以作用在应用的任何层次，例如 Service 层、Dao 层等。  使用时只需将该注解标注在相应类上即可。 |
| @Repository | 该注解用于将数据访问层（Dao 层）的类标识为 Spring 中的 Bean，其功能与 @Component 相同。 |
| @Service    | 该注解通常作用在业务层（Service 层），用于将业务层的类标识为 Spring 中的 Bean，其功能与 @Component 相同。 |
| @Controller | 该注解通常作用在控制层（如 Struts2 的 Action、SpringMVC 的 Controller），用于将控制层的类标识为 Spring 中的 Bean，其功能与 @Component 相同。 |

**其实这四种注解的作用都是一样的，都是用来表示该类可以通过Spring来进行生成，这样分成四个注解的原因是希望类作用的可视化。**

**当我们对我们想要通过Spring替我们生成的类添加了注解之后，只要在Spring的xml配置文件中开启组件扫描功能的代码就可以使用了。**

**XML：**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:c="http://www.springframework.org/schema/c"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:p="http://www.springframework.org/schema/p" xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/aop
       https://www.springframework.org/schema/aop/spring-aop.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context-3.2.xsd
">
    <!--开启组件扫描-->
    <context:component-scan base-package="需要通过注解生成bean对象所在包的全限定包名"/>
</beans>

```



我们可以通过以下注解将定义好 Bean 装配到其它的 Bean 中。

| 注解       | 说明                                                         |
| ---------- | ------------------------------------------------------------ |
| @Autowired | 可以应用到 Bean 的属性变量、setter 方法、非 setter 方法及构造函数等，默认按照 Bean 的类型进行装配。  @Autowired 注解默认按照 Bean 的类型进行装配，默认情况下它要求依赖对象必须存在，如果允许 null 值，可以设置它的 required 属性为 false。如果我们想使用按照名称（byName）来装配，可以结合 @Qualifier 注解一起使用 |
| @Resource  | 作用与 Autowired 相同，区别在于 @Autowired 默认按照 Bean 类型装配，而 @Resource 默认按照 Bean 的名称进行装配。  @Resource 中有两个重要属性：name 和 type。 Spring 将 name 属性解析为 Bean 的实例名称，type 属性解析为 Bean 的实例类型。如果指定 name 属性，则按实例名称进行装配；如果指定 type 属性，则按 Bean 类型进行装配；如果都不指定，则先按 Bean 实例名称装配，如果不能匹配，则再按照 Bean 类型进行装配；如果都无法匹配，则抛出 NoSuchBeanDefinitionException 异常。 |
| @Qualifier | 与 @Autowired 注解配合使用，会将默认的按 Bean 类型装配修改为按 Bean 的实例名称装配，Bean 的实例名称由 @Qualifier 注解的参数指定。 |

**java代码：**

```java
//dao层代码
package dao.impl;

import dao.UserDAO;
import org.springframework.stereotype.Repository;

@Repository("ud")
public class UserDaoImpl implements UserDAO {


    public void add(){
        System.out.println("添加用户操作");
    }
}

//业务层代码
package dao.service;

import dao.impl.UserDaoImpl;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Service;

@Service
public class UserService {

    @Autowired
    @Qualifier("ud")
    private UserDaoImpl userDao;

    private UserService() {
    }

    public UserService(UserDaoImpl userDao) {
        this.userDao = userDao;
    }

    public void add(){
        userDao.add();
        System.out.println("添加用户成功");
    }

    public UserDaoImpl getUserDao() {
        return userDao;
    }

    public void setUserDao(UserDaoImpl userDao) {
        this.userDao = userDao;
    }
}

	//测试代码
    public void testZJ(){
        UserService userService = (UserService) GetBeanFactory.getContext().getBean("userService");
        userService.add();
    }
```

**这里是通过@AutoWired注解和@Qualifier来配合进行Bean的注入**

**通过@Resource注解进行Bean的注入：**

```java
//dao类
package dao.impl;

import dao.UserDAO;
import org.springframework.stereotype.Repository;

@Repository("ud")
public class UserDaoImpl implements UserDAO {


    public void add(){
        System.out.println("添加用户操作");
    }
}

//service类
package dao.service;

import dao.impl.UserDaoImpl;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Service;

import javax.annotation.Resource;

@Service
public class UserService {

//    @Autowired
//    @Qualifier("ud")
//	  @Resource(type = UserDaoImpl.class)
//	  @Resource(type = UserDaoImpl.class,name = "ud")
    @Resource(name = "ud")
    private UserDaoImpl userDao;
    
```

**这里是通过bean的名字来进行注入，也可以通过type来进行注入,也可以通过type和name来精确指定需要注入的bean**

## AOP面向切面编程

**面向切面编程AOP是Spring的核心功能之一，他的核心就是动态代理，这里只不过通过spring来帮我进行大部分代码的书写，我们只需要进行核心代码的书写。**

### AOP相关术语：

- 增强处理

  - 前置增强

    在需要增强的代码之前添加的代码被称为前置增强。

  - 后置增强

    在需要增强的代码之后添加的代码被称为后置增强。

  - 返回后增强

  - 抛出异常增强

  - 环绕增强

    在需要增强的代码前后都添加增强代码被称为环绕增强。

- 切入点

  可以是类，也可以是方法，若切入点是类，那么该类的所有方法都回被增强。

- 连接点

  AOP 的核心概念，指的是程序执行期间明确定义的一个点，例如方法的调用、类初始化、对象实例化等。

  在 Spring 中，连接点则指可以被动态代理拦截目标类的方法。

- 切面

  增强和切入点的组合。

- 目标对象

  需要进行增强的对象。

- AOP代理

  指生成代理的对象。

### AOP操作步骤

**通过xml配置文件对代码进行增强**

1. 在项目中添加AOP相关的jar包和在xml文件中添加相关文件
2. 编写迁前置增强和后置增强方法
3. 编写Spring配置文件，对业务代码进行增强处理
4. 编写代码获取带有增强处理的业务对象

**添加jar包，添加xml文件相关配置:**

```xml
<!--jar包-->
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-aop -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>5.3.20</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
    <!--Joinpoint-->
    <dependency>
      <groupId>org.aspectj</groupId>
      <artifactId>aspectjweaver</artifactId>
      <version>1.9.1</version>
    </dependency>



<!--spring.xml文件配置-->
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/aop
       https://www.springframework.org/schema/aop/spring-aop.xsd
">
    <!--被增强的类-->
    <bean id="user" class="dao.impl.IUserImpl"/>
    <!--实现动态代理的增强类-->
    <bean id="proxy" class="dao.proxy.UserProxy"/>
    <aop:config proxy-target-class="true">
        <!--定义切面-->
        <aop:aspect ref="proxy">
            <!--定义切入点-->
            <aop:pointcut id="a" expression="execution(public void add(..))"/>
            <!--通过切入点将增强(通知)织入进连接点-->
            <aop:before method="before" pointcut-ref="a"/>
        </aop:aspect>
    </aop:config>
</beans>
```

**java代码:**

```java
//实现类
package dao.impl;

import dao.intfce.IUser;


public class IUserImpl implements IUser {
    @Override
    public void add() {
        System.out.println("添加用户操作");
    }
}

//业务代码
package dao.proxy;

import org.aspectj.lang.JoinPoint;

public class UserProxy {

    public void before(JoinPoint joinPoint){
        System.out.println("前置增强");
        System.out.println("当前方法名："+joinPoint.getTarget());
    }
}

```

**测试代码：**

```java
@Test    
public void shouldAnswerWithTrue(){
        AbstractApplicationContext abstractApplicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
        IUserImpl user = abstractApplicationContext.getBean("user",IUserImpl.class);
        user.add();
}
```





















****

## IDEA无法识别并加载spring.xml配置文件

**报错：**`IOException parsing XML document from class path resource [applicationContext.xml]; nested exception is java.io.FileNotFoundException: class path resource [applicationContext.xml] cannot be opened because it does not exist`

出现这种情况是因为IDEA加载文件原理的问题，当IDEA运行的时候，识别的是target文件夹中的内容，我们只要将xml配置文件放在该文件夹中的classes文件夹中就可以识别到xml文件了。

#### 解决方法：

1. 将我们需要的xml文件放在target文件夹中的classes文件夹中。

   ![image-20220608115925638](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220608115925638.png)

2. 创建resources文件夹，将xml文件放在该文件夹中。

   ![image-20220608120013305](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220608120013305.png)

   这样的解决问题的原理是maven在编译的时候会将resource文件夹中的资源文件自动加载进classes目录中。

**出现错误的原因就是idea编译后的类中的spring容器找不到xml文件，只要将配置文件放到他们可以找到的位置就解决问题了。**



IDEA的pom中导入相关配置来加properties文件和xml文件。

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



****



