# 温故而知新之ajax总结篇
## 一、什么是ajax
&nbsp;&nbsp;&nbsp;&nbsp;在总结ajax知识点之前，首先我们需要知道什么是ajax。ajax的全称是Asynchronous JavaScript and XML即异步的JavaScript和XML。而XML是一种很像超文本标记语言的可扩展标记语言,它被设计用来传输和存储数据，其焦点是数据的内容(超文本标记语言被设计用来显示数据，其焦点是数据的外观)。ajax有以下特性:

* ajax不是新的编程语言，而是一种使用现有标准的新方法。ajax是与服务器交换数据并更新部分网页的艺术，在不重新加载整个页面的情况下。
* ajax是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。
* ajax是一种用于创建快速动态网页的技术。通过在后台与服务器进行少量数据交换。ajax可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。而传统的网页（不使用ajax）如果需要更新内容，必须重载整个网页面。
* ajax的应用使用支持以上技术的web浏览器作为运行平台。这些浏览器目前包括：Mozilla、Firefox、Internet Explorer、Opera、Konqueror及Safari。但是Opera不支持XSL格式对象，也不支持XSLT。
* ajax前景非常乐观，可以提高系统性能，优化用户界面。AJAX现有直接框架AjaxPro，可以引入AjaxPro.2.dll文件，可以直接在前台页面JS调用后台页面的方法。但此框架与FORM验证有冲突。另微软也引入了AJAX组建，需要添加AjaxControlToolkit.dll文件，可以在控件列表中出现相关控件。

　　除了以上ajax的特性，它还有很多优点被程序设计者青睐：
　　
 1. 最大的优点就是页面无刷新，用户的体验非常好。
 2. 使用异步方式与服务器通信，具有更加迅速的响应能力。。
 3. 可以把以前一些服务器负担的工作转嫁到客户端，利用客户端闲置的能力来处理，减轻服务器和带宽的负担，节约空间和宽带租用成本。并且减轻服务器的负担，ajax的原则是“按需取数据”，可以最大程度的减少冗余请求，和响应对服务器造成的负担。
 4. 基于标准化的并被广泛支持的技术，不需要下载插件或者小程序。
 5. ajax可使因特网应用程序更小、更快，更友好。

　　除此之外ajax还有一些的缺点：

 * ajax不支持浏览器back按钮。
 * 不支持跨域访问
 * 安全问题 AJAX暴露了与服务器交互的细节。
 * 对搜索引擎的支持比较弱。
 * 破坏了程序的异常机制。
 * 不容易调试。
  
## 二、进行ajax请求一般流程
### 1. 创建ajax请求对象
&nbsp;&nbsp;&nbsp;&nbsp;当我们需要进行数据传输交互的时候，首先需要创建一个ajax请求对象， 通过该对象调用ajax请求的属性和方法。需要注意的是，ajax请求对象有兼容问题，我们可以通过以下代码解决兼容问题:

       var ajaxObj = null; //ajax有兼容，下面是处理兼容的方法
       if(window.XMLHttpRequest){
          ajaxObj = new XMLHttpRequest();//IE7+,标准浏览器
       }else{
          ajaxObj = new ActiveXObject("Microsoft.XMLHTTP");//IE5,IE6
       }   

### 2.建立连接
&nbsp;&nbsp;&nbsp;&nbsp;我们通过ajax.open()方法建立与后台的数据连接请求。该方法有三个参数：

   * 参数1：请求的方式是GET还是POST，
   * 参数2：需要请求的PHP文件的路径地址。
   * 参数3：选择请求的方式是同步还是异步。true是异步请求，false同步请求

        ajaxObj.open("GET","index.php",true);
        ajaxObj.open("POST","index.php",true);
        
### 3.发送请求
&nbsp;&nbsp;&nbsp;&nbsp;我们通过ajax.send()方法向后台发送请求。send()方法分为有参和无参两种情况，当我们建立请求使用GET方式时，send()方法无参。放建立请求使用POST方式时， 我们需要字符串格式的参数作为数据传递给后台,同时，我们还需要设置请求头信息。具体实例如下：
        
       ajaxObj = new XMLHttpRequest;//创建ajax请求对象，在这里暂不考虑兼容问题
       ajaxObj.open("GET","index.php",true);//GET方式创建请求
       ajaxObj.send();//发送请求
       
       ajaxObj = new XMLHttpRequest;
       ajaxObj.open("GET","index.php",true);//POST方式创建请求
       ajaxObj.setRequestHeader("Content-type","application/x-www-form-urlencoded"); //post方式时设置请求头信息
       var data = "dataKey1="+dataValue1+ "&dataKey2="+dataValue2;  
       ajaxObj.send(data);

### 4. 根据服务器的响应去做对应的处理（监控请求状态并处理）
&nbsp;&nbsp;&nbsp;&nbsp;我们通过onreadystatechange方法监控请求状态并做响应处理。XMLHttpRequest的请求状态readyState有0到4的发生状态变化：

* 0: 请求未初始化,还没来得及调用open方法
* 1: 初始化，服务器连接已建立，正在调用send方法，发送请求
* 2: send方法已经调用完毕，请求已接收
* 3: 服务器已经响应，请求处理中
* 4: 请求已完成，且响应已就绪

        ajaxObj.onreadystatechange = function(){ //状态码变化时执行的函数
            if(ajaxObj.readyState == 4&&ajaxObj.status == 200){
            console.log(ajaxObj.responseText); //打印PHP返回的内容
          }else if(ajaxObj.readyState == 4&&ajaxObj.status != 200){
            console.log(ajaxObj.status) //打印服务器错误状态码
          }
        }
        
