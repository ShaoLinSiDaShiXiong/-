# Java反射机制(Reflection)

## 动态语言和静态语言

### 动态语言

动态语言是一类在运行时可以改变其结构的语言，例如新的函数、对象、甚至代码可以被引进，已有的函数可以被删除或是其他结构上的变化，通俗点来说就是在运行时代码可以根据某些条件改变自身的结构。

**主要的动态语言：**Object-c、C#、JavaScript、PHP、Python等



### 静态语言

与动态语言相对的，运行时结构不可变的语言就是静态语言。如Java、C、C++

**Java不是动态语言，但可以被成为“准动态语言”，即Java有一定的动态行，我们可以利用反射机制获取类似动态语言的特性。**

****

## 反射机制概述

**Reflection(反射)是Java被视为准动态语言的关键，反射机制允许程序在执行期间借助Reflection API取得任何类内部信息，并能直接操作任意对象的内部有属性以及方法。**

```java
Class c = Class.forName("java.lang.String");
```

**加载完类之后，在堆内存的方法区中就产生了一个Class类型的对象，（一个类只有一个Class对象）这个对象就包含了完整的类的结构信息。我们可以通过这个对象看到类的结构。这个对象就像一面镜子，透过这个镜子看到类的结构，所以我们星星的称之为反射。**

**正常方式：**引入需要的包类名称 => 通过new实例化 => 取得实例化对象

**反射方式：**实例化对象 => getClass()方法 => 得到完整的“包类”名称。

****

## 反射提供的功能

- 在运行时判断任意一个对象所属的类。
- 在运行时构造任意一个类的对象。
- 在运行时判断任意一个类的对象。
- 在运行时判断任意一个类所具有的成员变量和方法。
- 在运行时获取泛型信息。
- 在运行时调用任意一个对象的成员变量和方法。
- 在运行时处理注解。
- 生成动态代理。

##### 反射的优点

可以实现动态创建对象和编译，体现出很大的灵活性。

##### 反射的缺点

对性能有影响，使用反射基本上是一种解释操作，我们可以告诉JVM，我们希望做什么并且满足我们的需求，这类操作总是慢于直接执行相同的操作。

##### 反射的主要API

- java.lang.Class:代表一个类。
- java.lang.Method:代表类的方法。
- java.lang.reflect.Field:代表类的成员变量。
- java.lang.reflect.Constructor:代表类的构造器。

<font color="#f00">**一个类在内存中只有一个Class对象。**</font>

<font color="#f00">**一个类被加载后，类的整个结构都会被封装在Class对象中**</font>

## Class类

在java世界里，一切皆对象。从某种意义上来说，java有两种对象：实例对象和Class对象。每个类的运行时的**类型信息**就是用Class对象表示的。它包含了与类有关的信息。

**每一个类都有一个Class对象，每当编译一个新类就产生一个Class对象，Class类没有公共的构造方法，Class对象是在类加载的时候由Java虚拟机以及通过调用类加载器中的 defineClass 方法自动构造的，因此不能显式地声明一个Class对象。**

- Class本身也是一个类
- Class对象只能系统建立对象。
- 一个加载的类在JVM中只会有一个Class实例。
- 一个Class对象对应的是一个加载到JVM中的一个.class文件。
- 

### Class类的常用方法

| 方法名                                  | 功能说明                                                  |
| --------------------------------------- | --------------------------------------------------------- |
| static ClassforName(String)             | 返回指定类名name的Class对象。                             |
| getName()                               | 返回此Class对象所表示的实体(类、接口、数组类或void)的名称 |
| Class getSuperClass()                   | 返回当前Class对象的父类的Class对象。                      |
| Class[] getInterfaces()                 | 获取当前Class对象的接口。                                 |
| ClassLoader getClassLoader()            | 返回该类的类加载器。                                      |
| Constuctor[] getConstructors()          | 返回一个包含某些Constructor对象的数组。                   |
| Object newInstance()                    | 调用缺省构造函数，返回Class对象的一个实例。               |
| Method getMothed(String name,Class.. t) | 返回一个Method对象，此对象的形参类型为paramType           |
| Field[] getDeclaredFields()             | 返回Field对象的一个数组。                                 |

