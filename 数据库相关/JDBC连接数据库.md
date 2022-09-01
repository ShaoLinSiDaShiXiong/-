# JDBC连接数据库

**我们一般会将数据库操作的代码放在DAO层**

## DAO和Service

**DAO层一般指的是数据库的增删改查操作，我们一般将对数据库操作的实现类的代理类等和操作数据库的操作放在DAO层中**

**Service一般指的是业务层，业务和DAO的区别是，业务层没有增删改查。业务值得是一件事情进行的过程，比如说学生的报名和学费缴费，这些都是业务，而将业务产生的数据存入数据库就是DAO层要做的事情。**

****

**JDBC是（Java Database Connectivity）是一种执行SQL语句的JavaAPI。可以通过JDBC API连接到关系型数据库，使用SQL语句进行数据库操作。使用JDBC开发的软件可以访问不同的数据库，并在不同的平台上运行。**

## 数据库

**市面上有两种数据库类型：**

- 关系型数据库：所有的关系型数据库都是以表的形式存在的，按照一定的数据结构来存储数据，类似于表的形式。

  关系型数据库是建立在关系模型基础上的数据库，借助集合代数等概念和方法来处理数据库中的数据。

- 非关系型数据库：非关系型数据库NoSQL(Not Only SQL，不仅仅是SQL)，的数据通常是以对象的形式存储在数据库中，而对象之间的关系通过每个对象的自身属性来决定，Key—value的形式。

  非关系型数据库可以使用key-value，文档，图片形式进行存储，使用灵活应用场景广泛。

### 数据库组成部分

数据库系统是由在计算机系统中引入数据库后的系统。完整的数据库系统结构关系如下：

**用户 > 应用程序 > 应用开发工具 > 数据库管理系统 > 数据库**

## 使用Java连接MySQL

**想要使用Java连接进行MySQL操作需要进行一下几个步骤：**

1. 通过反射来加载驱动,在此之前一定要先保证有mysql的jar包。
2. 通过Connection来创建链接，创建连接需要 链接，用户名，密码。
3. 通过连接来获取statement对象。
4. 执行SQL语句。
5. 获取结果集。
6. 遍历结果集。
7. 按照开启的顺序，从最后开始依此关闭对象。

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
import java.sql.ResultSet;

