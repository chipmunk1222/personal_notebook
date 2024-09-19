**组件定义：** 一个.vue文件被称作单文件组件（SFC）

**组件注册：
- 全局注册：const app = createApp({})
	- app.component("componentname",component).component("name2",component2)
- 局部注册：在  \<setup>选项中，组件可以直接被导入，无需注册
- 注：组件注册建议使用大驼峰命名法

**组件传递：**
*父传子：*
- 原理：在 \<setup>选项中，传递标签需要用defineProps宏，返回一个对象，包含所有传递的所有props
- 样例：const props = defineProps(\['title'])，传递值可以是数组或对象，校验方式等同于vue2
- 调用：props.title
- 注：参数建议使用小驼峰命名法
*子传父（事件监听）：*
- 原理：在 \<steup>选项中，使用defineEmits宏传递事件，
- 样例：const emit = defineEmits(\['eventname'])
- 使用：function buttonClick() { emit('eventname',params) }，参数方式等同于vue2
- 注：如果显示地使用了setup函数,而不是 \<setup>,则需要通过emits选项定义:emits:\['eventname'],再使用上下文对象调用:setup(props,ctx){ ctx.emit('eventname')}
- 事件校验：可以在抛出事件前校验其是否合法
- 样例: const emit = defineEmit({
		 submit:({name,password}){
			 return name&&password
		 }
	- })  //通过返回值判断是否合法(需要抛出)
	- function submitForm(email, password) { emit('submit', { email, password }) }

*v-model组件绑定：*
- 原理：在 \<setup>标签下，使用defineModel宏实现双向绑定
- 样例：const model = defineModel()   
		\<input v-model = "model">
- 注：defineModel返回值为一个ref
- 底层机制：const props = defineProps(\['modelValue'])
	- const emit = defineEmit(\['update:modelValue'])
	-  \,\<input :value="props.modelvalue" @input="emit('update:modelValue',$event.target.value)">
	- 解释：update:modelValue表示传递的update事件，加入:modelValue是为了区分参数
- v-model参数传递：
- 原理：v-model接收一个参数用来在父组件中指定绑定对象，从而实现多绑定
- 样例：const model = defineModel('modelname')
	- 子组件： \<input v-model="model">
	- 父组件： \<input v-model:modelname='name'>
- 附加：如果要为底层props添加额外配置项，可以在第二个参数中添加

*透传Attributes：*
- 原理：在父组件调用子组件时传入了没被声明的props或emit时，该属性会被直接加到子组件的根节点上，若为多节点则不会添加，除非添加v-bind:$attr指定
- 事件监听器继承：如果传入没有被声明的事件，则在子组件中的行为会触发父组件事件，如果传入了事件，则会同时触发两个事件
- 实例参数 \$attr：在子组件中可以使用$attr可以接收透传属性