
### 客户端与服务器进行交互，传递文件

文件上传.（客户端向服务器端传递数据）

文件上传对客户端的要求.
				1. 必须是表单提交
				2. 我必须有一个input 选项  它的类型是file
				3. 我必须是post 方式提交。
				4. 必须设置在表单上面设置一个属性  form   enctype="multipart/form-data";

文件上传在服务端怎么去获取数据.
				服务器去获取客户端的数据，
				假设客户端是以get 方式提交的数据 我就是用$_GET
				假设客户端是以post 方式提交的数据，我就是用$_POST
				假设客户端的数据是文件上传上传，我就是用  $_FILES

***

### http 协议.

协议.规定，要求，按照要求去找
规定了.客户端与服务器进行通讯的数据格式。

http 协议的数据分为两部分.

- 客户端发送给服务器的数据，我们称为请求的数据格式。（我假设在客户端浏览器发送一个http 请求，客户端浏览器会自动帮我封装数据格式，然后发送给服务器）

- 发送到服务器端的请求的数据格式分为四部分.（客户端发送服务器的数据）
	1.请求首行
	2.请求头 (请求头的名称，请求头的值)
	3.请求空行 (请求空行没有什么作用)
	4.请求体  （get 方式提交没有请求体）

- get 方式提交.
GET /day08/mycode/02array.html HTTP/1.1
Host  127.0.0.1
Cache-Control max-age=0
Upgrade-Insecure-Requests 1
User-Agent  Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.106 Safari/537.36
告诉服务器客户端浏览器接收的数据格式。
Accept  text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
//接受的编码，
Accept-Encoding gzip, deflate, sdch
//接收的语言.
Accept-Language zh-CN,zh;q=0.8
If-None-Match "1900000000036e-af-53c595c55c0ef"
If-Modified-Since Tue, 13 Sep 2016 01.16.22 GMT


- post 请求提交方式的数据格式.
/day07/mycode/12poPOSTst.php HTTP/1.1
Host. 127.0.0.1
Content-Length. 35
Cache-Control. max-age=0
Origin. http.//127.0.0.1
Upgrade-Insecure-Requests. 1
User-Agent. Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.106 Safari/537.36
//如果是post 提交，一定会有这个请求头，
Content-Type. application/x-www-form-urlencoded
Accept. text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
//请求来自于那个页面.
Referer. http.//127.0.0.1/day07/mycode/12post.html (作用.1.做广告流量统计 2.防盗链)
	Accept-Encoding. gzip, deflate
	Accept-Language. zh-CN,zh;q=0.8
	//请求体，这个请求体是发送到服务器的参数数据
	username=zhangsan&password=zhangsan

***

### **get  提交与post 提交的区别  （重点掌握）**

- get
> 1.get 提交请求的参数都在地址栏当中。不安全
> 2.get 提交没有请求体
> 3.get 提交因为请求都在地址栏当中，所以发送给服务器的数据的大小会有限制 1kb 左右

- post
> 1.post 提交请求参数都在请求体当中，数据大小没有限制
> 2.安全
> 3.它必须有一个特殊的请求头Content-Type."application/x-www-form-urlencoded";

### 服务器给客户端响应的数据，我们称为响应的数据格式。

- 响应的数据格式也分为四部分.
	响应首行，
	响应头
	响应空行
	响应体
	HTTP/1.1 200 OK
	Date. Tue, 13 Sep 2016 02.33.55 GMT
	Server. Apache/2.2.21 (Win32) PHP/5.3.10
	Last-Modified. Tue, 13 Sep 2016 01.16.22 GMT
	ETag. "1900000000036e-af-53c595c55c0ef"
	Accept-Ranges. bytes
	Content-Length. 175
	Content-Type. text/html

```
	<!DOCTYPE html>
	<html>
	<head lang="en">
			<meta charset="UTF-8">
			<title></title>
	</head>
	<body>
	<a href="02array.php">查询用户信息</a>
	</body>
	</html>
```


- 响应的数据的格式 （服务器给客户端浏览器）
 响应首行
 响应头
 响应空行
 响应体
 响应的协议版本
  200 响应的状态吗 代表成功
  404 请求的资源没有找到
  500 服务器内部错误
 HTTP/1.1 200 OK

>//告诉客户端浏览器服务器的时候
Date. Tue, 13 Sep 2016 02.33.55 GMT
//告诉客户端浏览器我服务器时候的版本
Server. Apache/2.2.21 (Win32) PHP/5.3.10
//最后修改时间.
Last-Modified. Tue, 13 Sep 2016 01.16.22 GMT
ETag. "1900000000036e-af-53c595c55c0ef"
Accept-Ranges. bytes
Content-Length. 175
//Content-Type.服务器给客户端浏览器的，告诉客户端浏览器，我的内容类型.
Content-Type. text/html;

```
		<!DOCTYPE html>
		<html>
		<head lang="en">
				<meta charset="UTF-8">
				<title></title>
		</head>
		<body>
		<a href="02array.php">查询用户信息</a>
		</body>
		</html>
```

