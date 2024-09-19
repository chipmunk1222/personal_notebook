node_modules：第三方依赖
public：index文件
package.json：包含vue各信息（使用npm i可自动安装package.json中的依赖）

vue创建的项目中public中html文件只负责存放标头以及调用框架CDN连接

src文件存放文件主体，源代码目录
- .vue后缀文件相当于显示部分
- \<template>中存放相当于body
- \<style>中存放相当于css
- \<script>存放javascript，外部文件调用，框架参数等

main.js：入口js文件，最先执行文件
App.vue：挂载app的根组件

assets：静态资源目录
component文件中存放项目组件信息，根据路由调用，
- 性质：组件化编程，通过调用组件不断集成完善
- 使用方法：通过import ‘URL’导入组件，后在components配置项中注册组件，在对应使用位置直接使用组件（局部注册）
- 在main.js引入组件为全局注册import ‘URL’引入，Vue.component(’组件名‘，组件对象)

view文件中存放视图信息，根据文件层级关系分级
router文件存放js文件，包括页面跳转等路由配置

router文件内部元素
- 引入包import Vue，VueRouter
- 定义路由文件 const router = new router（）{ routes} 
- 使用路由文件 export default router Vue.use(VueRouter)
- 配置路由参数：const routes = \[
	- path：外部调用时的路径
	- name：外部调用时的别名
	- component：()=>import{' 外部文件'} 需要调用的文件
	- children：\[子路由列表] 子列表路由，用以展示子列表
- ]
	


一些文件命名规范：
- stats：表示统计类资源
- wms：表示地理信息
- user：表示用户信息
- role：表示角色信息