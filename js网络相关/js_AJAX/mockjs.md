依赖安装：npm install mockjs

使用场景：在后端数据接口未提供时进行数据模拟，保证前后端并行开发，效果等同于json-server，但mockjs是通过拦截ajax实现数据mock，json-server则通过创建模拟服务器的方式

注意事项：
- 如果同时使用axios和mockjs时，确保mockjs比axios先引入，否侧会有404报错
- 在大多数情况下，优先检查axios和mockjs的配置路径

原理：
- Ajax拦截：mockjs会检查请求的URL、请求方法和参数对Ajax请求进行拦截，一旦匹配成功，mockjs就会返回模拟数据而不是后端数据，这样就实现了对Ajax请求的拦截。
mock语法：
- import Mock from ‘mockjs’
- Mock.mock("url",GET,{
	- “code”：0，   //错误码
	- “msg”：null， //错误消息
	- data：{}          //获取的数据
- })
- 错误码详情：0：无错误，406：数据错误，500：服务器不存在
URL正则匹配：
- 使用场景，当URL地址带有params参数时，可使用正则表达式进行匹配
- 样例：/^\/api\/blog(\?.+)?$/
- /表示使用正则式/，^标志字串开始位置
mock函数选项：
- 作用：用于传递参数，具有type，url，body三个属性
- 语法：将template改为function(options){return Mock.mock(template)}
配置语法：
- Mock.setup({
	- timeout:400 / '200-600'  //设置响应时间
- })
使用技巧：
- 如果要对多个文件数据进行mockjs的拦截，可以创建一个中心文件导入子文件，那么在main.js中只需要调用中心文件就好了
- 此外，可以在中心文件中添加mockjs配置，从而使配置作用于所有mockjs文件