### 获取Class类的实例

获取其他对象的Class类对象的的方式有三种分别是

1. **已知具体的类，通过类的class属性获取，该方法最为可靠，程序性能最高。**

   ```java
   //通过类来获取Class对象
   Class<Student> c2 = Student.class;
   System.out.println(c2.hashCode());
   ```

2. **已知某个类的实例，调用该实例的getClass()方法获取Class对象。**

   ```java
   //通过对象来获取该类的Class对象
   Class<? extends Student> c3 = new Student().getClass();
   System.out.println(c3.hashCode());
   ```

   在这里是简写的形式来展示获取Class对象的方式，在正常的代码中我们一般都是使用对应的对象来使用getClass方法来获取对应的Class对象。

3. **已知一个类的全名，且该类在路径下，可以同故宫Class类的静态方法forName()获取，可能抛出ClassNontFoundException**

   ```java
   //通过类名来获取Class对象
   try {
   	Class c1 = Class.forName("reflection.Student");
   	System.out.println(c1.hashCode());
   }catch(ClassNotFoundException e) {
   	System.out.println(1);
   }
   ```

<font color="#f00">Java的内置基本数据类型可有直接用类名。Type</font>

```java
//获得基本类型的Class对象
Class<?> c5 = Integer.TYPE;
System.out.println(c5);
```

<font color="#f00">**还可以利用ClassLoader**</font>

**完整代码如下**

```java
package reflection;

public class Reflection {
	public static void main(String[] args) {
		//通过类名来获取Class对象
		try {
			Class c1 = Class.forName("reflection.Student");
			System.out.println(c1.hashCode());
		}catch(ClassNotFoundException e) {
			System.out.println(1);
		}
		//通过类来获取Class对象
		Class<Student> c2 = Student.class;
		System.out.println(c2.hashCode());
		
		//通过对象来获取该类的Class对象
		Class<? extends Student> c3 = new Student().getClass();
		System.out.println(c3.hashCode());
		
		//获得student父类的class对象
		Class<?> c4 = c3.getSuperclass();
		System.out.println(c4);
		
		//获得基本类型的Class对象
		Class<?> c5 = Integer.TYPE;
		System.out.println(c5);
	}
}

//声明一个父类
class Preson{
	private String name = "人";

	public Preson(String name) {
		this.name = name;
	}

	public Preson() {}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	@Override
	public String toString() {
		return "Preson [name=" + name + "]";
	}
	
	
}

//声明一个子类来继承父类
class Student extends Preson{
	private Integer age;
	public Student() {}
	public Student(Integer age) {
		this.age = age;
	}
	public Integer getAge() {
		return age;
	}
	public void setAge(Integer age) {
		this.age = age;
	}
	@Override
	public String toString() {
		return "Student [age=" + age + "]";
	}

```

### 那些类可以有Class对象？

**在Java中有一下几个类型可以拥有Class对象**

- **class：**外部类，成员（成员内部类，静态内部类），局部内部类，匿名内部类。
- **interface：**接口
- **[]：**数组（二维数组）
- **enum：**枚举
- **annotation：**注解@interface
- **primitive type:**基本数据类型
- **void**

```java
	public static void main(String[] args) {
		Class c1 = Class.class;//类
		Class c2 = String[].class;//一维数组
		Class c3 = int[][].class;//二维数组
		Class c4 = Override.class;//注解
		Class c5 = ElementType.class;//枚举
		Class c6 = Runnable.class;//接口
		Class c7 = Boolean.class;//基本数据类型
		Class c8 = void.class;//void
		
		System.out.println(c1);
		System.out.println(c2);
		System.out.println(c3);
		System.out.println(c4);
		System.out.println(c5);
		System.out.println(c6);
		System.out.println(c7);
		System.out.println(c8);
	}
```

**运行结果：**

```
class java.lang.Class
class [Ljava.lang.String;
class [[I
interface java.lang.Override
class java.lang.annotation.ElementType
interface java.lang.Runnable
class java.lang.Boolean
void
```

##   Java内存分析

