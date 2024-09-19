框架定义：实现跨端需求、兼容h5、各厂商小程序、app等场景的跨端框架
使用特色：条件编译：可以编写适配不同端的代码，最后生产环境只保留对应端的代码，减小体积
api：[unidemo.dcloud.net.cn/api/news](https://unidemo.dcloud.net.cn/api/news)

移动端生命周期钩子：
- 新增：添加了页面的生命周期和应用的生命周期
- 引入：import {name} from '@dcloudio/uni-app'
- 常见新增钩子：
	- onLaunch(options)：应用启动时触发，options参数包含应用被打开的场景值
	- onShow(options)：应用进入前台时触发，options参数包含应用被打开的场景值
	- onHide()：应用进入后台触发，没有参数
	- onLoad(options)：页面加载完成，options包含页面参数
	- onUnload()：页面销毁时触发，没有参数

uni-app数据请求：
- 基本使用：const res = uni.request({
	- url:String         //请求路径
	- data: Object    //请求参数
	- method: String  //请求方法
	- header:Object   //配置请求头
	- success:Function  //请求成功后操作，具有请求结果的默认参数 
	- fali:Function          //请求失败后的操作，具有请求结果的默认参数
	- complete:Function   //请求结束后的操作，具有请求结果的默认参数
- })
- 特性：如果希望用一个对象接收，则必须添加一个处理函数，否则返回Promise对象


uniapp路由配置：
- tabbar底栏配置：
	- color：字体颜色
	- selectedColor：选中字体颜色
	- backgroundColor：背景颜色
	- borderStyle：边框样式
	- lists： \[{
		- pagePath：路径
		- iconPath：图标路径
		- selectedIconPath：选中图标路径
		- text：名称
	- }]   //底部导航栏配置
- 注：底部导航栏配置不少于两项

- uni.setTabBarItem：设置底栏api
- 样例：uni.setTabBarItem：{
	- index：0，
	- text：‘text’，
	- iconPath：‘url’，
	- selectedIconPath：‘url’
- }
- 补充：index表示对应的底栏的项，其余部分等同于底栏初始化

uniapp路由跳转：
- 基本使用：uni.navigateTo({url:""})  //打开对应路径
- 可使用uni.navigateBack返回先前跳转的页面