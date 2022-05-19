# Ajax

**AJAX 是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。**

## AJAX工作原理

![AJAX](https://www.runoob.com/wp-content/uploads/2013/08/ajax.gif)

## 使用原生js来发送ajax请求

想要使用Ajax技术，需要知道一下几个步骤

1. **创建XMLHttpRequest对象**
2. **调用onreadystatechange事件**
3. **通过XMLHttpRequest对象的open方法来设置请求并通过send方法来发送请求。**
4. **通过检测请求是完成且相应已经准备就绪且页面状态为200来执行代码**
4. **通过responseText来获取响应内容**

**以上四个步骤就是js使用ajax的最基本的操作。代码如下：**

```html
 <script type="text/javascript">
            var xmlhttp;//需要获取的XMLHttpRequest对象
            if(windoow.XMLHttpRequest){//除IE5 IE6以外的浏览器XMLHttpRequest是window的子对象
                xmlhttp = new XMLHttpRequest();
            }else{
                // IE6, IE5 浏览器执行代码
                xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
            }


            //p1输入框失去焦点时调用此方法
            function myinput(){
                xmlhttp.open("post","findusername",true);//创建请求对象
                xmlhttp.send(null);//将请求发送到服务器
                if(xmlhttp.readyState == 4 && xmlhttp.status == 200){
                    var b = xmlhttp.responseText;
                    if(true == b){
                        document.getElementById("p1").innerHTML="该用户名已被注册";
                    }else{
                        document.getElementById("p1").innerHTML="a";
                    }
                }
            }
  </script>
```

当html页面的用户注册输入框失去焦点的时候就会将其中的信息通过ajax发送请求到服务器 ，然后获得响应内容，并且做出响应操作。

****

## jQuery使用Ajax

### $.ajax()

##### **1.url**: 

要求为[String类](https://so.csdn.net/so/search?q=String类&spm=1001.2101.3001.7020)型的参数，（默认为当前页地址）发送请求的地址。

##### **2.type**: 

要求为String类型的参数，请求方式（post或get）默认为get。注意其他http请求方法，例如put和delete也可以使用，但仅部分浏览器支持。

##### **3.timeout**: 

要求为Number类型的参数，设置请求超时时间（毫秒）。此设置将覆盖$.ajaxSetup()方法的全局设置。

##### **4.async**: 

要求为Boolean类型的参数，默认设置为true，所有请求均为异步请求。如果需要发送同步请求，请将此选项设置为false。注意，同步请求将锁住浏览器，用户其他操作必须等待请求完成才可以执行。

##### **5.cache**: 

要求为Boolean类型的参数，默认为true（当dataType为script时，默认为false），设置为false将不会从浏览器缓存中加载请求信息。

##### **6.data**: 

要求为Object或String类型的参数，发送到服务器的数据。如果已经不是字符串，将自动转换为字符串格式。get请求中将附加在url后。防止这种自动转换，可以查看　　processData选项。对象必须为key/value格式，例如{foo1:"bar1",foo2:"bar2"}转换为&foo1=bar1&foo2=bar2。如果是数组，JQuery将自动为不同值对应同一个名称。例如{foo:["bar1","bar2"]}转换为&foo=bar1&foo=bar2。

##### **7.dataType**: 

要求为String类型的参数，预期服务器返回的数据类型。如果不指定，JQuery将自动根据http包mime信息返回responseXML或responseText，并作为回调函数参数传递。可用的类型如下：
xml：返回XML文档，可用JQuery处理。
html：返回纯文本HTML信息；包含的script标签会在插入DOM时执行。
script：返回纯文本JavaScript代码。不会自动缓存结果。除非设置了cache参数。注意在远程请求时（不在同一个域下），所有post请求都将转为get请求。
json：返回JSON数据。
jsonp：JSONP格式。使用SONP形式调用函数时，例如myurl?callback=?，JQuery将自动替换后一个“?”为正确的函数名，以执行回调函数。
text：返回纯文本字符串。

##### **8.beforeSend**：

要求为Function类型的参数，发送请求前可以修改XMLHttpRequest对象的函数，例如添加自定义HTTP头。在beforeSend中如果返回false可以取消本次[ajax](https://so.csdn.net/so/search?q=ajax&spm=1001.2101.3001.7020)请求。XMLHttpRequest对象是惟一的参数。
      function(XMLHttpRequest){undefined
        this;  //调用本次ajax请求时传递的options参数
      }

##### **9.complete**：

要求为Function类型的参数，请求完成后调用的回调函数（请求成功或失败时均调用）。参数：XMLHttpRequest对象和一个描述成功请求类型的字符串。
     function(XMLHttpRequest, textStatus){undefined
       this;  //调用本次ajax请求时传递的options参数
     }

##### **10.success**：

要求为Function类型的参数，请求成功后调用的回调函数，有两个参数。
     (1)由服务器返回，并根据dataType参数进行处理后的数据。
     (2)描述状态的字符串。
     function(data, textStatus){undefined
      //data可能是xmlDoc、jsonObj、html、text等等
      this; //调用本次ajax请求时传递的options参数
     }

##### **11.error**:

要求为Function类型的参数，请求失败时被调用的函数。该函数有3个参数，即XMLHttpRequest对象、错误信息、捕获的错误对象(可选)。ajax事件函数如下：
    function(XMLHttpRequest, textStatus, errorThrown){undefined
     //通常情况下textStatus和errorThrown只有其中一个包含信息
     this;  //调用本次ajax请求时传递的options参数
    }

##### **12.contentType**：

要求为String类型的参数，当发送信息至服务器时，内容编码类型默认为"application/x-www-form-urlencoded"。该默认值适合大多数应用场合。

##### **13.dataFilter**：

要求为Function类型的参数，给Ajax返回的原始数据进行预处理的函数。提供data和type两个参数。data是Ajax返回的原始数据，type是调用jQuery.ajax时提供的dataType参数。函数返回的值将由jQuery进一步处理。
      function(data, type){undefined
        //返回处理后的数据
        return data;
      }

##### **14.dataFilter**：

要求为Function类型的参数，给Ajax返回的原始数据进行预处理的函数。提供data和type两个参数。data是Ajax返回的原始数据，type是调用jQuery.ajax时提供的dataType参数。函数返回的值将由jQuery进一步处理。
      function(data, type){undefined
        //返回处理后的数据
        return data;
      }

##### **15.global**：

要求为Boolean类型的参数，默认为true。表示是否触发全局ajax事件。设置为false将不会触发全局ajax事件，ajaxStart或ajaxStop可用于控制各种ajax事件。

##### **16.ifModified**：

要求为Boolean类型的参数，默认为false。仅在服务器数据改变时获取新数据。服务器数据改变判断的依据是Last-Modified头信息。默认值是false，即忽略头信息。

##### **17.jsonp**：

要求为String类型的参数，在一个jsonp请求中重写回调函数的名字。该值用来替代在"callback=?"这种GET或POST请求中URL参数里的"callback"部分，例如{jsonp:'onJsonPLoad'}会导致将"onJsonPLoad=?"传给服务器。

##### **18.username**：

要求为String类型的参数，用于响应HTTP访问认证请求的用户名。

##### **19.password**：

要求为String类型的参数，用于响应HTTP访问认证请求的密码。

##### **20.processData**：

要求为Boolean类型的参数，默认为true。默认情况下，发送的数据将被转换为对象（从技术角度来讲并非字符串）以配合默认内容类型"application/x-www-form-urlencoded"。如果要发送DOM树信息或者其他不希望转换的信息，请设置为false。

##### **21.scriptCharset**：

要求为String类型的参数，只有当请求时dataType为"jsonp"或者"script"，并且type是GET时才会用于强制修改字符集(charset)。通常在本地和远程的内容编码不同时使用。

```js
$(function(){
    $('#send').click(function(){
         $.ajax({
             type: "GET",
             url: "test.json",
             data: {username:$("#username").val(), content:$("#content").val()},
             dataType: "json",
             success: function(data){
                         $('#resText').empty();   //清空resText里面的所有内容
                         var html = ''; 
                         $.each(data, function(commentIndex, comment){
                               html += '<div class="comment"><h6>' + comment['username']
                                         + ':</h6><p class="para"' + comment['content']
                                         + '</p></div>';
                         });
                         $('#resText').html(html);
                      }
         });
    });
});
```



## Ajax通过jQuery遍历Servlet响应的JSON数据

**当我们通过$.ajax({})方法来进行ajax请求的时候，我们获得的响应（data）中的JSON数据是不可以直接进行$(jsonString).each()进行遍历的。需要将json对象进行解析，解析为js对象才可以正常遍历，否则会显示语法有误。**

<font color="#f80">**JSON字符串转换为JavaScript对象。要修复它，通过标准JSON.parse()或[jQuery](https://so.csdn.net/so/search?q=jQuery&spm=1001.2101.3001.7020) 的 $.parseJSON 将其转换为JavaScript对象。这里使用的是JSON.pares()方法进行解析**</font>

```javascript
	//点击a链接之后调用此方法发送请求
	function a(){
		console.log("aaa")
		$.ajax({
			"url" : "servlet",
			"type" : "post",
			"data" : "edit=0",
			"dataType" : "text",
			"success" : function(data){//如果请求成功，就将数据放在页面中
				var arrstr = data;
				//获取要放置信息的位置，放入无序列表
				var myul = "<ul id='myul'></ul>";
				$("#rightDiv").html(myul);

				//同过id来放置数据
				/* $.each(JSON.parse(data),function(index,object){//josn数据需要进行修复才可以进行遍历
					$("#myul").append("<li>"+this.zt+"</li> <a href='#'>编辑</a><a href='#'>删除</a>");
				}); */
				$(JSON.parse(arrstr)).each(function(){
					$("#myul").append("<li>"+this.zt+"</li> <a href='#'>编辑</a><a href='#'>删除</a>");
				});
			},
			"error" : function(){
				alert("请求有误");
			}
		
		});
	}
```

<font color="#f00">**这里需要注意的是，只有servlet传入的json对象需要进行解析，如果是json格式的数据，或者json文件则不需要进行解析，否则就会报出“Uncaught SyntaxError: Unexpected token u”此类错误。**</font>

**只有参数dataType是“text的情况下才需要这样操作，如果参数是json的情况下可以直接进行each()遍历。”**

*这里进行遍历数据又两种方式，其中$.each(data,function(index,object){});方式中，data是需要遍历的json对象，index是遍历当前的下标，object是当前对象。*
