Cookie：存储在浏览器中的一种小文本，用来记忆用户是谁
获取cookie：document.cookie = "username1 = namevalue1"

js-cookie：轻量化的处理javascript cookie的api
- 依赖安装：npm i js-cookie
- 导入：import Cookies from ‘js-cookie’
- 创建cookie：Cookies.set('name','value')
- 创建定时cookie：Cookies.set('name','value',|{expires:7,path:''})  //表示定时7天，对当前页面有效

- 读取cookie：Cookies.get('name')=>value,Cookies.get(null)=>undefined
- 读取所有cookie：Cookies.get()=>{name:'value'}

- 删除cookie：Cookies.remove('name',|{path:'',domain:'',secure:true})
- 注：删除cookie必须按照注册时的方式配置参数{path：网页路径，domain：域名，secure：是否需要安全协议}