# Java读取Excel

使用Java读取Excel内容需要导入jxl的jar包

## 导入依赖

**依赖：**

```xml
<dependency>
  <groupId>net.sourceforge.jexcelapi</groupId>
  <artifactId>jxl</artifactId>
  <version>2.6.12</version>
</dependency>
```

导入依赖之后，我们就可以通过jar包提供的类来对Excel来进行读取。

其中需进行读取的核心类有一下三个。

<font color="#F00">**此jar包只能用于xls后缀Excel文件的操作，如需要进行xlsx后缀Excel文件操作请导入POIjar包：**</font>

**依赖：**

```xml
  <!-- https://mvnrepository.com/artifact/org.apache.poi/poi-ooxml -->
  <dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.2</version>
  </dependency>
```

## 读取Excel进入Workbook

读取Excel文件的主要工具类有三个。

1. **读取Excel表所使用的类：**`import jxl.Workbook;`
2. **读取表格里的单元格的类：**`import jxl.Cell;`
3. **读取工作簿的类：**`import jxl.Sheet;`

### 生成Workbook实例

**通过`jxl`jar包进行操作时获取Workbook实例：**

```java
//获得相应的Excel文件
File Inputfile = new File("D:\\redisInput\\GPSINFO.xls");
//通过文件输入流来加载Excel文件
FileInputStream fileInputStream = new FileInputStream(Inputfile);
//使用workbook去接fileInputStream
Workbook workbook = Workbook.getWorkbook(fileInputStream);
```

**通过`POI`jar包进行操作时获取Workbook实例：**

POI和jxl获得Workbook实例方法大同小异，**唯一不同的是POI中需要调用Workbook类的构造方法，且Workbook类有两种类型，分别对应xlsx文件和xls文件**

```java
//生成xlsx后缀文件的workbook实例
logger.info("正常加载xlsx后缀Excel文件:" + excel);
workbook = new XSSFWorkbook(fileInputStream);
//生成xlsx后缀文件的workbook实例
logger.info("正常加载xls后缀Excel文件:" + excel);
workbook = new HSSFWorkbook(fileInputStream);
```

## 判断工作簿Sheet



330950367