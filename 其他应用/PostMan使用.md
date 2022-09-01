# PostMan使用

## 简介

PostMan是一个用来进行servlet链接测试的软件，他还可以生成相应链接的接口文档，可以说是大大减少了我们的工作时间。b(￣▽￣)d

## 新建链接

![Inkedimage-20220527113920305_LI](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\Inkedimage-20220527113920305_LI.jpg)

1. 新建链接，然后创建新的请求。
2. 给请求起一个合适的名字
3. 设置响应的url，和请求方式，可选get和post
4. 设置传入的参数，填写备注是为了后期生成接口api
5. send一下，就可以看到响应的数据了。

## 设置环境变量

我们可以通过{{}}来调用相应的环境变量，这样可以使我们少写很多代码。

![image-20220527115002496](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220527115002496.png)

点击此按钮来创建新的环境变量。

![image-20220527115040549](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220527115040549.png)

之后点击这个小眼睛就可以设置响应的环境变量了，点击画圈的地方可以切换不同的环境变量。

## 生成接口API

首先需要去官网下载响应的运行文件，并且设置为环境变量。

之后导出接口的json文件，最后通过相应的的指令运行下载好的运行文件就会生成我们想要的API了。

```
生成在线html文档
docgen server -f C:\Users\admin\Desktop\api\api.json(json文件位置) -p 8000
生成在线markdown文档
docgen server -f C:\Users\admin\Desktop\api\api.json(json文件位置) -p 8000 -m
html文档
docgen build -i C:\Users\admin\Desktop\api\api.json(json文件位置) -o C:\Users\admin\Desktop\api\api.html(生成文档希望在的位置)
生成markdown文档
docgen build -i C:\Users\admin\Desktop\api\api.json(json文件位置) -o C:\Users\admin\Desktop\api\api.md -m(生成文档希望在的位置)
```

