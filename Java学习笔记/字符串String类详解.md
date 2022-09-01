# 字符串String类详解

**字符串是我们在代码中经常见到的一个引用数据类型**

## String的特性和基础知识

- String类是被final修饰的类，不能被其他类继承
- String实现了Serializable和Comparable接口，表示String支持序列化和课比较大小
- String底层是通过char类型的数组数据实现的，并被final修饰，所以字符串的值创建之后就不可以被修改，具有不可变性。
- String类重写了equals方法，String类重写后的equals方法是比较两个字符串内容是否一致的，而不是比较引用地址。

```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {
    /** The value is used for character storage. */
    private final char value[];
```

### String类型的不可变性

通过字面量方式为字符串赋值时，此时的字符串存储在堆内存中的字符串常量池中，并且在字符串常量池中不会存储相同内容的字符串。

此时如果有两个变量都以字面量的形式声明了相同的字符串，那么他们指向的是字符串常量池中的一个字符串，若此时对两个变量使用”==“得到的结果会是true。

若将其中一个变量的字符串改为其他字符串，那么该变量就会指向新的字符串地址，抛弃原本的地址，此时使用”==“得到的结果会是false。因为”==“比较的是引用地址。

```java
String str1 = "hi";
String str2 = "hi";
System.out.println(str1 == str2);//true
str2 = "hello";
System.out.println(str1 == str2);//false
```

**String字符串具有不可变性，当字符串重新赋值时，不会在原来的内存地址进行修改，而是重新分配新的内存地址进行赋值。**

**当字符串进行拼接时，也不会在原来的内存地址进行修改，而是重新分配新的内存地址进行赋值。**

**当调用String的replace方法修改指定的字符或字符串时，也不会在原来的内存地址进行修改，也是重新分配新的内存地址进行赋值。**

****

### String内容在内存中的表现

**我们声明String类型的数据又两种方式，一种是通过字面量的形式来声明，另外一种就是通过new来创建。**

- **字面量形式声明String：**

  ```java
  String str1 = "value";
  ```

  如果是以字面量的形式来声明的字符串，那么该变量中指定的字符串是直接指向字符串常量池中的字符串的。

  `str1 => [(堆内存) “value”]`

- **通过new来声明String：**

  ```java
  String str2 = new String("value");
  ```

  如果以new来声明字符串，那么该变量指向的是堆内存中的String对象，该String对象指向包含字符串的字符串常量池中的字符串。

  `str1 => [(堆内存) String => “value”]`

### String不同拼接方式的对比

```java
public static void main(String[] args) {
    String s1="Hello";
    String s2="World";

    String s3="HelloWorld";
    String s4="Hello"+"World";
    String s5=s1+"World";
    String s6="Hello"+s2;
    String s7=s1+s2;

    System.out.println(s3==s4); //true
    System.out.println(s3==s5); //false
    System.out.println(s3==s6); //false
    System.out.println(s3==s7); //false
    System.out.println(s5==s6); //false
    System.out.println(s5==s7); //false
    System.out.println(s6==s7); //false

    String s8=s5.intern();
    System.out.println(s3==s8); //true
}
```

(1)Java中有常量优化机制，“Hello"和"World"本身就是字符串常量，所以在编译时，会直接把"Hello"和"World"合并成"HelloWorld"字符串，又因为在执行s3的时候已经在常量池中创建了"HelloWorld”，所以s3==s4。
(2)当变量与字面量或变量与变量进行拼接时，会在堆中创建一个StringBuilde对象，然后使用StringBuilder的append()方法将变量与字面量或变量与变量进行拼接，最后调用toString()方法转成String对象。所以s5、s6、s7指向的都是堆内存中String对象的地址值。
(3)使用intern()这个方法时，首先会检查字符串常量池中是否有对应的字符串，如果存在则返回这个字符串的引用；否则会先将字符串添加到字符串常量池中，然后再返回这个字符串的引用。所以s3==s8。

