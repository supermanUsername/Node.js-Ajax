# Middleware（中间件） #
Express 是一个自身功能极简，完全是由路由和中间件构成一个的 web 开发框架：从本质上来说，一个 Express 应用就是在调用各种中间件。

Express提供的大部分功能是通过中间件函数完成的，这些中间件函数在Node.js收到请求的时点和
  发送响应的时点之间执行。

通过Express支持的中间件可以让你快速提供静态文件，实现Cookie，支持会话，处理POST数据，等等。

中间件（Middleware） 是一个函数，它可以访问请求对象（request object (req)）, 响应对象（response object (res)）, 
  和 web 应用中处于请求-响应循环流程中的中间件，一般被命名为 next 的变量。
  
  
## 中间件定义 ##
    app.use(function(req , res , next){
	    //代码
    });
    
    
### 中间件的功能包括： ###

- 执行任何代码。
- 修改请求和响应对象。
- 终结请求-响应循环。
- 调用堆栈中的下一个中间件。
    
    
### Express 应用可使用如下几种中间件： ###

#### 应用级中间件 ####

        var app = express();

        // 没有挂载路径的中间件，应用的每个请求都会执行该中间件
        app.use(function (req, res, next) {
          console.log('Time:', Date.now());
          next();
        });

        // 挂载至 /user/:id 的中间件，任何指向 /user/:id 的请求都会执行它
        app.use('/user/:id', function (req, res, next) {
          console.log('Request Type:', req.method);
          next();
        });

        // 路由和句柄函数(中间件系统)，处理指向 /user/:id 的 GET 请求
        app.get('/user/:id', function (req, res, next) {
          res.send('USER');
        });
        
#### 路由级中间件 ####

        var app = express();
        var router = express.Router();

        // 没有挂载路径的中间件，通过该路由的每个请求都会执行该中间件
        router.use(function (req, res, next) {
          console.log('Time:', Date.now());
          next();
        });

        // 一个中间件栈，显示任何指向 /user/:id 的 HTTP 请求的信息
        router.use('/user/:id', function(req, res, next) {
          console.log('Request URL:', req.originalUrl);
          next();
        }, function (req, res, next) {
          console.log('Request Type:', req.method);
          next();
        });

        // 一个中间件栈，处理指向 /user/:id 的 GET 请求
        router.get('/user/:id', function (req, res, next) {
          // 如果 user id 为 0, 跳到下一个路由
          if (req.params.id == 0) next('route');
          // 负责将控制权交给栈中下一个中间件
          else next(); //
        }, function (req, res, next) {
          // 渲染常规页面
          res.render('regular');
        });

        // 处理 /user/:id， 渲染一个特殊页面
        router.get('/user/:id', function (req, res, next) {
          console.log(req.params.id);
          res.render('special');
        });

        // 将路由挂载至应用
        app.use('/', router);
        
        
#### 错误处理中间件 ####

        app.use(function(err, req, res, next) {
            console.error(err.stack);
            res.status(500).send('Something broke!');
        });
        
        
####  内置中间件(静态资源的中间件) ####

        app.use(express.static('public'));
        app.use(express.static('uploads'));
        app.use(express.static('files'));
        
        
#### 第三方中间件 ####

        var express = require('express');
        var app = express();
        // 加载用于解析 cookie 的中间件
        var cookieParser = require('cookie-parser');
        app.use(cookieParser());
        
        // 解析post请求体的中间件
        var bodyParser = require("body-parser");
        app.use(bodyParser.urlencoded({extended:false}));
        
        
使用可选则挂载路径，可在应用级别或路由级别装载中间件。另外，你还可以同时装载一系列中间件函数，从而在一个挂载点上创建一个子中间件栈。
  
  
  
  
  
### 代码英语 ###
Middleware    英 ['midlwεə]    n. 中间件；中间设备
use    英 [juːz]    n. 使用；用途；发挥
static    英 ['stætɪk]    adj. 静态的
cookie    英 ['kʊkɪ]    n. 饼干；小甜点
parser    英 ['pɑːsə]    n. [计] 分析程序
