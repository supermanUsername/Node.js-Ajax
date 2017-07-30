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
    
    
    
    
    

### 代码英语 ###

express    英 [ɪk'spres; ek-]    n. 快车，快递，专使
app    英 [æp]    abbr. 应用（Application）
use    英 [juːz]    n. 使用；用途；发挥
get    英 [get]    vt. 使得；获得；受到；变成
static    英 ['stætɪk]   adj. 静态的
public    英 ['pʌblɪk]    adj. 公众的；公用的
request    英 [rɪ'kwest]    n. 请求；需要
response    英 [rɪ'spɒns]    n. 响应；反应；回答
query    英 ['kwɪərɪ]    [计] 查询
send    英 [send]    vt. 发送，寄
listen    英 ['lɪs(ə)n]     n. 听，倾听

    