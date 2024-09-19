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
- el指定挂载点（指定管理的盒子），data提供渲染数据（实例中内容），computed（计算属性），methods提供方法（函数）
- data（）{return{ 对象、规则}}
- methods项：预先编写可调用的函数，可以在注册事件中直接调用，引用时可不加括号（无参数）

- computed项：计算属性和data属性并列，调用方法相同，引用时不能加括号
- components项：提供外部引入组件，便于直接调用，调用方式\<组件名 />
- props项：用以从父文件向子文件传递参数

- router参数：写在最外层框架中，用于指示页面跳转，子列表参数用于指示同一个页面内部内容跳转，router-view：动态显示当前路由下的内容



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
- 生命周期四阶段：1、创建实例2、挂载3、更新数据4、销毁
- 生命周期对应8个状态1、befor Create2、created3、beforeMount4、mounted5、beforeUpdate6、updated7、beforeDestroy8、destroyed
- mounted生命周期钩子表示在Vue组件完成初始化渲染并创建DOM节点后运行，即页面展示运行
- mounted与el：el表示Vue实例创建即绑定对应DOM元素，mounted表示渲染完成后触发
- mounted与watch：watch表示数据有修改则触发，mounted表示渲染周期内运行
- updated与watch的区别：updated在DOM元素变化后触发，watch表示数据变化

侦听器（watch）：
- 作用：监视数据变化，执行一些业务逻辑或异步操作，数据变化就执行相关操作
- 语法：属性名（new，old）{”表达式“}
- 注：若监听对象为对象内属性，在方法名上加引号
- 配置项：
	- deep：true 对对象内部所有数据的监视
	- 注：对对象的监视要在watch中写完整写法
	- obj：{
		deep：true
		handler(newval){"表达式"} 
	- }
	- immidiate：true 表示初始状态下立即执行一次