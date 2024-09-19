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
- 2、调用规则：\<a href="#/url">  
- 3、定位：使用\<router-view><\\router-view>定位路由出口，\<router />定位父级出口

注：
- 在router.js中使用vuerouter时，需要import Vue from ‘vue’，且export default router
- 绝对路径，使用@代表src文件
- 在路由最后配置path："\*",处理未匹配时的404界面
- routes中添加配置项：mode：“history”，在列表显示中不显示#号


router-link：
- 用法：用router-link替代a标签，可以直接实现active标签的定制效果（主要为高亮）
- 语法：\<router-link to="/url">\<\\router-link>
标签样式定制：
- a.router-link-active：模糊匹配（在多级标题下保持样式效果）
- a.router-link-exact-active：精确匹配（精确导航下显示样式）
自定义标签类名：
在routes中添加配置项：
- linkActiveClass：修改模糊匹配类名
- linkExactActveClass：修改精确匹配类名


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


- $route是一个局部的跳转路由对象,包含各项属性，this. $route相当于指向当前界面的指针
- $route.path返回相当于当前页面相对于根目录的绝对路径

路由记录文件页面地址
- 使用路由进行文件跳转：this.$router.push('URL')
- 标签中使用router属性，表示页内跳转
- router-view标签：多位对应，用以表示在页内某一部分插入路由部分（页内显示）
- router-link标签：参数：to="URL"：用以路由跳转
- 页面子集显示：在父集中写入\<router />表示子集先返回到父集
- matched属性：常用于面包屑，this.$route.matched用以返回路由下所有嵌套父集

router文件内部元素
- 引入包import Vue，VueRouter
- 定义路由文件 const router = new router（）{ routes} 
- 使用路由文件 export default router Vue.use(VueRouter)
- 配置路由参数：const routes = \[
	- path：外部调用时的路径（网站相对于根目录的显示路径）
	- name：外部调用时的别名
	- component：()=>import{' 外部文件'} 需要调用的文件
	- children：\[子路由列表] 子列表路由，用以展示子列表
- ]