易错的笔试题

```java
public static void main(String[] args) {
    final String s1="Hello"; 
    String s2="HelloWorld";
    String s3=s1+"World";
    System.out.println(s2==s3); //true
}
```


此时的s1用final进行修饰，表示的是一个常量，所以此时s1+“World"就相当于"Hello”+“World”，结果仍然是一个常量，所以s2==s3。

## String类的常用方法

```java
int length()：返回字符串的长度
char charAt(int index)：返回指定索引处的字符
boolean isEmpty()：判断字符串是否为空
String toLowerCase()：将字符串中的所有字符转换为小写
String toUpperCase()：将字符串中的所有字符转换为大写
String trim()：返回字符串的副本，去掉前导空白和尾部空白，中间的空白不会被去掉
boolean equals(Object obj)：比较字符串的内容是否相同
boolean equalsIgnoreCase(String anotherString)：忽略大小写，比较字符串的内容是否相同
String concat(String str)：将指定字符串连接到此字符串的结尾，等价于用“+”。但是相比之下，concat方法的效率要高于“+”
int compareTo(String anotherString)：比较两个字符串的大小
String substring(int beginIndex)：返回从beginIndex到末尾的子字符串
String substring(int beginIndex, int endIndex)：返回从beginIndex到endIndex前一位的子字符串,不包括endIndex
boolean endsWith(String suffix)： 判断字符串是否以指定的后缀结束
boolean startsWith(String prefix)：判断字符串是否以指定的前缀开始
boolean startsWith(String prefix, int toffset)：判断字符串在指定索引开始的子字符串是否以指定前缀开始
boolean contains(CharSequence s)：判断当前字符串中是否包含指定的字符串
int indexOf(String str)：返回指定子字符串在当前字符串中第一次出现处的索引
int indexOf(String str, int fromIndex)：返回从指定的索引后，指定子字符串在当前字符串中第一次出现处的索引
int lastIndexOf(String str)：返回指定子字符串在当前字符串中最后一次出现处的索引
int lastIndexOf(String str, int fromIndex)：返回从指定的索引后，指定子字符串在当前字符串中最后一次出现处的索引
注：indexOf和lastIndexOf方法如果未查找到指定子字符串时，返回值都为-1。
String replace(char oldChar, char newChar)：替换当前字符串中指定的子字符串
String[] split(String regex)：根据指定的符号拆分当前字符串，然后返回一个String数组
```

## StringBuilder和StringBuffer

**因为String是不可变的，如我我们要在短时间内对字符串进行拼接，如果直接使用String+=不仅效率低下，且所带来的内存占用是很大的。因为需要不断的new对象。**

**测试代码：**

```java
    @Test
    public void test03(){
        String a = "a";
        StringBuilder b = new StringBuilder();
        StringBuffer c = new StringBuffer();
        Long time = System.currentTimeMillis();
        for(int i = 0; i < 3000_0; i++){
            a += i;
        }
        Long nowTime = System.currentTimeMillis();
        System.out.println("+=:"+(nowTime - time));

        time = System.currentTimeMillis();
        for(int i = 0; i < 3000_0; i++){
            a = a.concat(String.valueOf(i));
        }
        System.out.println("concat:"+(System.currentTimeMillis() - time));

        time = System.currentTimeMillis();
        for(int i = 0; i < 3000_0; i++){
            b.append(i);
        }
        System.out.println("StringBuilder:" + (System.currentTimeMillis() - time));

        time = System.currentTimeMillis();
        for(int i = 0; i < 3000_0; i++){
            c.append(i);
        }
        System.out.println("StringBuffer:" + (System.currentTimeMillis() - time));
    }
```

**运行结果：**

```
+=:1402
concat:1025
StringBuilder:1
StringBuffer:3
```

