# Java加密

## MD5加密

```Java
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;

public class Test {
	public static void main(String[] args) {
		try {
			String a = "1234312";//需要进行加密的字符串
			MessageDigest md = MessageDigest.getInstance("MD5");//通过MessageDigest类的getInstance静态方法来获得指定摘要算法的MessageDigest对象。
			byte[] md5 = md.digest(a.getBytes());//将想要加密的字符串转换为byte数组，然后调用MessageDigest对象的digest方法来进行加密。
			for(byte b : md5) {
				System.out.print(b);
			}
		} catch (NoSuchAlgorithmException e) {
			e.printStackTrace();
		}
	}
```







****

## Base64加密

在Java8中，Base64比那吗已经成为Java类库的标准。

**Base64原理：** Base64编码方法，要求把每三个8Bit的字节转换为四个6Bit的字节，其中，转换之后的这四个字节中每6个有效bit为是有效数据，空余的那两个 bit用0补上成为一个字节。因此Base64所造成数据冗余不是很严重，Base64是当今比较流行的编码方法，因为它编起来速度快而且简单。



**Base64工具类提供了一套静态方法获取下面三种BASE64编解码器：**

- **基本：**输出被映射到一组字符A-Za-z0-9+/,编码不添加任何行标，输出的解码仅支持A-Za-z0-9+/。

- **URL：**输出映射到一组字符A-Za-z0-9+_，输出是URL和文件。
- **MIME：**输出隐射到MIME友好格式。输出每行不超过76字符，并且使用'\r'并跟随'\n'作为分割。编码输出最后没有行分割

### 内嵌类

| 序号 | 内嵌类 & 描述                                                |
| :--- | :----------------------------------------------------------- |
| 1    | **static class Base64.Decoder**该类实现一个解码器用于，使用 Base64 编码来解码字节数据。 |
| 2    | **static class Base64.Encoder**该类实现一个编码器，使用 Base64 编码来编码字节数据。 |

**通过调用这两个类来进行字符串的加密和解密**

### 方法

| 序号 | 方法名 & 描述                                                |
| :--- | :----------------------------------------------------------- |
| 1    | **static Base64.Decoder getDecoder()**返回一个 Base64.Decoder ，解码使用基本型 base64 编码方案。 |
| 2    | **static Base64.Encoder getEncoder()**返回一个 Base64.Encoder ，编码使用基本型 base64 编码方案。 |
| 3    | **static Base64.Decoder getMimeDecoder()**返回一个 Base64.Decoder ，解码使用 MIME 型 base64 编码方案。 |
| 4    | **static Base64.Encoder getMimeEncoder()**返回一个 Base64.Encoder ，编码使用 MIME 型 base64 编码方案。 |
| 5    | **static Base64.Encoder getMimeEncoder(int lineLength, byte[] lineSeparator)**返回一个 Base64.Encoder ，编码使用 MIME 型 base64 编码方案，可以通过参数指定每行的长度及行的分隔符。 |
| 6    | **static Base64.Decoder getUrlDecoder()**返回一个 Base64.Decoder ，解码使用 URL 和文件名安全型 base64 编码方案。 |
| 7    | **static Base64.Encoder getUrlEncoder()**返回一个 Base64.Encoder ，编码使用 URL 和文件名安全型 base64 编码方案。 |

**注意：**Base64 类的很多方法从 **java.lang.Object** 类继承。

<font color="#900">使用Base64进行数据的加密很简单，加密使用的Encode类，解密使用Decode类，每种加密解密都基本，URL和Mime三中方式。</font>

```java
import java.util.Base64;
import java.util.UUID;
import java.io.UnsupportedEncodingException;
 
public class Java8Tester {
   public static void main(String args[]){
      try {
        
         // 使用基本编码
         String base64encodedString = Base64.getEncoder().encodeToString("runoob?java8".getBytes("utf-8"));
         System.out.println("Base64 编码字符串 (基本) :" + base64encodedString);
        
         // 解码
         byte[] base64decodedBytes = Base64.getDecoder().decode(base64encodedString);
        
         System.out.println("原始字符串: " + new String(base64decodedBytes, "utf-8"));
         base64encodedString = Base64.getUrlEncoder().encodeToString("runoob?java8".getBytes("utf-8"));
         System.out.println("Base64 编码字符串 (URL) :" + base64encodedString);
        
         StringBuilder stringBuilder = new StringBuilder();
        
         for (int i = 0; i < 10; ++i) {
            stringBuilder.append(UUID.randomUUID().toString());
         }
        
         byte[] mimeBytes = stringBuilder.toString().getBytes("utf-8");
         String mimeEncodedString = Base64.getMimeEncoder().encodeToString(mimeBytes);
         System.out.println("Base64 编码字符串 (MIME) :" + mimeEncodedString);
         
      }catch(UnsupportedEncodingException e){
         System.out.println("Error :" + e.getMessage());
      }
   }
}
```