Java的内存分为三个部分分别是`堆内存`，`栈内存`，和`方法区`

### 堆内存

堆内存中存放的是new的对象和数组，堆内存中的数据可以被所有的线程共享，且不会存放别的对象的引用。

### 栈内存

栈内存中存放基本变量类型（会包含这个基本类型的基本数值）和引用对象的变量（会存放这个引用在堆里面的具体地址）

### 方法区

可以被所有线程共享，包含所有class和static变量

****

## Java类的加载过程

当程序主动使用某个类时，如果该类还未被初始化加载到内存中，则系统会通过一下三个步骤来对类进行初始化。

**`类的加载(load)>类的链接(Link)>类的初始化(Initlalize)`**



## 类的加载于ClassLoader的理解

一个类的完整加载过程分为`加载》链接》初始化`以下三步：

#### 1.加载：

将class文件字节码内容加载到内存中，并将这些静态数据转换成方法区的运行时数据结构，然后生成一个代表这个类的java.lang.Class对象。

#### 2.链接：

将Java类的二进制代码合并到JVM的运行状态之中的过程。

1. ##### 验证：

   确保加载的类信息符合JVM规范，没有安全方面的问题。

2. ##### 准备：

   正式为类变量（static）分配内存，并设置变量为默认初始值的阶段，这些内存都将在方法区中进行分配。

3. ##### 解析：

   虚拟机常量池内的符号引用（常量名）替换为直接引用（地址）的过程。

#### 3.初始化：

1. 执行类构造器< clinit >()方法的过程。类构造器< clinit >()方法是由编译器自动收集类中所有类变量的赋值动作和静态代码块中的语句合并产生的。（类构造器是构造类信息的，不是构造该类对象的构造器）
2. 当初始化一个类的时候，如果发现其父类还没有进行初始化，则需要先出发其父类的初始化。
3. 虚拟机会保证一个类的< clinit >()方法在多线程环境中被正确加载和同步。

## 什么时候会发生类的初始化

### 类的主动引用（一定会发生类的初始化）

- 当虚拟机启动，先初始化main方法所在的类。
- new一个类的对象
- 调用类的静态成员（除了final常量）和静态方法
- 使用java.lang.reflect包的方法对类进行反射调用
- 当初始化一个类，如果其父类没有被初始化，则先会初始化他的父类

### 类的被动引用（不会发生类的初始化）

- 当访问一个静态域的时，只有真正声明这个域的类才会被初始化，如：当通过子类引用父类的静态变量，不会导致子类初始化。
- 通过数组定义类的引用，不会触发此类的初始化。
- 引用常量不会触发此类的初始化（常量在链接阶段就存入调用类的常量池中了）

## 类加载器的作用

**一个类的正常加载会经历下面这些过程，首先Java编译器会将.java源文件编译成字节码文件（.class）之后再通过类装载器，最后通过字节码校验器进行校验，再通过解释器解释成操作系统平台可以看的懂的形式进入操作系统平台。**

-  类加载器的作用：

  将class文件字节码的内容加载到内存中，并将这些静态数据库转换成方法去的与运行时数据结构，然后在队中生成一个代表这个类的java.lang.Class对象，作为方法区中类数据的访问入口。

- 类缓存：

  标准的JavaSE类加载器可以按要求查找类，但一旦某个类被加载到类加载器中，它将维持加载（缓存）对短时间。不过JVM垃圾回收机制可以回收这些Class对象。

**类加载器的作用是用来把类（class）装载进内存的。JVM规范定义了如下类型的类和加载器。**

- **引导类加载器：**

  用c++编写的，是JVm自带的类加载器，负责Java平台核心库，用来装载核心类库，该加载器无法直接获取。

- **扩展类加载器：**

  负责jre/lib/ext目录下的jar包或-D java.ext.dire指定目录下的jar包装入工作库。

- **系统类加载器：**

  负责java-classpath或-D java.class.path所指的目录下的类与jar包装如入工作，是最常用的类加载器。

<font color="#f00">**java的核心jar包就是`rt.jar`包，这个包里面包含了我们最常用的一些包，比如lang，math，io，sql等等**</font>
