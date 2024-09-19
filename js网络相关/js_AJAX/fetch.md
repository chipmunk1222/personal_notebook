- 定义：1、fetch api能够实现xhr的所有任务，且更容易易用，区别是fetch必须异步。
	- 2、fetch传入请求参数，返回一个期约，期约解决完毕后返回一个response响应对象，包含任务的具体值
- 基本用法：fetch('url').then((response)=>{})

- fetch参数：
	- fetch可传入两个参数，第一个参数为服务器url地址，第二个参数为init对象，包含fetch配置信息
	- method：指定fetch请求方法
	- headers：用于指定请求头部
	- body：用于指定请求体的内容，包括参数等
- Request对象：
	- 定义：暴露请求的相关信息，用于作为参数传递给fetch，参数格式等同于fetch
	- 特性：可使用构造函数或clone()克隆request对象，后传入的参数会覆盖原先的参数，通过fetch调用一次后会被标记为已用，需要克隆传递多个fetch
- response对象：
	- 定义：fetch成功解决后返回的对象，包含响应信息
	- text()：将响应内容解释为字符串，本质仍是一个期约，可通过.then()解析
	- json()：将响应结果解释为json数据格式，可通过.then()解析
	- arrayBuffer()：将结果解析为可查看和修改的二进制文本，blob()：不可查看的二进制文本
	- status：响应状态码
	- statusText：状态文本，表述请求状态
	- ok：更简单区分状态的属性，true表示状态码200成功


WebSocket：
- 定义：通过一个长时连接实现与服务器的双向通信
- 特性：websocket使用自定义协议，将http和https改为ws和wss，确保连接安全
- api：
	- 基本样例：let socket = new WebSocket('wss://')
	- readystate：描述WebSocket状态，0：正在建立；1：已建立；2：正在关闭；3：已关闭
	- close()：关闭Web Socket连接
	- send()：发送数据
	- onmessage()：接收到消息时触发的函数
	- onopen()：连接成功时触发，operror()：连接错误时触发，onclose()：关闭时触发
