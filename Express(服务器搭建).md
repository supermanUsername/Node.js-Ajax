# Express #
 
Express是Node中的web服务器框架，通过Express可以快速的在Node平台中搭建Web服务器
        
    // 安装Express并添加依赖npm install express --save
    
    // 引入express模块
    var express = require("express");
    
    // 创建应用对象
    var app = express();
    
    // 配置静态资源
    app.use(express.static("public"));
    
    // 创建路由
    app.get("/hello",function(request,response){
    // 参数：1路由映射的请求地址  2回调函数
    // request 表示客户端发送的请求报文，获取用户发送的信息
    // response 表示服务器发送的响应报文，用户返回的内容
    
    
    // 可以通过query来获取get请求的用户发送的信息
    var username = request.query.username;
    
    // send() 用于设置响应体
    response.send("你好，我是hello路由返回的内容");
    });
    
    // 开启服务器
    app.listen(1314,function(){
    console.log("成功开启服务器");
    });
