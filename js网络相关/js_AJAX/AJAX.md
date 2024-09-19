全称：asynchronous JavaScript and XML
功能：能够发送请求并得到服务器返回内容
XHR和Fetch都是AJAX的技术手段，只是API不同

AJAX特性：
- 在不重载的情况下更新页面
- 向服务器请求数据
- 向服务器发送或接收数据
- Get请求主要用来向服务器中获取数据，Post请求用来向服务器发送需要保存到数据

跨源资源共享CORS：
- 定义：全称(Cross-Origin Resourse Sharing)，定义了浏览器与服务器之间的跨源通信
- 方式：XHR默认请求为当前域名，如果需要跨源请求则需要包含完整URL地址
- 限制：1、不能设置自定义头部，2、不能发送和接收cookie，3、无法获取响应头

Ajax安全：
- 要求通过SSL访问能够被访问到的资源
- 要求每个请求都发送一个按约定算法计算好的token
- 无效方法：
	- 要求POST替代GET(请求方法容易伪造)
	- 验证URL来源(来源URL容易伪造)
	- 基于cookie验证(同样容易伪造)

AJAX建立请求样例：
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      document.getElementById("demo").innerHTML =
      this.responseText;
    }
  };
  xhttp.open("GET", "xmlhttp_info.txt", true);
  xhttp.send();
  - 流程：创建实例,初始化请求->状态变化异步调用函数->请求状态判断->接收处理返回值
  - 异步调用优势：javascript执行请求时无需等待，可以直接执行后续脚本
  
XMLHttpRequest方法：
- new XMLHttpRequest()：创建请求对象
- abort()：删除请求对象
- open(method，url，async)：指定请求类型，method：方法（‘’GET“：获取，”post：“发布）；url：（文件url地址）；async（true：异步，false：同步）
- send（）：发送GET请求；send（string）：发送POST请求，携带数据
- setRequestHeader（header，value）：设定发送文件目标，header：头文件
- getAllResponseHeaders()：返回所有请求头的序列化结构

XMLHttpRequest对象属性：
- onload = function()：当请求收到时，执行函数
- onreadystatechange = function（）：当readystate变化，执行函数
- readyState：返回请求的状态（0：未初始化，1：建立连接，2：收到请求，3：处理请求，4：请求处理完毕）
- status：返回网络状态（200：”OK“，403：”“Forbidden，404：”not found“）
- statusText：以字符串的形式返回网络状态
- responseText：以字符串的方式返回数据，
- responseXML：以XML的方式返回数据
- timeout：设置超时时间

FormData类型：
- 使用：通过新建FormData对象用来以键值对的方式存储序列化数据，用于send
- append()方法：FormData通过append('key','value')接收参数扩展键值对

fetch api：
- fetch返回值为一个Promise对象，可使用.then((data)=>{return data.json()})接收响应头内容，.then((data)=>return data)接收响应体内容
- 样例：async fn = （）=>{
	- let x = await fetch("URL") //异步获取请求头
	- let y = x.json() //获取请求体数据
- }