http状态可以参考百度百科[@http状态码](https://baike.baidu.com/item/HTTP状态码/5053660?fr=aladdin)查看详细信息。

## 三、ajax跨域问题
ajax是不支持跨域访问的，一般情况下，我们通过以下三种方法解决跨域问题

1. 设置服务器代理 具体设置方法可以参照百度经验[@设置服务器代理](http://jingyan.baidu.com/article/b7001fe169f3800e7382dd5c.html)。


2. jsonp方法 原理：利用Script标签的src属性，将src路径文件解析成js文件执行
   当我们遇到跨域问题时，可以将有跨域问题的请求文件路径，以字符串的形式在本地没有跨域问题的请求文件内保存下来，通过js创建script标签，将该script的src属性赋值成保存好的路径字符串，再将该标签添加到DOM里，Script标签的src属性会将src路径文件解析成js文件执行。具体实例如下
        
         //index.html 请求跨域交互的HTML文件
         <!DOCTYPE html>
         <html>
         <head>
		     <meta charset="utf-8" />
		     <title></title>
	     </head>
	     <body>
		     <input type="button"value="btn" id="btn"/>
	     </body>
         </html>
         <script type="text/javascript">
	          function call(data){
	             console.log(data);
	           }
	     btn.onclick = function(){
	           var obj =  new XMLHttpRequest;
	           obj.onreadystatechange = function(){
	              if(obj.status == 200 && obj.readyState == 4){
	                 var script = document.createElement("script");
	                 script.src = obj.responseText +"?callback=call";
	                 document.body.appendChild(script);
	              }
	              obj.open("GET","text.php",true);
	              obj.send();
	              }
	       </script>
     
        //没有跨域问题的本地文件
         <?php
            echo "http://172.18.25.245/Myphp/jsonp/jsonp.php";
         ?>

3. XMLHttpRequest Level 2 提供的方法 即在服务器/后台数据库填上响应头 "header(‘Access-Control-Allow-Origin:*’)";  * 表示接受所有的域

## 四、ajax函数封装

&nbsp;&nbsp;&nbsp;&nbsp;ajax函数做网络请求，参数以对象的形式传递，对象所必须具备的属性：

1. url 请求的PHP文件地址
2. type  请求的类型 GET POST
3. 向后台传递的数据，最好是对象形式
4. success  请求成功时执行的回调函数
5. error  请求失败时执行的回调函数


        //ajax.js原生封装
          function AJAX(obj){   //解决了跨域问题的AJAX函数封装
	        var ajaxObj = null;
	        if(window.XMLHttpRequest){
		        ajaxObj = new XMLHttpRequest();
	        }else{
	        	ajaxObj = new ActiveXObject("Microsoft.XMLHTTP");
	        }
	        ajaxObj.onreadystatechange = function(){
		        if(ajaxObj.readyState == 4 && ajaxObj.status == 200){
		        	if(obj.successCall){
		        		if(obj.successCall&&obj.crossDomainCall){ //有跨域请求的crossDomainCall函数，有此函数表示有跨域请求
					        var script = document.createElement("script");
	                       script.src = obj.responseText +"?"+obj.callBack+"="+obj.crossDomainCall;  //callBack当做函数名传递给后台(可以自定义函数名，不用加obj)，后台需要 _GET("callBack")接收一下，从而方便传函数名和传参数 ,crossDomainCall函数是obj对象的crossDomainCall函数(自定义)。
	                       document.body.appendChild(script);
				        }else{
					        obj.success(JSON.parse(ajaxObj.responseText));
				        }
			        }else{
				        alert("缺少成功时执行的回调函数");
				        return
			        }
		        }else if(ajaxObj.readyState == 4 && ajaxObj.status != 200){
		        	if(obj.error){
			        	obj.error(ajaxObj.status);
			        }else{
			        	alert("缺少失败时执行的回调函数");
			        }			
		        }
	        }
	        var type = obj.type || "GET";
	        var param = "";
	        for(var key in obj.data){
	        	param += key + "=" + obj.data[key] + "&";
		        param = param.slice(0,param.length-1);
	        }
	        if(type == "GET"){
		        ajaxObj.open("GET",obj.url+"?"+param,true);
		        ajaxObj.send();
	        }else{
		        ajaxObj.open("POST",obj.url,true);
		        ajaxObj.setRequestHeader("Content-type","application/x-www-form-urlencoded");
		        ajaxObj.send(param);
	        }
        };

        //ajax函数封装（基于JQ）
        //url：地址
        //data：数据对象，在函数内部会转化成json串，如果没传，表示用GET方法，如果传了，表示用POST方法
        function ajax(url, data, callback) {   
            $.ajax({     
                 url: url,     
                 type: data == null ? 'GET' : 'POST',     
                 dataType: "json",     
                 data: data == null ? '' : JSON.stringify(data),     
                 async: true,     
                 contentType: "application/json",     
                 success: function (resp) {       
                     callback(resp);     
                 },     
                 error: function (XMLHttpRequest, textStatus, errorThrown) {    
                       if (XMLHttpRequest.status == "401") {
                              window.parent.location = '*****.html';
                              self.location = '*****.html';    
                        } else {         
                              alert(XMLHttpRequest.responseText);        
                        }     
                  }     
            });
        }


当我们碰到多个异步ajax请求时，通常会把多个Ajax请求顺序着写下来，而后面的请求，对前面请求的返回结果是有依赖的。我们可以利用Promise解决多个异步Ajax请求导致的代码嵌套问题，具体方法可以参考博客[@多个异步Ajax请求问题](http://m.jb51.net/article/106837.html)

