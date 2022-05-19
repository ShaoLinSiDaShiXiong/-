# Java问题

**2022/2/14	**

**https://blog.csdn.net/weixin_43847596/article/details/106137612**

```java
public Student queryStudent(int id) {
		Student stu = null;
		String sql = "SELECT * FROM student WHERE id=?";
		
		PreparedStatement ps = null;
		ResultSet rs = null;
		try {
			ps = conn.prepareStatement(sql);
			ps.setInt(1, id);
			rs = ps.executeQuery();
			if(rs.next()) {
				Student stu1 = new Student();//如果不在此代码块中添加student对象，会出现空针异常。
				stu1.setId(rs.getInt(1));
				stu1.setName(rs.getString(2));
				stu1.setAge(rs.getInt(3));
				stu1.setGender(rs.getString(4));
				stu1.setAddress(rs.getString(5));
				stu1.setId_number(rs.getString(6));
				stu = stu1;
			}
		} catch (SQLException e) {
			System.out.println("sql语句有误");
			e.printStackTrace();
		}finally {
			if(rs != null) {
				dbc.closeResultSet(rs);
			}
			if(ps != null) {
				dbc.closePreparedStatement(ps);
			}
		}
		
		return stu;
	}
```

## eclipse中文乱码

eclipse默认的字符保存格式是gbk，在使用Servlet的时候如果也页面设置的字符格式是utf-8就会出现中文乱码的情况。

![image-20220323113459916](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220323113459916.png)

![image-20220323113442134](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220323113442134.png)

这个时候只要更该eclipse中的默认字符编码格式就可以解决此问题了。

![image-20220323113630728](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220323113630728.png)

<font color="#900">**需要注意的是，如果使用了utf-8的字符集，那么以前的中文都会出现乱码。**</font>
