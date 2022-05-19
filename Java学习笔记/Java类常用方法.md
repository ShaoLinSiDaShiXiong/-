# Java类常用方法

## String类常用方法：

#### 大小写转换：

<font color="#900">**相同字母的大小写ASSCII（阿斯克码）之间的差值是32.可以通过这个特性来进行大小写的转换。**</font>

```java
import java.util.Scanner;
public class Letter {
	public static void main(String[] args) {
		System.out.print("请输入一个字母：");
		Scanner sc = new Scanner(System.in);
		char xx = sc.next().charAt(0);
		if(xx >='a' && xx <= 'z') {
			xx = (char)(xx-32);     //将转换成的大写字母的ASCII数字用char转换成大写字母输出
			System.out.println("转换成大写为："+xx);
		}
		else
			System.out.println("输入不是小写字母："+xx);
		
		System.out.print("请再输入一个字母：");
		Scanner st = new Scanner(System.in);
		char dx = sc.next().charAt(0);
		if(dx >='A' && dx <= 'Z') {
			dx = (char)(dx + 32);
			System.out.println("转换成小写为："+dx);
		}
		else
			System.out.println("输入不是大写字母："+dx);
	}
}

```



- **大写字母转小写字母：<font color="#900">String.toLowerCase()</font>**

  调用toLowerCase()方法可以将大写字母转换成小写字母，字母以外的字符不受影响

  ```java
  String str = "ABCD";
  System.out.println(str.toLwerCase());
  ```

  

- **小写字母转大写字母：<font color="#900">String.toUpperCase()</font>**

  ```java
  String str = "abcd";
  System.out.println(str.toUpperCase());
  ```

  

#### 字符串截取方式：

- **通过spilt()截取字符串：**

  ```java
  String str = "123456@qq.com";
  String[] sarr = str.split("@");
  for(String ss : sarr){
      System.out.println(aa);
  }
  //运行结果：123456     qq.com
  ```

- **通过subString(int beginIndex)方法来截取字符串：**

  ```java
  String str = "abcdef";
  String s = str.subString(2);
  System.out.println(s);
  //输出结果： cdef
  ```

  *此方法通过传入的字符串下标来截取字符串，一直到字符串末尾，下标索引以0开头。*

- **通过传入两个参数的subString(int beginIndex,int endIndex)方法截取字符串：**

  ```java
  String str = "123456@qq.com";
  String s = str.subString(0,6);
  System.Out.println(s);
  //输出结果 123456
  ```

  *此方法传入的两个参数第一个是字符串开始的下标，第二个是字符串结束的下标，最后会返回一的字符串包含下标从beginIndex开始到endIndex下标之前一位的字符串。*<font color="#900">截取的字符串不包含下标endIndex的字符。</font>

- **通过subString方法根据某个字符截取字符串：**

  ```java
  String str = "123456@qq.com";
  String s = str.subStrig(0,str.indexOf("@"));
  System.out.prinln(s);
  //运行结果： 123456
  ```

  *indexOf(String str)方法返回的是子字符串第一次出现在字符串的索引位置，上面的代码返回的是@前面的字符。*



****

#### 判断字符串以指定字符结尾endsWith()

```java
String str = "hello";
boolean flag1 = s.endsWith("o");
boolean flag2 = s.endsWith("llo");
boolean flag2 = s.endsWith("l");

System.out.println(flag1);
System.out.println(flag2);
System.out.println(flag3);

//输出结果为 true true false
```



****

## StringBuffer

