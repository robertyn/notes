[TOC]
## 复习

### 基础知识
1. bs 架构与cs 架构
2. 客户端
3. 服务端
4. 客户端与服务端要进行通讯，数据就需要走网络，然后学习网络
	 ip   域名， dns，端口
5. 计算机   安装一个操作系统，对外提供web 服务器，就需要安装web 服务器
	 web 服务器
				apache ，tomcat，nodejs
	 wamp windows  apache mysql php  （集成软件，里面包含了这三个软件）

### 软件安装

1. 配置了允许所有的用户可以访问我的服务器  (Allow from all)

2. 配置了一个网站的根目录，就是客户端访问我的服务器，默认去查找我服务器的那个盘里面的页面.
								1:178 行
								2:205行
				 --------------------------------------------
3. 配置域名
		第一步:windows 下面的system  hosts 文件
		第二步:apache 下面  httpd.conf 第467行的注释打开
		第三步:配置 conf/extra/httpd-vhost.conf
				拷贝，然后修改.


### 动态资源与静态资源
> 动态资源：需要被服务器转换，转换成了静态资源。
静态资源：浏览器可以直接解析的。
我们以后要使用web 服务器，这个web 服务器一定要具备转换php 的能力，你的php 才能部署上去。

### PHP
- 新建一个php，后缀.php 因为你之后后缀是.php,放在wamp 上面，我访问这个php，所以这个服务器才会转换
1. 定义变量 $username="zhangsan";
2. echo  $username

#### 变量的类型
##### 数组
######普通数组
$array=array("","","");
######关联数组
$array11=array("username"=>"zhangsan","age"=>11)
######二维数组
$array2=array(
array("username"=>"zhangsan3","age"=>11),
array("username"=>"zhangsan2","age"=>12),
array("username"=>"zhangsan1","age"=>13)
);
5.字符串拼接，我们使用  点"."
#### 函数
```
 function sayHello($username="zhangsan"){
 echo ""
 }
 sayHello();
```
#### 向客户端输出

>echo    输出字符串
>print_r 输出数组或者对象
>var_dump 数组数组的详细信息.

#### 常见的函数

> count() 统计数组的长度
> in_Array 判断数组当中是否存在某个元素
> array_key_exists 判断数组当中是否存在某个key
> file_get_contents 读取文件里面的内容转换成字符串.


### 客户端 与服务端进行交互.
> 客户端：发送请求
> 第一步:通过浏览器地址栏输入一个地址  get
> 第二步:点击一个超链接   get
> 第三步:表单提交    get  ，post

### 两种提交方式   get  ，post
##### 发送参数:
> get 在地址的后面：
13demo.php?username=zhangsan&age=11

> post 表单提交。自动把参数发送给服务器.

>服务端：
接收客户端的数据，我们只需要调给我们提供的一些变量把客户端的可以获取到
$_GET 这个里面存放客户端以get 方式提交的数据
$_POST 这个里面存放客户端以post 方式提交的数据.
php 里面的代码动态输出.


