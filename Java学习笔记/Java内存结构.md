# Java内存结构

**Java程序是交由JVM执行的，所以我们在谈Java内存区域划分的时候实际上是指JVM内存区域划分。**

**Java程序的执行顺序是这样的：**

1. Java源代码文件(.java)。
2. Java字节码文件(.class)，通过Java编译器（Java Compiler）编译之后的.java文件。
3. 类加载器(Class Loader)。
4. 运行时数据区(Runtime Data Area)。
5. 执行引擎(Exceution Engine)。

**首先java源代码会被java编译器编译为字节码文件，然后由JVM中的类加载器加载各个类的字节码文件，加载完毕后交给JVM进行引擎执行。在这整个过程JVM会用一段空间来存储程序执行期间需要用到的数据和相关信息，这段空间就被我们成为 Runtime Data Area（运行时数据区）我们常说的内存管理就是真对这段空间进行管理。**

****

