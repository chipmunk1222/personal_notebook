背景：随着web应用程序的出现，直接在客户端存储数据的需求随之出现，包括登录信息、个人偏好、还是其他数据。

*cookie：
- HTTP cookie通常也叫做cookie，最初用于在客户端存储会话信息，具体方式为在HTTP请求时携带包含Set-Cookie的头部
- 实现样例：
	- HTTP/1.1 200 OK
	- Content-type：text/html
	- Set-Cookie：name=value
	- other-header：other-header-value
- 该样例中设置了name=value的键值对的cookie，于是每次请求中都会包含这些信息
- 返回样例：
	- GET  /index.jsl HTTP/1.1
	- Cookie:name=value
	- other-header:other-header-value
- cookie的构成(参数)：
	- cookie名称(name)：唯一标识cookie的名称，不区分大小写，必须经过URL编码
	- cookie值(value)：存储在cookie里的字符串，必须经过URL编码
	- 域(domain)：cookie有效的域，发送到对应域的请求包含相应cookie
	- 路径(path)：明确URL路径，对域名的补充，只有对应路径才会包含cookie
	- 过期时间(expire)：标识cookie何时删除的时间戳，默认浏览会话结束后就删除，但可以设置，格式为GMT格式(Wdy,DD-MM-YYYY hh:mm:ss GMT)
	-  安全标志(secure)：设置之后，只有使用SSL安全链接(https)才会把请求发送到服务器
- jscookie读取：document.cookie，以name1=value1;name2=value2的格式读取cookie，因为原生js处理cookie方式过于简单，一般会对其进行进一步封装
- 子cookie：为绕过浏览器对cookie个数的限制，在同一个cookie中存储多个键值对

*Web Storage：*
- 解决通过客户端存储不需要频繁发送回服务器数据时使用cookie的问题
- 特点：1、提供在cookie之外存储会话数据的方式 2、提供会话持久化存储大量数据的方式
- Storage类型：
	- clear()：删除所有值
	- getItem(name)：获取给定name的值
	- setItem(name,vlaue)：设置对应键值对
	- removeItem(name)：删除给定name的键值对
	- key(index)：给定下标的名称，用于遍历等用途
	- length：键值对总数长度
- localStorage：
	- 特点：Storage类型，可调用Storage提供的方法，localStorage中的数据会保存到js删除或用户清除系统缓存，不会受页面或窗口关闭影响
- sessionStorage：
	-  特点：Storage类型，可调用Storage提供的方法，只存储会话数据，数据只会存储到浏览器关闭，不受页面刷新影响，可在浏览器崩溃重启后恢复
- 存储事件：
	- 通过监听storage处理相应事件
	- 样例：window.addEventListener("storage",(event)=>{console.log(event)})
	- event属性：
		- domain：变化的域名
		- key：被设置或删除的键
		- newValue：被修改的值，删除为null
		- oldValue：修改前的值
	- 注：localStorage和sessionStorage的变化都活触发Storage事件

*indexDB：*
- 定义：indexed DataBase Api，简称indexedDB，是浏览器中存储结构化数据的一个方案
- 特点：indexedDB几乎是完全异步的，大多数操作以请求的方式执行，绝大多数indexedDB操作要求添加onsuccess或onerror处理程序输出
- 方法：
	- let request = indexedDB.open(‘name’)：发送打开对应名称数据库的请求并接收
	- request.onerror = (event) =>{console.log(event.target.errorcode)}：失败处理
	- event.target：指向request本身
- 对象存储：使用js对象的格式来存储数据