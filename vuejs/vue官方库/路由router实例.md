Vue官方文档：[入门 | Vue Router (vuejs.org)](https://router.vuejs.org/zh/guide/)

Vue3重大变化：
- 引包：npm install vue-router@4
- 引入：import {createRouter ，createMemoryHistory}  from ‘vue-router’
- 安装注册：createAPP(App).use(router).mount('#app')
- 创建路由对象：const router = createRoute（{ 
	- history：createMemoryHistory
	- routes
- }）
 
VueRouter实例创建：
 - 引包：npm install vue-router@3.6.5(Vue2 为3.x Vue3为4.x)
 - 引入：import VueRouter from 'vue-router'
 - 安装注册：Vue.use(VueRouter)
 - 创建路由对象： const router = new VueRouter（{ routes }）
 - 注入：new Vue({
	 - render: h=>h(app)
	 - router
- }).$mount('#app')

VueRouter组件化配置：
- 1、创建规则：routes:\[path:'/url'  component:()=>{import('url')}]（component一般为页面组件，写在views文件里）
	- 其余配置项：name：命名路由，redirect：地址重定向，meta：元数据（路由附加信息）
- 2、调用规则： \<RouterLink to=url />\<\\RouterLink>
- 3、出口规则：使用 \<RouterView />定位路由出口，\<router />定位父级出口

注：
- 在router.js中使用VueRouter时，需要import Vue from ‘vue’，且export default router
- 绝对路径，使用@代表src文件
- 在路由最后配置path："\*",处理未匹配时的404界面
- router中添加配置项：mode：“history”，在列表显示中不显示#号

router-link(RouterLink)：替代a标签的页内跳转
- 用法：用router-link替代a标签，可以直接实现active标签的定制效果（主要为高亮）
- 语法： \<router-link to="/url">\<\\router-link>
- 命名路由：用名字跳转时，通过动态传递name对象进行路由跳转
标签样式定制：router-link自带的标签类，匹配选中页样式
- a.router-link-active：模糊匹配（在多级标题下保持样式效果）
- a.router-link-exact-active：精确匹配（精确导航下显示样式）
配置项修改：
在router中添加配置项：
- linkActiveClass：修改模糊匹配类名
- linkExactActveClass：修改精确匹配类名
router-link属性：
- exact：多级精确匹配，若为false，则允许多级匹配
- active-class：修改router-link-active的类名
- exact-active-class：修改router-link-exact-active的类名

路由原型对象：$route，\$router
- $route：存储路由信息，包含参数，查询参数，路由历史等
- $router：控制路由跳转

router-link传参：
- 查询参数传参（适合多个参数）
- 语法：
	- 跳转：to=“/url/?参数名=值&参数名2=值”
	- 获取：$route.query.参数名
- 动态路由传参（适合单个参数，简洁优雅）
	- 配置路由：/path/:参数名？
	- 跳转：to=“/url/值”
	- 获取：$route.params.参数名

router跳转：
- this.$router.push('URL') ,表现为切换路由，本质上是添加历史记录
- this.$router.push({
	- name:'路径名  （使用名字跳转）
	- query：{
		- 参数名：’参数值‘（query跳转语法）
	- }
	- params：{
		- 参数名：‘参数值’（动态路由跳转语法）
	- }
- '})
- 注：路由跳转参数并不会直接重置组件生命周期，如需更改数据，需要加入侦听器侦听$route进行参数绑定操作

- $route是一个局部的跳转路由对象,包含各项属性，this. $route相当于指向当前界面的指针
- $route.path返回相当于当前页面相对于根目录的绝对路径

路由记录文件页面地址
- matched属性：常用于面包屑，this.$route.matched用以返回路由下所有嵌套父集

router配置属性
- 配置路由参数：const routes = \[
	- path：外部调用时的路径（网站相对于根目录的显示路径）
	- name：外部调用时的别名
	- component：()=>import{' 外部文件'} 需要调用的文件
	- children：\[子路由列表] 子列表路由，用以展示子列表
	- meta：{}：存放元数据，即格外信息
- ]
	
路由守卫：
- *全局前置守卫：
- 定义：在路由导航之前调用，常用于全局的登录验证和权限检查
- 语法：router.beforeEach((to,from)=>{
	- //表达式，校验条件
	- return false
- })
- 参数：to：即将进入的目标；from：退出的目标
- 返回值：false：取消当前导航；{name：路由名称}：重定向跳转到对应路由
- *全局后置守卫：
- 定义：在路由跳转后调用，常用于修改页面标题，声明页面等操作
- 语法：route.afterEach((to,from)=>{
	- //表达式
	- 
- })
- *路由独享守卫：*
- 定义：在单个路由配置中被定义，仅在该路由触发时调用
- 使用场景：在路由配置项上加上路由守卫：
- 语法：beforeEnter：((to,from)=>{
	- //表达式
	- return false
- })
- 注：路由独享守卫只在路由本身被一次调用时触发，对于改变query，param，hash并不会触发