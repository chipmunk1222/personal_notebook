安装依赖：npm install pinia
*pinia实例创建：*
- 引包：import {createApp} from ‘vue’
		import {createPinia} from ‘pinia’
		import App from './app'
- 创建实例：const app = createApp(App)
			const pinia = createPinia()
- 注入：app.use(pinia)
- 挂载：app.mount('#app')

*store:* 
- 定义：保存状态和业务的实体
- 使用场景：包含可以在整个应用中访问的数据，需要在页面中保存的数据
- 使用方式：
	- import {defineStore } from 'pinia'
	- export const useCountStore = defineStore('counter',{options}/()=>{params})  //第一个参数指定一个独一无二的名称，第二个参数指定配置/组合式函数
	- 使用仓库：
		- import {useCountStore} from ‘./store/useCount.js’
		- const useCount = useCountStore()
- 选项式：
	- state(data)：()=>({count:0})，   //函数，返回值为一个对象
	- getters(computed)：{
		- double：(state)=>{state.count\*2}
	- }，
	- actions(method)：{
		- increase(){
			this.count++
		- }
	- }
	- 注：这里this指针的用法类似于选项式的用法，直接指向仓库，可以直接调用实例
- 组合式：
	- export const useCounterStore = defineStore('counter', () => { 
		- const count = ref(0)
		- const doubleCount = computed(() => count.value * 2) 
		- function increment() { count.value++ } 
		- return { count, doubleCount, increment }
	- })
	- 注：组合式使用方式等同于组合式api，需要导入ref函数等实例，不过也可以导入监听器等配置使仓库更加灵活
-  解构：
	- storeToRefs：用来解构仓库响应式数据(state,getter)
	- 注：pinia实例是响应式的，要保持响应式应该使用数组调用，直接解构会导致响应式丢失