# Java关键字与命名规范

**Java是中是区分大小的，任何一个字母的输入错误，都会导致Java在编译时出现编译错误。**

## 标识符

**Java中标识符是为方法，变量，或其他用户定义项所定义的名称，标识符可以有一个或多个字符。**

- 标识符可以由数字（0~9），字母（A~Z，a~z），美元符号（$），下划线(_)和Unicode字符集中符号大于0xC0的所有符号组合构成的。
- 标识符的一个符号可以是字母，下划线，和美元符号，后面可以是任何符合标准的标识符。
- 标识符不可以和关键字一样，且不能以数字开头，也不能赋予标识符任何标准的方法名。

## 关键字

**关键字是对编译器有特殊意义的固定单词，不能在程序中做其他目的的使用。关键字具有专门的意义和用途，和自定义的标识符不同，不能当作一般标识符使用。**

**Java语言目前定义了51个关键字，这些关键子不能作为变量名，类名，和方法名来使用。关键字目前可以被分为八大类。**

1. 基本类型：boolean，true，false，byte，short，int，long，float，double，null。
2. 访问控制：private，protected，public。
3. 类，方法和变量修饰符：abstract，class，extends，final，implements，interface，native，new，static，strictfp，synchronized，transient，volatile。
4. 程序控制：break，continue，return，do，while，if，else，for，instanceof，switch，case，default。
5. 异常处理：try，catch，throw，throws。
6. 包相关：import，package。
7. 变量引用：super，this，void
8. 保留字：goto，const。

## 几个容易忘记的关键的字作用

### 访问控制

1. protected 受保护的：

   protected关键字是可以应用于类，方法，或字符按（在类中声明的变量）的访问修饰控制符，对于protected的子女朋友来说，就是public的，可以自由使用，没有任何限制，对于其他的外部class，protected就变成private。

   **暂时没有搞清楚**

### 类方法变量修饰符

**https://wenku.baidu.com/view/31c7c89d4128915f804d2b160b4e767f5bcf800c.html**

**具体笔记**

1. native 本地：

   native关键字可以用于方法，以指示该方法是用Java以外的语言实现的。

   **因为不是经常使用的关键字，所以留作以后补全笔记。**

2. strictfp 严格，精准：

   strictfp的意思是FP-strict，也就是说精确浮点的意思，在Java虚拟机进行浮点运时，如果没有指定strictfp关键字，Java编译器以及运行换件在对浮点数运算的表达式是采取一种近似于我行我素的行为来完成这些操作，以至于得到的结果往往令人无法满意，而一旦使用了strictfp来声明一个类，接口，或者方法时，那么声明的范围内Java编译器以及运行环境会完全依照浮点规范IEEE-754来执行。因此如果想让浮点运算更加精确，而且不会因为不同的硬件平台所执行的结果不一致的话，那么就可以使用strictfp关键字。

   **可与i将一个类，接口以及方法名声明为strictfp，但是不允许对接口中的方法以及构造函数声明strictfp关键字。**

3. synchronized 线程，同步：

   synchronized关键字可以应用于方法或语句块，并为一次只应由一个线程执行的关键代码段提供保护。

   **synchronized关键字可以防止代码的关键代码段一次被多个线程执行，如果应用于静态方法，那么该方法一次由一个和线程执行时，整个类将被锁定。**

   **如果应用于实例方法，那么当发i方法一次由一个线程进行访问时，该实例将被锁定。**

   **如果应用于对象或数组，当关联的代码块一次由一个线程执行时，对象或数组将被锁定。**

4. transient 短暂：

   transient关键字可以应用于类的成员变量，以便指出该成员变量不应在包含它的类实例已序列化时被序列化。

5. volatile 易失：

   volatile关键字用于表示可以被多个线程异步修改的成员变量。

### 程序控制语句

1. instanceof 实例：

   instanceof关键字用来确定对象所属的类。

### 保留字

1. goto 跳转：

   goto保留关键字，但无任何作用。结构化程序设计完全不需要，goto语言即可完成各种流程，而goto语句的使用往往会使程序的可读性降低，所以Java不允许goto跳转。

2. const 静态：

   const保留字时一个类型修饰符，使用const声明的对象不能更新，于final有些类似。