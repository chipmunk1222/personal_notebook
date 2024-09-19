定义：状态管理即对于大型项目需要处理多组件之间的共享数据时，要经历无比繁琐的数据传输，因此创建一个共有的仓库进行数据管理。

Vuex实例创建：
- 安装依赖：npm install vuex@next --save
- 引入：import Vuex from ’vuex‘
- 注册：Vue.use(Vuex)
- 创建配置对象：const store = new Vuex({
	- state:{}
	- mutations:{
		- fn(state,payload){}
	- }
	- actions:{} 
- })
- 注入：new Vue({
	 - render: h=>h(app)
	 - store
- }).$mount('#app')

Vuex构造器属性：
- state：存放数据，数据类型为响应式
- mutations：
	- mutations：存放数据处理方法，具有state默认参数，可传入payload额外参数
	- mutations调用：this.$store.commit('函数名'，payload):表示调用函数fn1，传入负载
- actions：
	- 作用：用以处理mutations无法处理的异步问题
	- 核心：action函数接收一个和store实例具有相同属性的context对象，通过调用context处理需求
	- 样例：actions:{
		- increment(context,payload){
			- setTimeout(()=>{context.commit('fn1',payload)},1000)
		- }
	- }
	- 调用：this.$store.dispatch('action1',payload)
	- action的函数本身是一个Promise，可以使用async异步返回
- modules：
	- 作用：将配置对象放到单独模块中，以解决数据过多导致的命名冲突
	- 样例：modules：{a：moduleA，b：moduleB}
	- 命名空间：加入命名空间从而避免命名冲突的问题
	- 加入命名空间（namespaced）后，模块内mutation、action的调用遵循路径法则，用‘/’连接，state的调用为this.$store.state.modulename.statevalue，不加命名空间则直接调用方法名
- 注：1、浏览器只能直接监控mutations的行为，故最终都使用mutations突变进行数据操作2、mutations中不允许出现异步操作

Vuex绑定的辅助函数：
- mapState：将Vuex仓库中的对象映射到Vue项目中的计算属性，起到简化作用
- 样例：import {mapState} from ‘vuex’
	- computed：mapState('modulename'，{
		- name:'name'  :=>name:this.$store.state.name
		- age: state => state.age   :=>age = this.$store.state.age
	- })
- 注：如果直接使用mapState映射会导致原有计算属性没地方放，故一般使用...数组拓展运算符将mapState添加到原计算属性后
Vuex注入后的实例对象：
- $store：存放Vuex对象