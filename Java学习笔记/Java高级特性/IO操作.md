# IO流

 PrintWriter

https://blog.csdn.net/thedarkclouds/article/details/85333033

## 什么是io流？

<font color="#900">**io流就是输入（Input Stream）流和输出流（Output Stream）**</font>

#### **按照流的流向来分可以分为两种流：**

- 输入流：输入流能从流中<font color="#900">读取</font>数据，而不能从流中写入数据。![](C:\Users\SaoLinSiDaShiXiong\Pictures\笔记图片\输入流.png)

  *网络，文件或者数据库等资源，通过输入流来将资源传送到目的地，来被程序获取，这个过程就是一个读取的过程。*

- 输出流：输出流只能向流中<font color="#900">写入</font>数据，而不能从流中读取数据。

  ![输出流](C:\Users\SaoLinSiDaShiXiong\Pictures\笔记图片\输出流.png)

  *从文件源通过输出流将数据输出到其他设备，或存储空间，这本身就是一个写入的过程。*



****

#### 流可以分为两种流

- 字节流：字节流所操作的基本数据单元是八位的字节（byte），这种字节只有机器读得懂，人都不懂，字节流是万能的，不管是什么文件都可以通过字节流来进行传输。比如图片和视频，如果用字节流来进行传输，那么他们的传输过程就会是一段一段的字节在进行写入。
- 字符流：字符流所操作的基本数据单元是十六位的字符（Unicode），字符流具有局限性，字符流里面的额数据，是人可以看得懂的数据。



****

#### 流按照功能可以分为两种：

- 节点流：
- 处理流：



****

## 字节流

### 字节输入流

**Java流相关的类都封装在java.io包中，而且每个数据流都是一个对象。所有字节输入流都是IntputStream抽象类（字节输入流）和Reader（字符输入流）的子类，其中InputStream类是字节输入流的抽象类，是所有字节输入流的父类。**

<img src="C:\Users\SaoLinSiDaShiXiong\Pictures\笔记图片\字节输入流.png" style="zoom:100%;" />

#### InputStream常用方法

| 返回值 | 方法名                         | 描述                                                         |
| ------ | ------------------------------ | ------------------------------------------------------------ |
| int    | read()                         | 从输入流读入一个8字节的数据，将他转换成一个0~255的整数，如果遇到输入流的结尾则返回-1。在这里每一个整数都代表着一个值，可以是英语单词，也可以是中文汉字。 |
| int    | read(byte[] b)                 | 从输入流读取若干字节的数据保存到参数b指定的字节数组中，返回的字节数表示读取的字节数，如果遇到输入流的结尾返回-1 |
| int    | read(byte[] b,int off,int len) | 从输入流读取若干字节的书v就保存到参数b指定的字节数组中，其中off是指在数组中开始保存数据位置的其实下标，len是值读取字节的位数，发挥的是实际读取的字节数，如果遇到输入流的结尾返回-1. |
| void   | close()                        | 关闭数据流，当完成对数据流的操作之后需要关闭数据流。<font color="#900">**每次进行玩流操作之后必须关闭流！**</font> |
| int    | available()                    | 返回可以从数据源读取的数据流的位数。                         |



****



### 文件输入流FileInpuStream

FileInputStream是Java流中比较常用的一种，他表示从文件系统的某个文件获取输入字节，。通过使用FileInPutStream可以访问文件中的一个字节，一批字节或整个文件。

**在创建FileInputStream类的对象时，如果找不到指定的文件则会抛出File Not Found Exception异常。**

#### FileInputStream 常用的构造方法。

1. FileInputStream(File file)：通过打开一个到实际文件的连接来创建一个 FileInputStream，该文件通过文件系统中的 File 对象 file 指定。
2. FileInputStream(String name)：通过打开一个到实际文件的链接来创建一个 FileInputStream，该文件通过文件系统中的路径名 name 指定。


下面的示例演示了 FileInputStream() 两个构造方法的使用。

```java

try {    // 以File对象作为参数创建FileInputStream对象
    FileInputStream fis1 = new FileInputStream(new File("F:/mxl.txt"));
    // 以字符串值作为参数创建FilelnputStream对象
    FileInputStream fis2 = new FileInputStream("F:/mxl.txt");} catch(FileNotFoundException e) {    System.out.println("指定的文件找不到!");}
```



****

### 文件输出流FileInpuStream

<font color="#900">FileOutputStream 类继承自 OutputStream 类，重写和实现了父类中的所有方法。</font>FileOutputStream 类的对象表示一个文件字节输出流，可以向流中写入一个字节或一批字节。<font color="#900">在创建 FileOutputStream 类的对象时，如果指定的文件不存在，则创建一个新文件；如果文件已存在，则清除原文件的内容重新写入。</font>

#### FileOutputStream 类的构造方法。

1. FileOutputStream(File file)：创建一个文件输出流，参数 file 指定目标文件。
2. FileOutputStream(File file,boolean append)：创建一个文件输出流，参数 file 指定目标文件，<font color="#900">**append 指定是否将数据添加到目标文件的内容末尾，如果为 true，则在末尾添加；如果为 false，则覆盖原有内容；其默认值为 false。**</font>
3. FileOutputStream(String name)：创建一个文件输出流，参数 name 指定目标文件的文件路径信息。
4. FileOutputStream(String name,boolean append)：创建一个文件输出流，参数 name 和 append 的含义同上。



