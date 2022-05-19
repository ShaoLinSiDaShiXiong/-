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

