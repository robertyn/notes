[TOC]
## 跨域
> 概念:我们叫做跨域名访问,域名不同就叫做跨域.
> 跨域属于浏览器的一种行为.因为浏览器认为不安全所以禁止.

#### 主域名相同跨域
```
http://www.itcast.cn/day11/code/cross/04cross.html
<iframe width="100%" src="http://wh.itcast.cn/cross.html"></iframe>
//解决方法:在两个页面js中都添加一句 document.domain="itcast.cn";
```



#### 关于dom 去获取另外的一个页面的元素.
```
var iframe=document.querySelector("#iframeId");
//我等 iframe 里面的内容加载完毕，触发
iframe.onload=function(){
     var contentWindow=this.contentWindow;
    //如果我能把字体颜色变红，说明一个问题，我就可以在同域当中不用进行处理，我就可以访问.
     contentWindow.document.querySelector("p").style.color="red";
}
```

#### 再来看一种方式的跨域：关于ajax
> 我通过ajax 访问，会存在跨域问题
http:/www.itcast.cn  去访问  通过xmlHttpRequest 这个对象去发送请求http://www.baidu.com  就会存在跨域问题域名都不相同，浏览器会觉得会有安全问题.

```
  $.ajax({
             url:"http://api.map.baidu.com/telematics/v3/weather",
             type:"get",
             data:{
                   location:cityName,
                   output:'json',
                   ak:'6tYzTvGZSOpYB5Oc2YGGOKt8'
             },
             /*预期服务器端返回的数据类型，假设我现在跨域了，我就改成jsonp 就可以了 */
           success:function(data){
             //百度那边的 数据已经回来，我现在要解析这个数据.
             var weatherData=data.results[0].weather_data;
             var obj={
                 list:weatherData
             }
             var html=template("templateId",obj);
             document.querySelector("table").innerHTML=html;
         }
     })
```
##### dataType:"jsonp"原理
>xmlhttpRequest 这个对象发送请求，如果请求的是另外的一个站点，
   浏览器对这个对象会有限制，所有我们是用创建一个script 标签，
   使用这个标签去发送请求。
> 1： 现在我们已经知道怎么去发送这个请求。
> 2： 不知道服务端的数据.
//当前页面xmlHttpRequest对象给其它的站点发送请求，有跨域
//我们使用script标签去发送请求。然后通过这样的一个回调函数把服务器端的数据获取到
//通过script 标签把一个函数名传递到服务器，服务器得到这个函数名
//把服务器要传递的数据跟这个函数进行组拼，组拼成方法调用的形式。
//发这个数据发送到客户端浏览器，客户端浏览器得到这个内容
//就以javascript 的方式去解析服务器端返回的数据
//这种方式我就们就可以通过jsonp 去解决
//jsonp 是用来解析xmlHttpRequest 对象的跨域.
//jsonp 的原理，就是通过script 标签来发送请求，接受数据