#### 对文件输出流有如下四点说明：

1. 在 FileOutputStream 类的构造方法中指定目标文件时，目标文件可以不存在。
2. 目标文件的名称可以是任意的，例如 D:\\abc、D:\\abc.de 和 D:\\abc.de.fg 等都可以，可以使用记事本等工具打开并浏览这些文件中的内容。
3. 目标文件所在目录必须存在，否则会拋出 java.io.FileNotFoundException 异常。
4. 目标文件的名称不能是已存在的目录。例如 D 盘下已存在 Java 文件夹，那么就不能使用 Java 作为文件名，即不能使用 D:\\Java，否则抛出 java.io.FileNotFoundException 异常。



****

### 字节输出流

**在Java中所有输出流类都是OutputStream抽象类（字节输出流）和Writer抽象类（字符输出流）的子类，其中OutputStream类是字节输入流的抽象类，是所有字节输出流的父类。**

![](C:\Users\SaoLinSiDaShiXiong\Pictures\笔记图片\字节输出流.png)

#### OutputStream的常用方法

| 返回值 | 方法名                           | 描述                                                       |
| ------ | -------------------------------- | ---------------------------------------------------------- |
| int    | write(byte b)                    | 将只当的字节数据写入到输出流。                             |
| int    | write(byte[] b)                  | 将指定的字节数组的内容写入输出流。                         |
| int    | write(bytep[] b,int off,int len) | 将指定自己的数组从off位置开始的len字节的内容写入到输入流。 |
| void   | close()                          | 关闭数据流，当完成对数据流的操作之后必须关闭数据流。       |
| void   | flush()                          | 刷新输出流，强行将缓冲区的内容写入到输出流。               |

​	

****

## 字符输入流

Reader 类是所有字符流输入类的父类，该类定义了许多方法，这些方法对所有子类都是有效的。

Reader 类的常用子类如下。

- CharArrayReader 类：将字符数组转换为字符输入流，从中读取字符。
- StringReader 类：将字符串转换为字符输入流，从中读取字符。
- BufferedReader 类：为其他字符输入流提供读缓冲区。
- PipedReader 类：连接到一个 PipedWriter。
- InputStreamReader 类：将字节输入流转换为字符输入流，可以指定字符编码。

**Reader类中也包含close(),mark(),skip()和reset()方法。他们的作用大同小异。**

#### Reader类中的read()方法

| 返回值 | 方法名                            | 描述                                                         |
| ------ | --------------------------------- | ------------------------------------------------------------ |
| int    | read()                            | 从输入流中读取一个字符，并把它转换为0~65535的整数。如果返回-1表示一斤到了输入流的末尾。 |
| int    | read(char[] cbuf)                 | 从输入流中读取若干个字符，并把他们保存到参数cbuf指定的字符数组中，该方法返回读取的字符数，如果返回-1表示已经到了输入流的末尾。 |
| int    | read(char[] cbuf,int off,int len) | 从输入流中读取若干个字符，并把他们保存到参数cbuf指定的字符数组中，其中off指定在字符数组中开始保存数据的其实下表，len指定读取的字符数，该方法返回实际读取的字符数，如果返回-1则表示已经到了输入流的末尾。 |



****





## 字符输入流

Writer 类是所有字符输出流的父类，该类中有许多方法，这些方法对继承该类的所有子类都是有效的。

Writer 类的常用子类如下。

- CharArrayWriter 类：向内存缓冲区的字符数组写数据。
- StringWriter 类：向内存缓冲区的字符串（StringBuffer）写数据。
- BufferedWriter 类：为其他字符输出流提供写缓冲区。
- PipedWriter 类：连接到一个 PipedReader。
- OutputStreamReader 类：将字节输出流转换为字符输出流，可以指定字符编码。

Writer类中的writer()方法和append()方法。

| 方法名及返回值类型                         | 说明                                                         |
| ------------------------------------------ | ------------------------------------------------------------ |
| void write(int c)                          | 向输出流中写入一个字符                                       |
| void write(char[] cbuf)                    | 把参数 cbuf 指定的字符数组中的所有字符写到输出流中           |
| void write(char[] cbuf,int off,int len)    | 把参数 cbuf 指定的字符数组中的若干字符写到输出流中。其中，off 指定 字符数组中的起始下标，len 表示元素个数 |
| void write(String str)                     | 向输出流中写入一个字符串                                     |
| void write(String str, int off,int len)    | 向输出流中写入一个字符串中的部分字符。其中，off 指定字符串中的起 始偏移量，len 表示字符个数 |
| append(char c)                             | 将参数 c 指定的字符添加到输出流中                            |
| append(charSequence esq)                   | 将参数 esq 指定的字符序列添加到输出流中                      |
| append(charSequence esq,int start,int end) | 将参数 esq 指定的字符序列的子序列添加到输出流中。其中，start 指定 子序列的第一个字符的索引，end 指定子序列中最后一个字符后面的字符 的索引，也就是说子序列的内容包含 start 索引处的字符，但不包括 end 索引处的字符 |

<font color="#900">Writer 类所有的方法在出错的情况下都会引发 IOException 异常。关闭一个流后，再对其进行任何操作都会产生错误。</font>