### http 协议分为两大部分
- 客户端发送给服务器  (请求的数据格式)
 	1.请求首行
 	2.请求头
 	3.请求空行
 	4.请求体
 发送http 请求 我们常见的方式有两种，一种是get post
 	 get  没有请求体，发送到服务器端参数都在地址栏当中,不安全，数据大小有限制
   post 有请求体，发送到服务器端数据都在请求体当中,安全，数据大小没有限制。
   有一个特殊的请求头
 	 Content-Type."application/x-www-form-urlencoded";


- 服务器响应给客户端  （响应的 数据格式）
 	响应的数据格式四部分
  响应首行
 	状态200   ok
 	状态404  not find
 	状态500 服务器内部错误
 	响应头
 	//我服务器给客户端浏览器一个这样的响应头。
 	//客户端浏览器接受到这个响应头，5秒钟之后会自动跳转到百度.
 	Refresh.5;url=http.//www.baidu.com
 	响应空行
 	响应体
  假设我在php 当中通过echo 输出，内容都在响应体当中.就是html内容

***

### http 协议  约束客户端浏览器与服务器进行通讯。

	 这两者之间的数据交互都有一定的数据格式。
		客户端会给服务器发送一些数据
				 请求首行
				 请求头
				 请求空行
				 请求体
		服务器也会给客户端响应一些数据
				 响应首行
				 响应头
				 响应空行
				 响应体.
		 我给服务器发送一个请求，服务器可以给客户端发送响应头
				 我发送一个Refresh 的响应   refresh  5;url=http.//www.baidu.com
***
### ajax  (都是交互，只是交互的方式不一样)


- 同步交互:
  		我发送一个请求，服务器接受到请求，服务器要对请求进行处理，然后给客户端浏览器进行响应。
  			响应回来的页面会把之前的界面给覆盖掉.
  	 	我发送请求给服务器，服务器对我的请求进行处理，在处理的过程当中，我的客户端不能做其它的操作.
- 异步交互:
  		我发送一个请求给服务器，服务器接受到请求，服务器对请求进行处理，然后给客户端浏览器响应数据
  响应回来的数据不会覆盖原来的界面.
  		我发送请求给服务器，服务器对我的请求进行处理，在处理的过程当中，客户端还可以做其它的事情.

#### 交互过程

1.创建对象
	var xhr=new XMLHttpRequest();
2.打开连接
	xhr.open("GET","URL");
3.发送数据
	xhr.send(null); get 提交数据放在  路径的后面.
4.接收数据
	在xhr 对象上面绑定一个函数
//服务端在响应的过程当中都会调用这个函数.
	xhr.onreadystatechange=function(){
	//获取服务器端状态，如果服务器返回的 	状态等于4，代表服务器的数据已经响应完毕.
	//xhr.readyState
	//服务器返回的状态吗，如果200 代表的是成功，如果是404 代表的响应失败
	//xhr.status
	if(xhr.readyState==4 && xhr.status==200){
	//在这里获取数据. 获取服务器端返回的数据.
	xhr.responseText;
	}
}

***

例:
//我通过ajax 异步交互我可以完成一个什么样的效果.页面不刷新，就可以完成与服务器端数据交互.
						1.  ajax  get 提交
						2.  ajax post 提交
						3.  检测用户名是否已经存在.

## 内容总结

```
 //php 的动态输出,在一个php 页面可以写很多的
 <?php if(true){ ?>
 <?php }  ?>
 <? for($i=0;$i<=1000;$++){?>
 		<div></div>
 <?php ?>
```

- 把php 里面的一个数组动态输出.


```
				<?php  $array=array("1","2","3");  ?>
				<?php for($i=0;$i<count($array); $i++){?>
										<?php echo $array[$i]?>
				<?php } ?>
				<?php
								 $array=array(
												array("username"=>"zhangsan","age"=>11),
												array("username"=>"zhangsan","age"=>11),
												array("username"=>"zhangsan","age"=>11),
												array("username"=>"zhangsan","age"=>11)
								 )
				?>
			 <table>
						<tr>
										<td>姓名</td>
										<td>年龄</td>
						</tr>
						<?php for($j=0;$j<count($array); $j++){?>
										<tr>
												<?php foreach($array[$j] as $key=>$val){?>
																<td>
																			<?php echo $val; ?>
																</td>
												<?php }?>
										</tr>
						<?php }?>
			 </table>
```


- 客户端的要求.
					1.表单提交
					2.表单必须是post 提交
					3.input type=file
					4.enctype=multipart/form-data
服务端的要求.
接收数据一定是使用  $_FILES;
$_FILES 这个是一个数组，这个里面存放着客户端传递 到服务器端的数据.
我要把这个$_FILES 获取出来，存到我硬盘上面的某个位置.

***

1.php 动态输出
2.文件上传的对客户端的要求
3.文件上传服务器获取数据
4.http 协议请求的数据格式四大部分
5.http 协议响应的数据格式四大部分
5.get 提交与post 提交的区别
6.同步交互与异步交互的概念
7.ajax 交互的四个步骤
8.ajax get 与post 方式提交
9.检测用户名是否已经存在






























