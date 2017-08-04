# AJAX #
## AJAX简介  ##

AJAX 是 Asynchronous JavaScript And XML 的简称。直译为，异步的JS和XML。
    
AJAX的实际意义是，不发生页面跳转、异步载入内容并改写页面内容的技术。
    
AJAX也可以简单的理解为通过JS向服务器发送请求。
    
AJAX这门技术很早就被发明，但是直到2005年被谷歌的大量使用，才在市场中流行起来，可以说Google为AJAX的推广起到推波助澜的作用。
    
    
## 同步处理： ##

AJAX出现之前，我们访问互联网时一般都是同步请求，也就是当我们通过一个页面向服务器发送一个请求时，在服务器响应结束之前，我们的整个页面是不能操作的，也就是直观上来看他是卡主不动的。
      
这就带来了非常糟糕的用户体验。首先，同步请求时，用户只能等待服务器的响应，而不能做任何操作。其次， 如果请求时间过长可能会给用户一个卡死的感觉。最后，同步请求的最大缺点就是即使整个页面中只有一小部分内容发生改变我们也要刷新整个页面。
      
## 异步处理： ##

而异步处理指的是我们在浏览网页的同时，通过AJAX向服务器发送请求，发送请求的过程中我们浏览网页的行为并不会收到任何影响，甚至主观上感知不到在向服务器发送请求。当服务器正常响应请求后，响应信息会直接发送 到 AJAX中，AJAX可以根据服务器响应的内容做一些操作。
      
使用AJAX的异步请求基本上完美的解决了同步请求带来的问题。首先，发送请求时不会影响到用户的正常访问。 其次，即使请求时间过长，用户不会有任何感知。最后，AJAX可以根据服务器的响应信息局部的修改页面，而不需要整个页面 刷新。
      
      
## 请求对象 ##
    
向服务器发送请求，毫无疑问需要使用Http协议，也就是我们需要通过JS来向服务器发送一个请求报文。
        
这是一个请求报文的格式，那我们如果手动的创建这么一个报文格式来发送给服务器想必是非常麻烦呢，于是浏览器为我们提供了一个XMLHttpRequest对象。


## XMLHttpRequest对象 ##

XMLHttpRequest对象是AJAX中非常重要的对象，所有的AJAX操作都是基于该对象的。

XMLHttpRequest对象用来封装请求报文，我们向服务器发送的请求信息全部都需要封装到该对象中。
    
这里需要稍微注意一下，XMLHttpRequest对象并没有成为标准，但是现在的主流浏览器都支持该对象，而一些如IE6的老版本浏览器中的创建方式有一些区别，但是问题不大。
    
## 获取XMLHttpRequest对象： ##
    
由于浏览器之间的差异，不同浏览器中获取XMLHttpRequest的方式不同，但总的来说一共有三种方式：

 - var xhr = new XMLHttpRequest()
 
      - 目前主流浏览器都支持
        var xhr = new ActiveXObject("Msxml2.XMLHTTP")
      - IE6支持的方式
        var xhr = new ActiveXObject("Msxml2.XMLHTTP")
      - IE5.5以下支持的方式
        var xhr = new ActiveXObject("Microsoft.XMLHTTP")
      
根据三种不同的方式编写通用方法来获取XMLHttpRequest对象：
    
      //获取XMLHttpRequest的通用方法
      function getXMLHttpRequest(){
      	var xhr;
      	try{
      		//大部分浏览器都支持
		xhr = new XMLHttpRequest();
      }catch(e){
		try{
	      		//如果不支持，在这里捕获异常并且采用IE6支持的方式
      			xhr = new ActiveXObject("Msxml2.XMLHTTP");
	      	}catch(e){
	      		//如果还不支持，在这里捕获异常并采用IE5支持的方式
	      		xhr = new ActiveXObject("Microsoft.XMLHTTP");
	      	}
      	}
	      return xhr;
      }
      
## XMLHttpRequest对象的方法： ##
    
### open(method,url,async) ###

open()用于设置请求的基本信息，接收三个参数。
      
- method
  - 请求的方法：get或post
  - 接收一个字符串
  
- url
  - 请求的地址，接收一个字符串

- Assync
  - 发送的请求是否为异步请求，接收一个布尔值。
  - true 是异步请求
  - false 不是异步请求（同步请求）
         
### send(string) ###
send()用于将请求发送给服务器，可以接收一个参数
        
string参数
  - 请求体，该参数只在发送post请求时需要。
  - string参数用于设置请求体
          
