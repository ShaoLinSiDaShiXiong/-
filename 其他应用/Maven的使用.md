

# Maven的使用

**Mven的安装与基本配置：https://baijiahao.baidu.com/s?id=1672782610709450638&wfr=spider&for=pc**

## Maven学习

### Maven Pom

POM（Project Object Model，项目对象模型）是Maven的基本组件，它以xml文件的形式存放在项目的根目录下。

当Maven执行一个任务时，会先查找当前项目下的POM.xml文件，读取多需要的配置信息，然后执行任务。

**POM文件中可以设置的配置如下：**

- 项目依赖
- 插件
- 目标
- 构建时的配置文件
- 版本
- 开发者
- 邮箱列表

**POM示例：**

```xml
<project xmlns="http://maven.apche.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>net.biancheng.www</groupId>
    <artifactId>maven</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</project>
```

这三个元素是一个mavenPOM文件必须拥有的三个元素。

| 节点      | 描述                                                         |
| --------- | ------------------------------------------------------------ |
| groupId   | 项目组ID，定义档期那maven项目隶属的组织或公司，通常是唯一的。它的取值一般是项目所属公司或组织的网址或URL的反写，例如net.biancheng.www。 |
| artiactId | 项目ID，通常是项目的名称，groupId和ArtifactId一起定义了项目在仓库中的位置。 |
| version   | 项目版本。                                                   |

#### SuperPOM

所有的POM文件都继承自一个父POM，他包含了一些可以 被继承的默认设置。我们可以进行覆盖操作。

## Maven的安装

Maven是一个基于Java的项目管理工具，因此最基本的要求是在计算机上安装JDK，安装使用JDK要求最低是JDK7.0。

我们需要在官网上下载Maven **https://maven.apache.org/download.cgi**下载Mave。这里需要注意到的是不同的操作系统上，需要安装不同的安装包，Windows操作系统需要安装以zip为后缀的安装包，在Linux系统和Mac os上都是以tra结尾的安装包。

安装之后在Path中加入Maven的bin目录的绝对路径。

## Maven的相关配置

- lib：库文件
- bin：可执行文件
- conf：最重要的，核心代码。

**我们自己想要更好的使用Maven需要做一些相关配置，在conf下的setting.xml文件中更改相关设置。**

**做好以下几个配置可以更方便的使用Maven：**

- **配置本地仓库：**就是第三方jar包的存放位置，这是一定需要配置的，一个maven项目创建好后，如果需要jar包，它会优先去本地仓库去找。我们可以将jar包放到专门的地方，方便管理。

  **如果本地仓库有该jar包，就直接使用，没有网络也能引入。**

  **如果本地仓库没有该jar包，就需要去中央仓库或者私服中去下载。**

  ```xml
  <settings xmlns="http://maven.apache.org/SETTINGS/1.2.0"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.2.0 https://maven.apache.org/xsd/settings-1.2.0.xsd">
    <!-- localRepository
     | The path to the local repository maven will use to store artifacts.
     |
     | Default: ${user.home}/.m2/repository
    <localRepository>/path/to/local/repo</localRepository>
    -->
  <localRepository>D:\Maven\jar<localRepository>
  ```

  要在<setting>标签中创建<localRepsitort>（本地仓库），里面填上需要放jar包的文件夹的绝对路径，这里将本地仓库的地址设置为在了d盘中。

- **配置私服：**maven所有的jar包都是从中央仓库下载的，是国外提供的一个资源库。但是在国内这种网络条件下，去访问国外的网站是比较慢的，所以私服就出来了。

  ```xml
    <mirrors>
      <!-- mirror
       | Specifies a repository mirror site to use instead of a given repository. The repository that
       | this mirror serves has an ID that matches the mirrorOf element of this mirror. IDs are used
       | for inheritance and direct lookup purposes, and must be unique across the set of mirrors.
       |
      <mirror>
        <id>mirrorId</id>
        <mirrorOf>repositoryId</mirrorOf>
        <name>Human Readable Name for this Mirror.</name>
        <url>http://my.repository.com/repo/path</url>
      </mirror>
       -->
      <mirror>
        <id>aliyunmaven</id>
        <mirrorOf>*</mirrorOf>
        <name>阿里云公共仓库</name>
        <url>https://maven.aliyun.com/repository/public</url>
        <blocked>true</blocked>
      </mirror>
    </mirrors>
  ```

  找到<mirrors>标签，在该标签下配置私服。

  阿里巴巴作为国内顶尖的互联网企业，就提供了一个公共代理仓库，配置阿里云私服即可。**https://maven.aliyun.com/repository/public**

  当然有的企业也会配置属于自己的私服。

- **配置jdk版本：**maven默认的版本是jdk1.4我们只需要将jdk后面的数字改成需要的版本就好了。

  ```xml
      <profile>
        <id>jdk-11</id>
  
        <activation>
          <jdk>11</jdk>
        </activation>
  
        <repositories>
          <repository>
            <id>jdk11</id>
            <name>Repository for JDK 11 builds</name>
            <url>http://www.myhost.com/maven/jdk11</url>
            <layout>default</layout>
            <snapshotPolicy>always</snapshotPolicy>
          </repository>
        </repositories>
      </profile>
  ```

  这里我选择的版本是jdk11。

## 在eclipse中使用Maven

## 在pom.xml中添加所需要的jar包

**pom文件配置详解：https://www.cnblogs.com/tanghaoran-blog/p/10429329.html**

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>li</groupId>
  <artifactId>li</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <dependencies>
  	<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.28</version>
</dependency>
  	
  </dependencies>
</project>
```

**首先先找到需要下载的jar包的Maven依赖，在pom文件中创建<dependencies>标签,maven的jar包依赖都是放在这个标签里面的。**

**jar包依赖链接复制地址：https://mvnrepository.com/**

****



## Eclipse构建MavenWeb项目

在eclipse中可以进行动态Web的项目构建，但是当我们要使用某些jar包的时候会很麻烦，这个时候如果使用Maven来进行项目的构建就能解决这类麻烦了。

**想要使用Maven来进行动态Web项目的构建有一下几点需要注意：**

1. **打开包方式设置为war**
2. **修改pom.xml文件的配置**
3. **更改Java版本和动态页面的模型版本**
4. **添加web.xml文件**

### 创建Maven项目

![image-20220429113149380](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220429113149380.png)



****

## Maven项目中的异常以及处理

### Maven项目pom文件第一行报错

![](C:\Users\SaoLinSiDaShiXiong\Pictures\笔记图片\2338988-20210926133219814-1763410218.png)

**出现这个错误的原因是Eclipse版本和Maven版本不一致 ，Maven中包含由Maven-war-plugin插件，插件版本太低**

**可以通过在pom.xml文件中的build标签中加入代码来解决：**

```xml
	<build>
		<finalName>lzyt</finalName>
		<plugins>
		<plugin>
			<groupId>org.apache.maven.plugins</groupId>
			<artifactId>maven-war-plugin</artifactId>
			<version>3.3.1</version>
		</plugin>
	</plugins>
	</build>
```

添加完以上代码之后  右键项目==>Maven==>Update Project就不会在报错了。

![image-20220320135317823](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220320135317823.png)

## eclipse构建mavenweb项目

