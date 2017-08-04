# 会话控制 #

HTTP协议是一个无状态的协议。
    
服务器的不能区分出多次请求是否发送自同一个客户端，但是在事件开发中确实具有该需求，而且十分的迫切。
    
会话控制主要采用两个技术Cookie 和 Session
    
    
## Cookie ##

Cookie相当于服务器发送给浏览器的一张“票”，服务器将Cookie发送给浏览器以后，浏览器每次方法都会将Cookie发回，这样服务器就可以根据浏览器发回的Cookie来识别出不同的用户了。
    
### Cookie的使用流程： ###

1.服务器向浏览器发送Cookie
2.浏览器收到并将Cookie保存
3.浏览器带着Cookie向服务器发送请求
4.检查用户的Cookie
        
###  Cookie实际上就是一个头，服务器以响应头的形式将Cookie发送给浏览器 ###
Set-Cookie: name=sunwukong; Path=/
			
### 浏览器以请求头的形式将Cookie发回给服务器 ###
 Cookie: name=sunwukong
			
我们可以通过为不同的用户发送不同的Cookie来识别出用户
        
### cookie的有效期 ###

cookie也是有有效期，浏览器并不会一直保存Cookie
        
cookie的默认有效期是一次会话 会话指的是一次打开关闭浏览器的过程，一旦关闭浏览器cookie则会自动失效
				
### 设置cookie的有效期   ###
        
cookie的作用：
1.保存用户的登录状态
2.保存用户的用户名
 3.广告
        
### cookie不足 ###
1.cookie都是明文保存的，容易泄露用户的隐私
2.浏览器对于cookie的数量和大小都是有限制的，不能使用cookie保存过多的信息
3.cookie是由服务器发送给浏览器，再由浏览器发回给服务器，如果cookie过大会导致请求速度过慢，降低用户的体验。
        
### 示例代码 ###

    var express = require("express");
    var app = express();

    //引入cookie-parser中间件
    var cookieParser = require("cookie-parser");

    //将cookie-parser设置为中间件
    app.use(cookieParser());

    app.get("/sendCookie",function (req , res) {

    	//向客户端发送cookie
    	//res.cookie(name, value [, options])
    	//通过res.cookie()可以用来向浏览器发送cookie
    	//cookie实际上就是一个名值对的结果

	    //设置一个永久有效的cookie
    	res.cookie("name","sunwukong",{maxAge:1000*60*60*24*365*10});

	    res.send("Cookie已经发送给浏览器~~~");

    });
    
        app.get("/checkCookie",function (req , res) {

    	//获取用户发送的Cookie
    	var cookie = req.get("Cookie");

    	//当引入cookie-parser以后，在Request中会多一个cookies这个属性
    	//这个属性值是一个对象，它会将cookie中解析的内容转换为对象中的属性
    	console.log(req.cookies.name);

    	res.send("检查用户的Cookie");
    });

    app.get("/delCookie",function (req , res) {

    	//删除cookie
	    //使用一个有效期为0的cookie来替换已有cookie
    	//res.cookie("name","shaheshang",{maxAge:0});
    	res.clearCookie("name");
    
    	res.send("cookie已死~~");

    });

    app.listen(3000,function () {
    	console.log("OK");
    });
    
  
## session（会话） ##

为了解决cookie的缺陷所以引入了session机制。
    
session是基于cookie的，如果没有cookie，session无法使用。
    
### session的原理： ###

session将用户的数据统一保存到服务器中的一个对象（session对象）里，每一次会话都会有一个对应的对象用来保存数据，每一个session对象都会有一个唯一的id，我们会将id以cookie的形式发送给浏览器，浏览器只需要在发送请求时将cookie发回，即可找到它对应的session对象。
    
 Express原生不支持session，需要引入新的中间件

 需要使用 express-session 来让express支持session

使用步骤:
1.安装 npm install express-session --save
2.引入 var session = require("express-session");
3.设置为中间件
app.use(session())
                
session中数据的有效期就是一次会话，浏览器关闭session中的数据自动丢失。
    
### session的应用 ###
我们可以在用户登录成功以后，将用户信息保存到session对象中，这样我们就可以通过检查session中是否有用户信息，来判断用户是否登录。
    
### 示例代码 ###

    var express = require("express");
    var app = express();

	//引入cookie-parser中间件
    var cookieParser = require("cookie-parser");

    //引入express-session中间件
    var session = require("express-session");

    //将cookie-parser设置为中间件
    app.use(cookieParser());
    //将session设置为中间件
    app.use(session({
    	resave:false,
    	saveUninitialized:false,
    	secret:"hello"
    }));

    //创建一个路由来测试session
    app.get("/test01",function (req , res) {

        //当引入express-session以后，在Request中会多一个session这个属性
    	req.session.str = "向session存储的数据";

    	res.send("测试session");
    });

    app.get("/test02",function (req , res) {

    	res.send(req.session.str);
    });

    app.listen(3000,function () {
    	console.log("OK");
    });
