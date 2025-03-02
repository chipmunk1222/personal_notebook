vue3响应式原理：使用统一的代理函数设置代理对象，只需访问代理对象即可实现数据响应式
vue2响应式原理：递归遍历所有对象，设置getter和setter


**响应式状态：**
*ref()：*
- 在组合式api中使用ref()函数来声明响应式状态
- 样例：
	- import {ref} from ‘vue’
	- setup(){
		- const count = ref(0)
		- return{
			- count
		- }
	- }
- 详解：ref()接收参数，并返回一个ref代理对象，该对象仅包含value属性，访问参数：count.value，如参数为对象，则value内部将设置reactive
- 参数调用：在setup()函数中添加参数的返回值{return {count}}
- 注：在模板中使用参数时，为方便期间vue3会自动解包从而无需附加.value
- 深层响应：ref具有深层响应式，在嵌套对象中也可以检测数据变化
- ref()解包机理：
	- 模板或被reactive()调用时会自动解包
	- ref()作为数组或集合时不会自动解包，需要使用.value属性
	- 只有对象中的顶级ref属性才会被自动解包

*computed():*
- 作用：相当于Vue2的计算属性，返回ref object代理
- 样例 const res = computed(()=>{return a+b})
- ref和computed都是ref object格式代理（要加value），reactive和readonly是reactive格式代理

*reactive():*
- 作用：reactive()函数用来使对象本身具有响应性（ref()是将参数包裹在一个对象中）
- 样例：
	- import {reactive} from ‘vue’
	- const state = reactive({count：0})
	- 调用：state.count
- 注：reactive()返回的是一个原始对象reactive的代理(深层赋值原始对象)，并不等同于原始对象；对代理使用reactive会返回自身
- reactive()的局限性：只能持有原始对象类型（对象、数组、集合、Map），不能持有原始类型（String，Number，Boolean）；不能重新赋值；解构后会丢失响应式

*readonly():*
- 作用：readonly()函数用来设置只读对象代理，用法等同于reactive()
- 注：readonly代理和reactive代理不是一个代理，同时使用时会在外部嵌套代理

**监听数据变化：**
*watchEffect：*
- 作用：监听响应式数据变化
- 样例 import {watchEffect} from ‘vue’
	- const stop = watchEffect(()=>{})    //传入一个函数并立即执行，返回一个函数
	- stop()           //调用返回的函数立即停止监听
- 特点：自动跟踪内部参数，当内部参数变化时自动执行
*watch：*
- 作用：用法近似于vue2中的watch
- 样例：import {watch} from ‘vue’
	- watch('watchobjname'，（newValue，oldValue）=>{}，options)
- 注：1、watch监听的只能是一个对象，如果要监听原始数据，需要传入函数 ()=>obj.value
	- 2、watch可同时监听多个对象，watch(\['name1','name2'],(\[new1,new2],\[old1,old2])=>{})
- watch使用场景：1、希望一开始不调用；2、需要比对旧值；3、结果不希望包含监控对象

**响应式工具：**
- isref：检查某个值是否为ref对象
- isProxy：检查某个值是否为reactive格式代理对象
- isReactive：检查某个值是否为reactive创建的代理对象
- isReadonly：检查某个值是否为readonly代理对象
- unref：语法糖，如果一个值是ref，返回ref.value；否则返回value
	- const val = unref(x)
- toRefs：将对象内的数据转化为ref类型，用以解构时保持响应式
	- const stateRef = toRefs(state)
	- 结果：stateRef：{ a:refobj,b:refobj}