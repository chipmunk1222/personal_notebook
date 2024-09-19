简介：axois是一个基于promise的http库，主要实现文件间数据交互，前端和服务端,后端交互

Promise api：使用异步方式处理接收数据，.then用于获取成功请求的数据，.catch用于处理错误捕获

axios特点：1、基于Promise异步请求，2、可用于错误响应拦截，3、请求取消，4、自动转化为json数据格式，适用于vue和react等框架

- 封装promise的特性：由于程序采取异步操作，所以JavaScript不会等待axios执行完后再执行其他东西，故axios是后执行的，如需得到结果，需要使用回调函数或.then（）方法中封装的等待。

CDN：<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>

axios创建示例方法：
安装依赖：
- npm install axios

在vue.js中引入依赖：
- import axios from 'axios'
- Vue.prototype.$axios = axios;

使用异步操作axios：
- async function fun_name(){
	- let res = await axios.get(url,{参数})
- }
- async function fun_name(){
	- let res = await axios.post(url,{body})
- }

axios响应结构：
- {
	- data：{}，        //响应的数据
	- status：200，   //响应的状态码
	- statusText：’OK‘， //响应的状态信息
	- header：{}，      //响应头
	- config：{}          //响应的配置项
- }

axios拦截器：
- 请求拦截器：用以在请求发送后对请求执行相关操作
- 语法：const ins = axios.interceptors.request.use(function(config){
	- //在发送请求前做点什么
	- return config
- }) ，function（error）{
	- //对请求错误做点什么
	- return promise.reject(error);
- }
- 响应拦截器：用以在获取响应结果前做点什么
- 语法：const ins = axios.interceptors.response.use(
	- function(respond){
		- //在获取响应结果前做点什么
		- return respond；
- }) ，function（error）{
	- //对响应错误做点什么
	- return promise.reject(error);
- }
- 移除拦截器：
- 


创建实例：
- this.$axios（{
	- url：‘/results’   //请求的url地址 ，注意url小写
	- method：‘get’   //请求方法，默认get
	- baseURL：‘https：//randomuser.me/api’  //相当于绝对路径注意URL大写
	- respondtype：‘json’  //服务返回类型
	- timeout：1000     //异步延时
	- params：{
		- id：’1‘    //请求配置
	- }
	- data：{
		- 注：由于axios有自动将json数据格式转化为JavaScript对象的功能，所以data内部数据格式用JavaScript对象格式表示
	- }    //用以post，patch数据
- }）
- 注：无论是get请求还是post请求，其本质都是请求与服务器内容相匹配的内容，其本质区别在于后端会做不同操作，前端只需要接收数据即可，故没有什么本质差别


- 注：delete和patch方法只能通过对URL的变化执行相关操作，即只能通过添加id进行筛选，但json-server没有提供检索多个id共存的方法，故在post数据时需要先检索是否已经存在相同数据