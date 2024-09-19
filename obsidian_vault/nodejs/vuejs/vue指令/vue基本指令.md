定义：带有v-前缀的标签属性，可以实现特殊功能

v-html：
- 用来动态设置元素innerhtml（带标签的表达式）
- 语法：v-html=“表达式”
- 注：配置相中的数据要使用引号

v-show、v-if:
- 控制界面的显示隐藏
- 语法：v-show=“表达式”，v-if=“表达式”（true / false）
- 表达式可以用预先渲染的数据，直接用，不能用插值法
- v-show原理：控制display：none控制显示，适用于需要反复切换的场景
- v-if原理：基于条件判断，是否创建或者移除节点，适用于不需要频繁切换的场景

v-else-if、v-else：
- 用以辅助v-if进行多条件判断
- 必须紧跟v-if使用，不可单独使用

v-on（@）：
- 作用：添加监听和处理逻辑
- 语法1：v-on：事件名=“内联语句”（适用于简单语句）
- 语法2：v-on：事件名=“methods的函数名”
- 简写：@事件名=“语句”

v-bind：
- 作用：1、动态设置html的标签属性2、对vue内置的各参数进行绑定，如key，props
- 语法：v-bind：属性名=“表达式”
- 简写：：属性名=“表达式”
- 特点：v-bind同时可动态控制类名和样式的调用
- 语法：：class\\style="{属性名：’属性值‘}"
- 样式修改主要用途：用来修改被组件预定义的样式

v-for：
- 作用：基于数据循环，多次渲染元素
- 语法：v-for=”（item，index）in 数组“（注意空格）
- item：每一项名称，index每一项下标（可省略）
- 常用于数组遍历，也可遍历对象、数字等
- v-for的key：给列表每一项加一个唯一标识
- key的注意点：只能是数组或数字，且必须唯一

v-model：
- 作用：给任意表单元素使用，双向数据绑定，用于快速获取或设置表单内容（视图和数据的绑定）
- 语法：v-model=“变量”
- v-model.trim：首尾去空格
- v-model.number：转数字 
- v-model拆解：value+对应事件的合写
- 对input框 :value=属性+@input事件的合写，@input = $event.target.value获取形参

v-slot：
- 作用：使组件像html标签一样可以插入具体内容
- 语法：v-slot：插槽名，在组件中写入<\slot name=""><\\slot>
- 简写：#插槽名
- 注：如果调用组件时需要多个插槽，用<\template>包裹内容块以便于识别
- slot参数传递：在组件内部slot位置添加想传递参数如：row=item msg=“”，在父组件内通过template包裹，并使用#插槽名（default）=“对象名”接收参数

指令修饰：
- 定义：对事件条件的封装
- 样例： @keyup.enter：按键enter弹起时触发、
- @事件名.stop：阻止事件冒泡
- @事件名.prevenet：阻止事件默认行为

自定义指令：
- 定义：根据自己定义的指令，封装一些dom操作，扩展额外功能
- 全局注册指令：
- Vue.derective('指令名',{
	- //在dom元素被添加时，获取绑定dom元素
	- inserted(el){
		- el.focus()
	- }
	- 在dom元素变动时，获取绑定dom元素
	- update(el,binding){
		- this.style.color = binding.value
	- }
- })
- 调用：v-focus
- 局部注册：
- directives：{
	- 指令名：{
		- inserted（el）{
			- el.focus()
		- }
	- }
- }