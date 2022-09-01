# Java类型转换

## Java基础数据类型之间的强制类型转换

## Java引用类型之间的强制类型转换

在Java中父类（接口）可以引用子类（实现类）的实例，这种方式被称为向上转型，多态。这样可以实现是因为父类（接口）定义的属性和方法子类（实现类）都可以继承，那么父类有的子类都有，而子类是父类的扩展，子类也可以看作是父类，所以父类可以，引用子类的实例。

但是反过来，通过子类来引用父类的实例是不行的，这种时候会在编译过程报错，因为子类是父类的拓展，子类有的东西父类不一定有，如果这个时候调用此实例就会调用不存在的方法，所以通不过编译。

**父类：**

```java
public class Father{
	public void a(){
        System.out.priuntln("a");
    }
}
```

**子类：**

```java
public class Son extends Father{
    public void b(){
        System.out.println("b");
    }
}
```

**测试代码：**

```java
public static void main(String[] args){
    Father father = new Son();//编译成功
    Son son = new Father();//编译报错
}
```

**此时在内存中声明了一个Father类型的属性，该属性实际指向的是Son类的实例，所以我们可以将该对象赋值给Son类型的属性：**

```java
public static void main(String[] args){
    Father father = new Son();//编译成功
    Son son = (Son) father;//编译成功
}
```

这样可以编译通过是因为father变量实际指向的对象本质还是Son类型的对象，这个时候使用该变量虽然只能调用父类中拥有的方法，但是不代表没有子类中的方法，我们不能调用只是因为该方法被隐藏了。所以我们可以通过强制类型转换将father变量放入Son类型的son变量中，且不会报错。

**测试代码2：**

```java
public static void main(String[] args){
    Father father = new Father();//编译成功
    Son son = (Son) father;//编译失败
}
```

**这里同样是Father类和Son类，但是这里的father变量指向的是一个Father类型的实例，下面在进行向子类强制类型转换的时候就会爆出编译错误。这里父类指向子类对象不会报错是因为父类有的子类都有，那么我们就可以将这两个类看作是同一个类。**

**但是其实父类和子类是两个不一样的类，父类是不包含子类自己定义的方法的，如果子类变量指定父类对象，就会报出异常，因为父类对象没有子类特有的方法，所以会爆出`java.lang.ClassCastException`异常。**

****

### instanceof关键字

**为什么要使用instanceof：**

在虽然在代码中我们可以使用强制类型转换来将包含子类对象的父类变量赋值给一个新的子类变量，但是这样做就违背了我们只通过代码来控制程序的原则，在代码中添加了人为的影响。

这个时候我们呢就可以通过instanceof关键字判断该对象是否可以转换为其他类。

**instanceof原理：**

instanceof是Java的保留字关键字，他的作用是测试左边的对象是否是他右边类的实例，最后会返回一个boolean数据类型。

**需要注意的是使用instanceof关键字时如果比较的对象和类之间没有继承和实现关系的话，也是会出现编译错误的。**

**实验代码：**

```java
Father father = new Father();
Son son = new Son();
String str = new String("value");

System.out.println(son instanceof Father);//true
System.out.println(son instanceof Son);//true
System.out.println(father instanceof Son);//false
System.out.println(str instanceof Son);//编译错误
```

**此处需要注意，若比较的对象是null的话，也会返回false**