### setRequestHeader(header,value) ###
用于设置请求头
        
- header参数
  - 字符串类型，要设置的请求头的名字
          
- value参数
  - 字符串类型，要设置的请求头的值
          
## XMLHttpRequest对象的属性： ##

### readyState ###

描述XMLHttpRequest的状态
      
一共有五种状态分别对应了五个数字：
-  0 ：请求尚未初始化，open()尚未被调用
-  1 ：服务器连接已建立，send()尚未被调用
-  2 ：请求已接收，服务器尚未响应
-  3 ：请求已处理，正在接收服务器发送的响应
-  4 ：请求已处理完毕，且响应已就绪。
        
### status ###

请求的响应码 

  200 响应成功
  404 页面为找到
  500 服务器内部错误 
  … … … …
         
### onreadystatechange ###
该属性需要指向一个函数，该函数会在readyState属性发生改变时被调用。
        
### responseText ###

获得字符串形式的响应数据。
responseXML（用的比较少）
获得 XML 形式的响应数据。


### 示例代码 ###

  - 使用AJAX发送GET请求
  
        //获取xhr对象
        var xhr = getXMLHttpRequest();
        //设置请求信息
        xhr.open("get","AjaxServlet?&t="+Math.random(),true);
        //发送请求
        xhr.send();
        //监听请求状态
        xhr.onreadystatechange = function(){
                //当响应完成
                if(xhr.readyState == 4){
                        //且状态码为200时
                        if(xhr.status == 200){
                        //接收响应信息（文本形式）
                         var text = xhr.responseText;
                        //弹出消息
                        alert(text);
                        }
                };
        };

这是一个最简单的AJAX代码，向AjaxServlet发送了一个get请求，并且在页面中输出响应的内容

  - 使用AJAX发送POST请求
  
        //获取xhr对象
        var xhr = getXMLHttpRequest();
        //设置请求信息
        xhr.open("post","2.jsp",true);
        //设置请求头
         xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
        //发送请求
        xhr.send("hello=123456");
        //监听请求状态
        xhr.onreadystatechange = function(){
                //当响应完成且状态码为200时
                if(xhr.readyState == 4 && xhr.status == 200){
                        //接收响应信息（文本形式）
                        var text = xhr.responseText;
                        //弹出消息
                        alert(text);
                }
        };
    
    
### 练习代码 ###
    
        <!DOCTYPE html>
        <html lang="en">
        <head>
                <meta charset="UTF-8">
                <title></title>
        </head>
        <body>
    
                <button id="btn">发送getAJAX请求</button>
                <button id="btn2">发送postAJAX请求</button>
    
                <div id="box"></div>
        </body>
        <script>
                 var box = document.getElementById("box");
    
    
                //为btn绑定单击响应函数
                var btn = document.getElementById("btn");
                btn.onclick = function(){
    
                        //1.创建XMLHttpRequest对象
                        var xhr = new XMLHttpRequest();
    
    
                        //2.设置请求信息
                        //Math.random()随机数 解决get缓存问题
                        xhr.open("get","/getAJAX?username=wukong&password=123123&t=" + Math.random());
    
    
                        //3.发送请求
                        xhr.send();
    
    
                        //4.接收响应
                        xhr.onreadystatechange = function(){
                                //判断readyState是否是4 同时 响应状态码是200
                                if(xhr.readyState == 4 && xhr.status == 200){
                                //将内容在页面中显示
                                box.innerHTML += "<h1>"+ xhr.responseText +"</h1>"
                                }
                        };
    
                };
    
    
                //为btn2绑定单击响应函数
                var btn2 = document.getElementById("btn2");
                btn2.onclick = function(){
    
                        //1.创建XMLHttpRequest对象
                        var xhr = new XMLHttpRequest();
    
    
                        //2.设置请求信息
                        xhr.open("post","/postAJAX");
    
    
                        /*
                        在发送post请求时，为可以正常解析到请求体中的参数
                        还必须为请求设置如下的一个请求头
                        Content-Type: application/x-www-form-urlencoded
                         */
                        xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
    
    
                        //3.发送请求
                        xhr.send("username=wukong&password=123123");
    
    
                        //4.接收响应
                        xhr.onreadystatechange = function(){
                                if(xhr.readyState == 4 && xhr.status == 200){
                                //将内容在页面中显示
                                box.innerHTML += "<h1>"+ xhr.responseText +"</h1>"
                                }
                        };
                };
    
        </script>
        </html>
