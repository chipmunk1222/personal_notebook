element-ui使用流程：
- 使用npm装入element-ui资源包
- 在main.js文件中调用资源包
- 直接调用插件

完整引入：
main.js 文件中

import Vue from 'vue';
import App from './App.vue'; 
import ElementUI from 'element-ui'; 
import 'element-ui/lib/theme-chalk/index.css'; 

Vue.use(ElementUI); 

new Vue({ 
	el: '#app', 
	render: h => h(App)
 });

element ui布局容器语法：
外部：el-container
内部：el-container+el-部件，以外部el-container为基准，内部撑开整个外部元素