# Route（路由） #
在Express中通过路由将请求地址和函数进行关联，这样当服务器收到请求时，可以直接调用函数去处理请求并返回响应。
			
## 路由的设置的方式 ##
    app.<method>(path,callback); 
  
### method表示要处理的请求方式： ###
-  app.get()
-  app.post()
-  app.all()
					

### path ###
要映射的路径，以/开头，/代表根目录
				

### callback ###
   当path对应的地址被访问时，要调用的回调函数。
   
#### 回调函数中有三个参数： ####
   
   - request路由的回调函数的第一个参数
   
 表示客户端发送给浏览器的请求报文,可以通过该对象来获取请求报文中的内容。
  
 属性和方法：
  -    originalUrl 获取请求的完整路径，请求首行的路径

  -    protocol 使用协议

  -    ip 客户端的ip地址

  -    path 请求路径不包括查询字符串
 
  -    host 主机地址

  -    method 请求方法

  -    headers 所有的请求头

  -    get(header) 获取指定的请求头
  
 -    query ***** 是一个对象，它里边保存了查询字符串中的请求参数可以通过qurey来获取get请求的发送的请求参数。
  
- response路由的回调函数的第二个参数

   表示服务器发送给浏览器的响应报文可以通过该对象向响应报文中设置内容。
   
   属性或方法：

   - res.status() 设置响应状态码
   
   - res.send() 设置响应体并发送响应报文
   
   - res.sendFile() 将文件设置响应体并发送给客户端
    - 使用该方法发送的文件，如果浏览器能打开则自动打开否则将会弹出下载窗口
   
   - res.download()将文件设置为响应头并提供给客户端进行下载
    - 使用该方法发送的文件，无论浏览器是否能打开，都会弹出下载窗口
   
   - res.redirect()
    - 请求的重定向
    - 将当前请求重定向到另一个地址
    - 重定向的流程：
     1.浏览器向一个路由发送请求。
     2.这个路由会向浏览器发送一个特殊的响应，这个响应告诉浏览器再去向另一个地址发送请求这个特殊的响应的响应状态码是302，表示重定向同时还具有一个响应头：Location: /hello.html。
     3.浏览器再次向新的地址发送请求。
  
  
   - next路由的回调函数的第三个参数

     - 可以为一个路径同时映射多个路由，这样当访问该路径时，多个路由都会被触发，触发顺序是按照路由的设置顺序触发的，多个路由只能返回一个响应

	示例代码：
			app.get("/hello",function (req , res , next) {

			});

			app.get("/hello",function (req , res , next) {

			});

			app.get("/hello",function (req , res , next) {

			});
			
			//===========================================
			app.get("/hello",function (req , res , next) {

			},function (req , res , next) {

			},function (req , res , next) {

			});
			
  - 可以通过next来控制路由是否相下进行，如果不调用next，则不会向下继续，而调用next则会触发下一个路由。
			
  - 同一个请求的req和res一定是相同的对象	
		
### 可以路由统一设置到Router上，这样将方便对路由进行管理 ###

			var router = express.Router();
			
			router.get(...);
			router.post(...);
			router.all(...);
			router.use(...);
			
			app.use(router);
