AJAX特性：
- 在不重载的情况下更新页面
- 向服务器请求数据
- 向服务器发送或接收数据

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
- send（）：发送接收请求；send（string）：发送发布请求
- setRequestHeader（header，value）：设定发送文件目标，header：头文件

XMLHttpRequest对象属性：
- onload = function()：当请求收到时，执行函数
- onreadystatechange = function（）：当readystate变化，执行函数
- readyState：返回请求的状态（0：未初始化，1：建立连接，2：收到请求，3：处理请求，4：请求处理完毕）
- status：返回网络状态（200：”OK“，403：”“Forbidden，404：”not found“）
- statusText：以字符串的形式返回网络状态
- responseText：以字符串的方式返回数据，
- responseXML：以XML的方式返回数据

