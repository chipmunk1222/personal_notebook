选项式api的缺点：
- 当组件配置项过多时，使用选项式会导致代码过于冗杂
- 配置项过于分散导致配置项之间联系微弱
- 以配置项为区分导致对于任务的处理过程过于分散，难以阅读

组合式api：
- 作用：解决选项式过于庞杂的问题
- 使用方法：setup()函数
- <\script setup> ：语法糖，无需导出，没有返回，所有顶层属性默认导出

组合式核心：
-  将配置文件提取到单独composition文件中，在模板文件中只需调用组合，并返回所需的数据

Vue3项目创建Vue实例：
- 特点：Vue3不存在构造函数——导致Vue2、3截断式兼容
- 创建样例：
	- import {createApp} from ‘vue’
	- import App from './app.vue'
	- createApp(App).mount('#app')

Vue3组件this指向：
- 在vue3中组件实例外嵌套了一层代理，组件中this指向代理，再由代理处理vue实例数据

Vue3组件配置项：
- Vue3中组件配置使用组合式（composition）api取代选项式（option）api

Vue3取消了构造函数的原因：
- 调用构造函数会对所有vue实例生效，不利于隔离应用
- vue2集成了太多功能，不利于treeshink，vue3将这些导出，能够充分利用treeshink减小打包体积
- vue2没有区分组件实例和vue应用，vue3中把两个概念区分开来，createApp创建的对象，是一个vue应用而不是一个组件


生命周期函数的变化：
- 1、语法变化：beforeMount->onBeforeMount
- 2、使用ref定义响应式，代码可直接置于setup中，取消了created和beforeCreated
- 3、destroyed改为了onUnmounted
- 使用方法：导入后直接用调用函数：onMounted(()=>{})