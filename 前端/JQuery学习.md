# jQuery 学习

## 引入jQuery

1. 直接引入网上已经存在的库
    ```
    <head>
      <script src="https://apps.bdimg.com/libs/jquery/2.1.4/jquery.min.js">
      </script>
    </head>
    ```

2. 直接引入已经下载好的库
    ```

    ```


## jQuery发起ajax请求

```
$.ajax({
    url:"/student/update_student",
    data:"id=1",
    type:"POST",
    success:function(data){

    },
    error:function(data){

    }
  })
```
- url：请求地址
- data：请求时携带的数据
- type：请求方式
- success:function：请求成功后执行的方法
- error:function：请求失败之后执行的方法

**通过Ajax发送form表单**
```
$.ajax({
    url:"/student/update_student",
    data:$("#form-member-add").serialize(),
    type:"POST",
    success:function(data){

    },
    error:function(data){

    }
  })
```
通过调用`form.serialize()`方法来将from表单中的元素放到请求中。
该方法的原理就是将表单内容序列化成键值对的样子。
