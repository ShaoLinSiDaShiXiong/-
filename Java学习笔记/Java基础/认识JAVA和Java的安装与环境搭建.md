# 认识JAVA和Java的安装与环境搭建

## 认识Java

**首先Java总共分为三个体系，不同的体系所面向的对象，和作用的领域都是是不同的。**

### JAVA SE

Java SE（Java Platform Standard Edition，Java平台标准版）Java SE是我们学习和使用的Java体系，Java SE包含支持Java Web服务开发的类，并为Java EE提供基础，如 Java语言基础，JDBC操作，I/O操作，网络通信以及多线程等技术结构。

Java SE是允许开发和部署在桌面，服务器，嵌入式环境和实时环境中使用的。

![Java SE体系结构图](E:\笔记\img\Java SE体系结构图.jpg)

![Java SE体系结构图](G:\笔记\img\Java SE体系结构图.jpg)

### JAVA EE

Java EE（Java Platform Enterprise Edition，Java平台企业版本）JavaEE实在JavaSE的基础上构建的，他提供Web服务，组件模型，管理和通信API，可以用来实现企业级的卖你想服务体系结构（Service Oriented Architecture，SQA）和Web2.0用用程序。

他是企业版本帮助与开发的部署可移植，健壮，可伸缩且安全的服务器段Java应用程序。

### JAVA ME

Java ME是为在移动设备和嵌入式设备（比如手机，PDA，电视机机顶盒和打印机）上运行的应用程序提供一个健壮且灵活的环境。

## Java的安装

想要使用Java这门语言进行编程，首先要做的就是在自己的电脑上安装Java的运行环境，我们需要到oracle（甲骨文）官网上下载Java的jdk安装包。在这里我们可以进行版本的选择，目前比较新的Java稳定版本分别是Java的第8版本和第14版本（大概）。

当我们找到合适我们电脑操作系统的jdk版本之后，我们就可以进行安装了。

## Java的环境搭建

当我们安装好Java之后，想要进行Java编程，我们还需要搭建Java的运行时环境，首先找到我们安装好的Java文件目录中的jdk中bin目录所在的位置，复制好bin目录的绝对路径地址，之后打开此电脑属性的高级系统设置中的环境变量，找到Path，将我们复制好的地址粘贴到里面即可。

在这之后我们就可以使用cmd进行Java的编译过程了。

**需要注意的是，即使我们不进行Java的环境搭建，也是可以使用Java命令的，不过这需要我们进入jdk中的bin目录，才可以执行Java中的指令命令。**

## Java中JVM，JRE和JDK三者的区别

**他们三者之间的关系是JDK包含JRE包含JVM，等于说，我们只要下载了JavaJDK工具包，我们就可以进行Java的开发与运行了。**