public class Test{
    public static void main(String[] args){
        //1.通过反射加载驱动
        try{
            Class.forName("com.mysql.cj.jdbc.Drivaer");
        }catch(ClassNotFound c){
            System.out.println("驱动加载失败");
        }
            
        //2.通过Connection获取链接，这里需要使用DriverManager类，需要导包。
        
        String url = "jdbc:mysql://192.168.9.110(这里填入IP地址，也可以本地登录 填入localhost):3306(3306是本机端口的意思)/student(这里需要填入要使用的数据库名字)?allowPublicKeyRetrieval=true&serverTimezone=UTC&useSSL=false&useUnicode=true&characterEncoding=UTF-8";
        String user_name = "用户名";
        String pass_word = "密码";
        Connection conn = null;
        try{
            conn = DriverManager.getConnection(url,user_name,pass_word);
        }catch(SQLException s){
            System.out.println("链接加载失败");
        }
        
        
        //3.通过链接获取Statement对象。
        Statement stat = null;
        try{
            stat = conn.createStatement();
        }catch(SQLException s){
            System.out.println("获取Statement对象失败");
        }
        
        //4.执行SQL语句,SQL语句其实是不分大小写的。
        //SELECT 列名 FROM 表名
        String sql = "SELECT id,name,age,gender FROM student";
        ResultSet rs = null;
        try{
            //5.这里通过Statement对象获取结果集并执行sql语句。(execute是执行sql语句)
            rs = stat.executeQuery(sql);
        }catch(SQLException s){
            System.out.println("获取结果集失败");
        }
        
        //6.这里在这里便利结果集。
        //ResultSet类中的next方法可以返回一个Boolean值，从第一个开始，结果集中下一行如果有值则返回true，并且指向下一行值。
        try{
            while(rs.next()){
                //这里是从数据库中拿到第一项数据，这里的下标是从1开始，最后将得到的结果打印出来。完成之后指向下一列数据，直至所有数据打印完。
                int id = rs.getInt(1);
                String name = rs.getString(2);
                String age = rs.getString(3);
                String gender = rs.getString(4);
                System.out.println(id+"--"+name+"--"+age+"--"+gender);
            }
        }catch(SQLException s){
            System.out.println("获取结果集失败");
        }
        
        //7.最后一步很重要，依照打开的顺序依次关闭对象。
        try {
			rs.close();
		} catch (SQLException e1) {
			e1.printStackTrace();
		}
		try {
			stat.close();
		} catch (SQLException e) {
			e.printStackTrace();
		}
		try {
			conn.close();
		} catch (SQLException e) {
			e.printStackTrace();
		}   
    }
}
```

**以上就是JavaJDBC连接数据库的几步操作，只有当我们执行查询操作的时候才需要使用结果集来进行遍历。**



**以上步骤需要特别记忆的有：1.导入项目jar包。(这里后面可以使用maven进行架构)	2.通过反射加载驱动（Driver）3.创建链接（Connection）4.通过链接获得Setatement对象，这里也可以使用Prepared Statement对象，使用动态sql语句。5.执行sql语句，使用execute()方法。6.关闭开启的对象。**



**数据库连接范本（更改内容之后记得删除括号内的提示内容）：jdbc:mysql://192.168.9.110(这里填入IP地址，也可以本地登录 填入localhost):3306(3306是本机端口的意思)/student(这里需要填入要使用的数据库名字)?allowPublicKeyRetrieval=true&serverTimezone=UTC&useSSL=false&useUnicode=true&characterEncoding=UTF-8     （这是链接数据库要使用的链接规范）**

### PreparedStatement类

为了防止SQL注入，Java提供了一个专门的类来解决这个问题。

**PreparedStatement是预编译的，是参数动态化的SQL语句，上班主要用这个。因为是预编译的SQL语句，在使用时需要我们手动填入参数。**

**PreparedStatement的使用：**

```Java
//假设现在我们要向数据库中添加一个学生的信息
//此方法可以用作向数据库中添加学生信息，添加成功返回true，失败返回false
public boolean add(Student stu){
    boolean flag = false;
    Connection conn = null;
		String sql = "INSERT INTO student id,name,age,gender,address,id_number VALUES(?,?,?,?,?,?)";
    
    //这里的意思是在student表中添加信息，表结构是id,name,age,gender,address,id_number，VALUES括号内的？是要添加进表的信息，？和前面参数的顺序和多少一定要对应！！
		
    	PreparedStatement ps = null;//这里这样写是因为要抛出异常
		try {
			ps = conn.prepareStatement(sql);//这里就是添加SQL语句的参数。第一个参数指定的是？的位置,下标从1开始，第二个参数此方法参数列表中的Student对象，如果在正常程序中，此参数应该从用户处获取。
			ps.setInt(1, stu.getId);
			ps.setInt(2, stu.getName);
			ps.setInt(3, stu.getAge);
			ps.setInt(4, stu.getGender);
			ps.setInt(5, stu.getAddress);
			ps.setInt(6, stu.getId_number);
		} catch (SQLException e) {
			e.printStackTrace();
		}
}
```



## SQL语句

**一下SQL语句全部使用预编译参数动态化的SQL语句**。

**大写的都是SQL指令中的命令，不能更改，小写的都是可以改变的。**

**FROM后面跟着的都是表名，WHERE后面跟着的都是筛选条件**

- 添加SQL语句：

  INSERT INTO  student（要添加进入信息的表名） id,name,address（这里对应数据库中表的参数，数据库中是什么这里就是什么）VALUES(?,?,?)（这里的问号和前面的参数一一对应）

- 修改SQL语句：

  UPDATE student（表名）SET name=?,address=? WHERE id=?;（WHERE后面跟的是筛选条件，这段语句的意思是通过id修改name和address。SET后面跟的是需要修改的内容。）

- 删除SQL语句：

  DELETE FROM student（表名）WHERE id=?；（删除语句只需要给出条件就会根据条件删除符合条件的一列数据，这段SQL语句读起来就是   删除student表中的id是?的数据）
  
- 查询SQL语句：

  SELECT id,name,address FROM student（表名）WHERE id=?;（想要获得查询到的结果，就必须要使用ResultSet结果集来接收数据库中得到的数据） 

****

## 事务管理

**我们在使用Java使用JDBC操作数据库的时候有七步操作。**

**当我们在执行SQL语句的时候，会涉及到事务管理。开始执行SQL语句的时候会自动开启事务管理，执行完之后会自动关闭事务。**

**在我们在编程中进行服务层的操作时，可能会用到不只一次sql语句，如果在多个sql语句执行到一半的时候报错，这个时候会有几个语句执行成功，后边sql没有执行的情况发生。这样会导致我们的代码出现错误和不合理的情况。为了避免这种情况我们可以手动的进行事务的提交处理。**

<font color="#900">在Java的JDBC操作中处理事务都是通过Connection完成的。同一事务的所有的操作，都是在使用同一个Connection对象。JDBC的事务是默认开启的，并且是默认提交的。	JDBC Connection接口提供了两种事务模式，自动提交和手动提交。</font>

### **setAutoCommit(booelan)**：

<font color="#900">Connection类中的**setAutoCommit(booelan)**可以设置事务提交的状态，如果值为true则表示自动提交（默认值就是true），也就是每条sql语句都是一个单独的事务，如果设置成false，则需要手动提交。</font>

### commit()：

<font color="#900">conmmit()：提交事务，当事务状态是手动提交状态的时候就需要调用此方法来手动提交事务。如果在提交事务之前，sql语句出现错误，那么在setAutoCommit(booelan)方法和commit()方法之间的sql语句都不会执行。</font>

### rollback()：

<font color="#900">回滚结束事务</font>

```Java
try{
    //1.获取连接对象。
    conn = JDBC.getConnection();
    //2.开启事务
    //3.sql语句
    //4.获取预处理的sql语句PreparedStatement对象
    //5.赋值
    //6.执行sql语句
    //7.模拟异常
    //8.业务完成正擦汗给你提交。
}catch{
    
}
```





## JDBC常见错误

### JDBC不报错，但是也不执行

<font color="#900">**他奶奶的！一定是没有执行SQL语句！记得调用Statement对象的execute()方法**</font>