可以看到，在进行字符串拼接时StringBuilder的效率是最高的，接下来是StringBuffer，concat方法的效率排在第二，最后才是使用“+”进行拼接。

### 认识StringBuilder和StringBuffer

StringBuilder和StringBuffer这两个类都是继承自AbstractStringBuilder类，该类分别继承自charsequence接口和Appendable接口。

StringBuilder和StringBuffer主要是用于进行字符串的频繁拼接，这两个类和String不相同的是，String每次做出更改都会创建新的对象，因为String的不可变性，但是StringBuilder和StringBuffer进行字符串拼接主要是操作创建的对象。



下面我们对比了String、StringBuffer与StringBuilder的区别：

| String                   | StringBuffer                               | StringBuilder          |
| ------------------------ | ------------------------------------------ | ---------------------- |
| final修饰，不可继承      | final修饰，不可继承                        | final修饰，不可继承    |
| 字符串常量，创建后不可变 | 字符串变量，可动态修改                     | 字符串变量，可动态修改 |
| 不存在线程安全问题       | 线程安全，所有public方法由synchronized修改 | 线程不安全             |
| 大量字符串拼接效率最低   | 大量字符串拼接效率非常高                   | 大量字符串拼接效率最高 |

**StringBuilder和StringBuffer非常相似，他们对字符串的操作是通过char[]来实现的，通过默认构造器创建的StringBuilder，其内部创建的char[]的默认长度为16，当然可以调用重载的构造器传递初始长度（推荐这样，因为这样可以减少数组扩容次数，提高效率）。**

**每次调用append(string)方法时，会首先判断数组长度是否足以添加传递来的字符串，如果传递的字符串长度 + 数组已存放的字符的长度 > 数组的长度，这时就需要进行数据扩容了**

**扩容规则如下：默认将数组长度设置为“ (当前数组长度 * 2) + 2”，但如果按此规则扩容后的数组也不足以添加新的字符串，就需要将数组长度设置为“数组内字符长度 + 传递的字符串长度”。**

**因此假如我们知道拼接的字符串大概长度有100多字符，我们就可以设置初始长度150或200，这样就可以避免或减少数组扩容的次数，从而提高效率。**

**总结：**

1. StringBuilder与StringBuffer 都是为了解决大量字符串拼接时的性能问题，其实就是为了解决String类在拼接过程中产生的大量对象的问题，因为这会导致大量内内存分配和GC 问题
2. StringBuilder与StringBuffer 二者之间的主要区别是线程是否安全，StringBuffer 通过对方法添加synchronized关键字保证了线程安全。
3. StringBuilder与StringBuffer底层都是依赖字符数组实现的，不同于String 的是String 底层的字符数组是不可变的，也就是final 修饰的，其实这就是StringBuilder与StringBuffer可变的原因，动态扩展字符数组来实现的。
4. 为了提高StringBuilder与StringBuffer的性能我们可以通过设置合适的容量来避免数组库容。

### StringBuffer 方法

以下是 StringBuffer 类支持的主要方法：

| 序号 | 方法描述                                                     |
| :--- | :----------------------------------------------------------- |
| 1    | public StringBuffer append(String s) 将指定的字符串追加到此字符序列。 |
| 2    | public StringBuffer reverse()  将此字符序列用其反转形式取代。 |
| 3    | public delete(int start, int end) 移除此序列的子字符串中的字符。 |
| 4    | public insert(int offset, int i) 将 `int` 参数的字符串表示形式插入此序列中。 |
| 5    | insert(int offset, String str) 将 `str` 参数的字符串插入此序列中。 |
| 6    | replace(int start, int end, String str) 使用给定 `String` 中的字符替换此序列的子字符串中的字符。 |

以下列表列出了 StringBuffer 类的其他常用方法：

