[TOC]

### jQuery中的ajax方法

```
$.ajax({
    url:"01ajax.php",
    type:"get",
    //data 是发送到后台的参数的数据，这个是第一种写法
    //data:"username=zhangsan&age=11&sex=nan",
    //第二种写法，以对象的方式把数据发送到服务端.
    data:{
         username:"wangwu",
         age:11
    },
    //超时，我现在给服务器发送一个请求，假设服务器过一段时间还没有给我
    //响应，我就断开这个连接
    /* timeout:3000, */
    //请求发送之前调用.
    beforeSend:function(){
    alert("请求发送之前调用");
    //这个函数如果没有返回值，我的执行顺序
    //beforeSend,success,complete
    //调用不会再去发送请求了.
    return false;
   },
    //这个回调函数，是请求响应完成，并且响应成功的 时候调用.
        success:function(data){
            alert("请求成功的时候调用");
        },
	//还有一些回调函数，请求失败的时候调用
        error:function(){
               alert("请求失败的时候调用");
        },
        //完成的意思，请求响应完毕之后调用.
        complete:function(){
              alert("请求响应完成");
        }
    })
```

### jQuery中的ajax六种方法
 jQuery封装了ajax操作，提供了一套api出来，它底层肯定是封装了xmlHttpRequest 这个对象
 jQuery 给我们提供了六个方法让我们来操作ajax ，跟后台进行数据交互。坦白说就从工作的角度来讲，会一个就可以。

```
方法一:$.ajax({
            url:"",
            type:"",
            data:""
            data:{
            }
            timeout:超时时间
            beforeSend 请求发送之前调用，如果返回的是false，就不发送请求了，对数据进行一些校验
            success: 请求成功的时候调用，我们一般在这里获取数据，解析数据，把数据放到页面上面
            error:请求失败的时候调用，我们一般是给一些用户友好的提示
            complete：请求结束的时候调用，一般我们在这里重置一些.
      })

方法二:$.get("url",{},function(data){
      });

方法三:$.post("url",{},function(){
 		});
      //默认是get方式提交，如果给服务器端发送参数，就是post 方式提交.
方法四:$("div").load("") 去载入服务端的内容放在当前元素里面。

方法五:$.getScript() 远程去载入一段脚本
      //当我的一个页面非常庞大，我们不会一次性把所有的脚本文件都加载出来。
      //需要的时候我再去获取这段脚本文件.

方法六:$.getJSON 发送一个请求给服务器端，服务器返回的数据一定是json 格式的数据。

其他一：serialize() 序列化 将当前表单的输入项的内容序列化成一个可以发送到服务器端的数据格式的字符串。
其他二：serializeArray()  序列化表单输入项的内容称为 一个数组,这个数组的数据也可以直接通过jQuery 发送到服务器.
```

### 模板
```
    1:模板是解决什么问题的
           我发送一个ajax 请求，服务器给我返回数据，我得到这个数据
    1：解析数据  （转换成javascript 对象）
    2：讲数据与标签组拼，然后放到页面上面去 遍历这个对象里面的数据，创建标签，跟标签进行组拼，然后放在页面。
    模板帮助解析数据，讲数据与标签组装。
    我们有很多的公司都提供了一些模板给我们使用
    我们使用的artTemplate ，我们需要去下载这个库  tempalte-native.js
    第一步：我需要在页面引入这个库 tempalte-native.js
    第二步：我要创建模板
           <% %> 用来写逻辑表达式
           <%=%> 向模板里面输出字符串
           <%for(var i=0;i<array.length;i++){%>
               <%=i%>
           <%}%>
    第三步：将数据与模板进行绑定
            传递的数据必须是一个对象
            template("templateId",mydata)
    第四步：返回数据，将数据写到页面
```

###做一个案例
```
           1：页面基本结构
           2：确定这个案例的功能
           3：根据这些功能找出对应的事件（事件是入口）
           4：事件确定出来方法，根据方法来写业务逻辑。
```


```

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
    table {
        width: 600px;
        border-collapse: collapse;
    }

    td {
        height: 40px;
        text-align: center;
        border: 1px solid #CCC;
    }
    </style>
    <script type="text/template" id="templateId">//模板定义在模板js之前
        <%for(var i=0;i<rows.length;i++){%>
            <tr>
                <td><%=rows[i].username%> </td>
                <td><%=rows[i].age%> </td>
                <td> <%=rows[i].sex%> </td>
                <td><%=rows[i].desc%> </td>
            </tr>
        <%}%>
    </script>
    <script src="js/jquery.min.js"></script>//jQuery文件
    <!--这个是腾讯的模板，用来解析js 数据，数据跟模板进行绑定.-->
    <script src="js/template-native.js"></script>//模板js文件
    <script>
    $(function() {
        $("#buttonId").on("click", function() {
            $.ajax({
                url: "01template.php",
                type: "get",
                success: function(data) {
                    var mydata = JSON.parse(data);
                    console.log(mydata);
                    var html = template("templateId", mydata);
                    $("table").append(html);
                }
            })
        });
    });
    </script>
</head>
<body>
    <input type="button" value="使用模板解析数据" id="buttonId">
    <table>
        <tr>
            <td>用户名</td>
            <td>年龄</td>
            <td>性别</td>
            <td>描述</td>
        </tr>
    </table>
</body>
</html>
```


```
//后台php文件
<?php
    $data= file_get_contents("user.txt");
    echo $data;
?>

```

```
user.txt中存放json数据,让php获取
```










