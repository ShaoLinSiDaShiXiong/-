# Vue学习

Vue.js（读音 /vjuː/, 类似于 view） 是一套构建用户界面的渐进式框架。

Vue 只关注视图层， 采用自底向上增量开发的设计。

Vue 的目标是通过尽可能简单的 API 实现响应的数据绑定和组合的视图组件

## Vue安装

我们可以从一下链接获得vue的代码，复制之后保存成本地的js文件即可，用法类似jquery。

- **Staticfile CDN（国内）** : https://cdn.staticfile.org/vue/2.2.2/vue.min.js
- **unpkg**：https://unpkg.com/vue@2.6.14/dist/vue.min.js。
- **cdnjs** : https://cdnjs.cloudflare.com/ajax/libs/vue/2.1.8/vue.min.js



## Vue使用基础

**一个Vue构造器中需要以下内容：**

```html
   <script type="text/javascript">
        //创建包含数据信息的json数据
        var data = { test1: "aaa", test2: "hello", url:"http://www.baidu.com", user: false,className:"class2",i:1,d:{a:"aaa",b:"bbb"}};//此数据必须声明为data


        //实例化Vue，可以有多个vue实例
        var ve2 = new Vue({
            el:"#a",
            data:data
        });
       
        var ve = new Vue({
            el: "#vue_test",
            data: data,
            methods: {
                t1: function () {
                    return "一个字符串"
                }
            }
        });
    </script>
```

<font color="#F00">**我们可以创建多个vue实例，但是需要使用多个script标签分开。每个vue实例都可以看作是一个组件**</font>

```html
<div id="my_vue1">
    <div v-html="v1">
        <div id="my_vue2">
        	<p>{{v1}}</p>
            <p>{{v4}}</p>
        </div>
    </div>
</div>

<script>
	var ve = new Vue({
        el:"#my_vue1",
        data:{
            v1:"v",
            v2:"php",
            v3:"c++"
        }
    });
</script>
<script>
	var ve = new Vue({
        el:"#my_vue2",
        data:{
            v1:"hello",
            v2:"你好",
            v4:"java"
        }
    });
</script>
```

**这里在一个vue实例中又嵌套了另外一个vue实例如果data中属性名相同的话页面上会显示最外面vue实例中的属性，要是属性名不同就会调取相应vue实例中的信息。**

- **el：**

  该值参数id，只要有元素使用了该id那么该元素就交由该Vue对象进行处理。**需要注意，只有该元素内的内容是可以由vue进行干预的，该元素之外的元素不受影响。**

  <font color="#F00">这里的el是一个选择器，可以是一个id也可以是class或元素选择器</font>

- **data：**

  该参数用于指定属性，所有属性由大括号包裹，该属性可以由外部提前指定，该属性是以json格式存在的，可以存储字符串，数组和对象。**上面代码使用了先声明data变量后面在赋值给vue对象的方法，这里需要注意，赋值给data属性的变量名必须为data，否则vue不会接收该数据对象。**

- **methods：**

  methods用来定义函数，所有函数用大括号进行包裹，大括号内可以包含多个函数，每个函数之间使用逗号进行分割，return用来返回函数值。

- **{}：**

  **{{ }}** 用于输出对象属性和函数返回值。

## Vue模板语法

Vue.js 使用了基于 HTML 的模板语法，允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据。

Vue.js 的核心是一个允许你采用简洁的模板语法来声明式的将数据渲染进 DOM 的系统。

结合响应系统，在应用状态改变时， Vue 能够智能地计算出重新渲染组件的最小代价并应用到 DOM 操作上。

**Vue.js模板语法的使用是在使用vue对象id的标签或子标签内部添加属性**

```html
<script>
	var ve = new Vue({
        el:"#my_vue",
       	data:{
              v1:"hello",
              v2:"你好",
              v3:"java",
              url:"http://www.baidu.com",
              style:"color:#F00",
              ok:true,
              no:false,
              message: 'RUNOOB'
         }
    });
    function a(){
      alert("警告");  
    };
</script>
```



#### 插值

##### 文本：{{}}

文本插值应该在拥有相应id的标签内使用大括号来获取值（data）：

```html
<div id="my_vue">
    <p>{{v1}}</p>
</div>
```

##### html：v-html

使用v-html用于在标签内部插入值

```html
<div id="my_vue">
    <p v-html="v1"></p>
</div>
```

##### 属性：v-bind

使用vue的v-bind可以指定html属性：

```html
<div id="my_vue">
    <p v-bind:class="v3">java类</p>
</div>
```

这里指定了p元素的class属性为”class1“，只要是标签中可以又的属性，都可以通过v-bind进行声明例如：

```html
<div id="my_vue">
    <a v-bind:href="url">百度</a>
    <p v-bind:style="style">红色的p</p>
</div>
```

这里指定了href属性和style属性并且调用了vue实例中data中的值。

##### 表达式

vue.js支持javascript中的所有表达式：

```html
<div id="my_vue">
    {{5+5}}<br>
    {{ ok ? 'YES' : 'NO' }}<br>
    {{ message.split('').reverse().join('') }}
    <div v-bind:id="'list-' + id">菜鸟教程</div>
</div>
```

##### 指令：v-if

指令相当于jsp中的if表达式，通过指令可以空值属性是否被显示：

```html
<div id="my_vue">
    <p v-if="no">不会被显示的标签</p>
</div>
```

这样这个p标签就不会被显示在页面上。

##### 事件监听器：v-on

 v-on 指令，它用于监听 DOM 事件：

```html
<div id="my_vue">
    <span v-on:click="a">一个警告</span>
</div>
```

这里点击文字就会弹出一个弹窗警告

##### 用户输入：v-model

**`v-model` 指令用来在 input、select、textarea、checkbox、radio 等表单控件元素上创建双向数据绑定，根据表单上的值，自动更新绑定的元素的值。**

在 input 输入框中我们可以使用 v-model 指令来实现双向数据绑定：

```html
<div id="my_vue">
    <p>{{message}}</p>
    <input type="text" v-model="message"/>
</div>
```

这里只要在输入框中输入内容，该vue实例中的message内容就会发生改变。

##### 缩写

###### v-bind缩写

```html
<!-- 完整语法 -->
<a v-bind:href="url"></a>
<!-- 缩写 -->
<a :href="url"></a>
```

###### v-on缩写

```html
<!-- 完整语法 -->
<a v-on:click="doSomething"></a>
<!-- 缩写 -->
<a @click="doSomething"></a>
```



##### 过滤器