| 序号 | 方法描述                                                     |
| :--- | :----------------------------------------------------------- |
| 1    | int capacity() 返回当前容量。                                |
| 2    | char charAt(int index) 返回此序列中指定索引处的 `char` 值。  |
| 3    | void ensureCapacity(int minimumCapacity) 确保容量至少等于指定的最小值。 |
| 4    | void getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin) 将字符从此序列复制到目标字符数组 `dst`。 |
| 5    | int indexOf(String str) 返回第一次出现的指定子字符串在该字符串中的索引。 |
| 6    | int indexOf(String str, int fromIndex) 从指定的索引处开始，返回第一次出现的指定子字符串在该字符串中的索引。 |
| 7    | int lastIndexOf(String str) 返回最右边出现的指定子字符串在此字符串中的索引。 |
| 8    | int lastIndexOf(String str, int fromIndex) 返回 String 对象中子字符串最后出现的位置。 |
| 9    | int length()  返回长度（字符数）。                           |
| 10   | void setCharAt(int index, char ch) 将给定索引处的字符设置为 `ch`。 |
| 11   | void setLength(int newLength) 设置字符序列的长度。           |
| 12   | CharSequence subSequence(int start, int end) 返回一个新的字符序列，该字符序列是此序列的子序列。 |
| 13   | String substring(int start) 返回一个新的 `String`，它包含此字符序列当前所包含的字符子序列。 |
| 14   | String substring(int start, int end) 返回一个新的 `String`，它包含此序列当前所包含的字符子序列。 |
| 15   | String toString() 返回此序列中数据的字符串表示形式。         |

## 注意事项

### 在网络中判断String是否为空

在Servlet中我们最常做的就是字符串的处理，但是在处理字符串之前，我们最好还是先进行字符串的非空判断。

**空字符串的几种表现：**

- 字符串为`null`

  这种情况是最好判断的，只要通过运算符进行比较就可以得到答案。

  ```java
  String str = "a";
  System.out.println(a == null)//false
  ```

  这种方式其实已经可以对应大部分的应用场景了，但是在实际应用中，我们还很可能接收到空字符串，此时字符串没有内容，但是页不为是null。

- 字符串为“”

  一般在这种情况发生在页面的请求中，客户端可能给通过请求发来一个空的字符串，这个时候我们需要通过String类自带的equals方法来进行判断。

  ```java
  String str = "";
  System.out.println("".equals(str))//true
  ```

  值得注意的是，通过equals方法判断字符串时，如果该对像本身为null，在代码执行的过程中就会报错，所以这里使用字面量的形式指定了一个空字符串来使用equals方法。

- 字符串中都是空格

  这种情况很类似于空字符串的情况，但是判断这种情况的方式和判断空字符串的方式大不相同，因为我们也不知道字符串中到底有多少个空格，可能是1个，也可能是一千个，我们总不能写一千个if来进行判断。

  这个时候我们需要可以调用Stirng自带的trim方法来去除空格（该方法会去除字符串前后的空格，字符串中间加载的空格不会被去除），或者使用contains方法来判断字符串是否包含空格。

  **trim方法：**

  ```java
  String str = "   ";
  //非空判断
  if(str != null){
  	//去除字符串中包含的空格。
      str = str.trim();
  }
  System.out.println("".equals(str))//true
  ```

  **contains方法：**

  ```java
  String str = "   ";
  //非空判断
  if(str != null){
  	//查看字符串中是否包含空格
      Boolean flag = str.contains(" ");
  }
  System.out.println(flag);//true
  ```

  <font color="#F00">需要注意的是，contains方法会将包含空格的正常字符串也判断为true，所以该方法一般用于字符串检查中用,因为在有些方法中，如果字符串带有空格也是一件很头痛的事情。</font>

### trim方法不能去除的空格

<font color="#F00">trimg方法不能去除全角空格，想要去除，需要将全角空格转换为半角空格。</font>

**全角空格是unicode为12288的字符串，这里进行了转换之后就可以正常去除了**

```java
str = str.replace((char)12288, ' ');
str = str.trim();
```

