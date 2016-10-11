[TOC]

### 常见数据格式

- 例子:
	 我检测用户名是否已经存在
			 我就给客户端发送一个  username=zhagnsan;
	 服务端给我返回数据。
			 该用户名已经存在or改用户名可以使用


#### xml

xml: 可扩展的标记语言
	它是自定义的，也就是这个里面的标签不固定，我们自己去定义。
	只要按照xml 的语法去写就行。 xml 的语法跟html 的语法类似
```
<book>
	<bookName>
	</bookName>
</book>
```

xml 语法：
	1.xml 的文档声明 声明这个是一个xml格式的文档

```
		<?xml version="1.0"  encoding="UTF-8" ?>
		 <books>
			<bookName></bookName>
		 </books>
```
	2.有且仅有有个根元素
	3.可以嵌套，（可以自定义）xml的目的是用来做输出传递，并不是用来做数据展示.

```
	<?xml version="1.0" encoding="utf-8"?>
	<users>
		<user>
			<username>111</username>
			<age>1</age>
		</user>
		<user>
			<username>adsf</username>
			<age>11</age>
		 </user>
	</users>
```
### json

1. json 的数据格式
	以键值对的方式来表示.

```
$array=array(
	  array("username"=>"zhangsan",age=>11),
	  array("username"=>"lisi",age=>12
);

```

```
//以xml 来表示
<?xml  version="1.0" encoding="utf-8"?>
<users>
	 <user>
		<username>张三</username>
		<age>11</age>
	</user>
	 <user>
			<username>李四</username>
			<age>12</age>
	 </user>
</users>
```

```
//以 json格式
 一条记录: {"username":"张三","age":11}
	 多条记录:[ {"username":"张三","age":11},{"username":"李四","age":11}]
 json 格式
	 {"key":[{"username":"张三","age":11},{"username":"李四","age":11}]}
```

### 案例:练习复杂一点的json 数据格式(省市联动)


### 数据解析

```
转换有两种方式：
	1：通过我们的js 提供的一个函数  eval
		var data='{"username":"zhangsan","age":11}';
		var obj=eval("("+data+")")
	2:提供JSON.parse 解析
		var obj=JSON.parse(data);
	根据key可以获取到value，看value 对应的值是什么.
	var obj='{
				"username":["zhangsan","lisi","zhaoliu"],
				"users":[{"username":"congcong"},{"username":"laoduan "}],
				"bgm":{"username":"cc"} ,
				"run":"function(){}"}';
	obj=eval("("+obj+")"); //变成对象
	//找到zhaoliu
	obj.username[2];
	//找到laoduan
	obj.users[1].username
	//获取到cc
	obj.bgm.username
	//获取到
	obj.run()
```
### Ajax请求发送过程
```
		我一个页面有多个地方发送ajax 请求。
		而我们发送ajax 请求都是四步
			1.创建对象
			2.打开连接
			3.发送数据
			4.接收数据
			5.解析数据
	我既然一个页面有多个地方需要发送请求，就有多个地方使用
			这段逻辑
			1.创建对象
			2.打开连接
			3.发送数据
			4.接收数据
			5.解析数据

```

***

1:ajax 聊天案例代码的实现
2:xml 的数据格式规范
3:xml 数据格式解析思路
4:json 解析思路
5:使用javascript json 数据格式解析的两种方式(eval,JSON.parse)
6:省级联动代码思路











