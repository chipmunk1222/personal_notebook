实例创建：
1、准备容器：
- 在流程代码中添加容器（div块等）
2、引包：
- 利用脚本调用对应网站的包
- 开发版本用于开发调试（包括警告和调试），生产版本用于发布
- 开发版本包<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
- 生产版本包<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16"></script>
3、创建实例
- 非vue文件通过构造函数创建Vue实例
- const app = new Vue（{el、data、methods、computed}）
- vue文件：export default{}
4、添加配置项->完成渲染
- 在创建出来的对象块中添加数据


vue核心概念：
- 注入：vue会将vue实例注入到创建的对象中，包括data、computed、method等，可在浏览器中直接查询
- 虚拟DOM：vue模板并不是真实的DOM，而是虚拟DOM，虚拟DOM本质上是一个字符串，vue内部会根据虚拟DOM生成真实DOM（vnode树），这个过程被称为vue渲染，通过虚拟DOM节点的对比修改数据，从而提高效率，vue渲染使用render()函数的返回值生成vnode，从而创建真实DOM
- 流程：实例创建->注入->创建虚拟DOM->挂载->渲染（数据修改）->完成渲染（返回）

**配置项：**
- el指定挂载点（指定管理的盒子），等同于$mount('css选择器')，data提供渲染数据（实例中内容），computed（计算属性），methods提供方法（函数）
- data（）{return{ 对象、规则}}
- methods项：预先编写可调用的函数，可以在注册事件中直接调用，引用时可不加括号（无参数）

- computed项：计算属性和data属性并列，调用方法相同，引用时不能加括号
- template项：在vue实例中提供DOM模板

- components项：提供外部引入组件，便于直接调用，调用方式\<组件名 />
- props项：用以从父文件向子文件传递参数
- 生命周期钩子：在页面创建各个阶段执行相关操作
- watch侦听器：对组件进行侦听，若组件变化执行相关操作

- router参数：写在最外层框架中，用于指示页面跳转，子列表参数用于指示同一个页面内部内容跳转，router-view：动态显示当前路由下的内容

- render:用来手动渲染vnode树

状态选项：
计算属性（computed）：
- 计算属性语法：属性名（）{return：返回值}
- 计算属性和方法的区别：计算属性调用后会存入缓存，再次调用时直接读取缓存->性能高
- 计算属性完整写法：属性名：{get（）{ }，set（）{ }}，get用于设置返回值，set用于修改
- 注：计算属性也是动态绑定的

传递项（props）：
- 作用：用以将父列表参数向子列表传递
- 使用方法：被传递项写props参数，在父列表中调用子列表组件时，通过v-bind绑定参数
- 语法：props：\[item1,item2]

路由（router）：
- 路由是Vue下的一个单独组件，用来记录页面信息


生命周期钩子（如mounted）：
- 生命周期四阶段：1、注入（导入data）2、生成VNode3、挂载真实DOM4、更新数据5、销毁
- 生命周期对应8个状态1、befor Create2、created3、beforeMount4、mounted5、beforeUpdate6、updated7、beforeDestroy8、destroyed
- mounted生命周期钩子表示在Vue组件完成初始化渲染并创建DOM节点后运行，即页面展示运行
- mounted与el：el表示Vue实例创建即绑定对应DOM元素，mounted表示渲染完成后触发
- mounted与watch：watch表示数据有修改则触发，mounted表示渲染周期内运行
- updated与watch的区别：updated在DOM元素变化后触发，watch表示数据变化

侦听器（watch）：
- 作用：监视数据变化，执行一些业务逻辑或异步操作，数据变化就执行相关操作
- 语法：属性名（new，old）{”表达式“}
- 注：若监听对象为对象内属性，在方法名上加引号
- 样例： \["obj.childObj"](){}
- 完整写法：
	- obj：{
		deep：true   //表示是否监听内部属性变化
		handler(newVal，oldVal){"表达式"} 
		immidiate：true  //表示初始状态下立即执行一次
	- }

混入（mixins）：
- 作用：抽离重复代码以优化工程结构
- 语法：
	- 外部：mixins:\[function]
	- 内部：export default function(defaultValue = null){data(){return{}}
- 在外部文件中导出具体数据，在组件中定义函数来获取数据
- 特点：相当于把两个部分拼合在一起，相当于函数提取公共部分


**实例成员：**
- $mounted：挂载节点，作用等同于el配置项
- $emit：用于从子组件向父组件通信，
- 语法：子组件：$emit=("事件名"，参数)；父组件：@事件名=“方法名”
- $el：获取组件的真实DOM元素
- $event：事件参数，如果使用方法时不传参数，则默认参数即为事件参数，一般加上\.target选中对应元素
- $listeners：用于接收父组件调用子组件时的方法
- $on：事件总线用以接收数据