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

<font color="#900">**这里使用的是MD5的加密方式，Java平台支持MD5，SHA-1，SHA-256，三种算法。**</font>