DOM节点：
- 层级：DOM以document为根节点，后续文档元素以树形节点排列
- childNodes数组：存储子nodelist节点
- dom.hasChildNodes()：返回true说明有一个或多个子节点
- 操作dom节点：
	- dom.appendChild(node)：在nodelist末尾添加节点
	- dom.insertBefore(node,dom.childNodes\[num])：在指定位置前插入节点
	- dom.replacChild、removeChild(node,poi)：替换、删除指定位置的节点
	- dom.cloneNode(bool)：复制节点，传入true表示深复制，复制完后节点为“孤儿节点”
- 获取dom节点：
	- document.getElementById('id')：通过id获取节点
	- document.getElementByTagName('name')：通过标签获取dom元素
	- document.getElementByClassName('classname')：通过类名获取dom元素
	- document.querySelector('css选择器')：通过css选择器获取dom元素
	- document.querySelectorAll('css选择器')：返回符合条件的nodelist
	- 元素遍历：
		- dom.firstElementChild：返回元素第一个子节点
		- dom.lastElementChild：返回元素最后一个子节点
		- dom.nextElementSibling：返回元素后一个兄弟节点
- 修改dom节点信息：
	- dom.getAttribute('attr')：获取属性值，属性包括id、class、title等
	- dom.removeAttribute('attr')：删除属性
	- dom.setAttribute('attr',value)：修改属性值
- 创建dom节点：
	- document.createElement('div')：创建dom节点
	- 修改元素信息：
		- .innerHTML：修改标签内内容（识别标签）.innerText修改标签内内容
		- 修改样式：.style.属性=new 属性值
		- 修改类名：.classList=‘类名’ 后缀：.add('类名') .remove('类名') .toggle（'类名'）

事件：
- 事件流：
	- 冒泡事件流：嵌套容器中的事件由具体的事件到不具体的事件的顺序触发
	- 捕获事件流：由不具体的容器到具体的容器捕获事件
	- DOM事件流：DOM2规定事件流分为三个阶段：事件捕获，到达目标和事件冒泡
- 事件处理函数：
	- onclick、onload：DOM0事件处理函数
	- addEventListener(type,handler,false)：DOM2事件处理函数，第三个参数表示在冒泡阶段处理事件
	- removeEventListener：移除事件处理函数
	- event对象，所有事件处理函数中都会有一个默认的event对象指向事件本身
- 事件类型：
	- 用户界面事件(UIEvent)：涉及BOM交互的浏览器通用事件
		- load：在窗口内容完全加载后触发
		- unload：当window页面完全卸载后触发
		- select：在文本框中选择了字符后触发
		- resize：window窗口被缩放时触发
		- scroll：在包含滚动条的元素上滚动时触发
	- 焦点事件(FocusEvent)：在元素获得和失去焦点时触发
		- blur：失去焦点时触发
		- focus：在获得焦点的元素上触发
	- 鼠标事件(MouseEvent)：使用鼠标操作时触发
		- click：单击触发
		- dbclick：双击触发
		- mouseover：鼠标悬浮触发
	- 滚轮事件(WheelEvent)：使用鼠标滚轮时触发
		- mousewheel：滚轮事件
		- event.wheelDelta：滚轮滚动参数
	- 输入事件(InputEvent)：向文档中输入文本时触发
	- 键盘事件(KeyboardEvent)：使用键盘时触发
		- keydown：按下某个键时触发
		- keyup：某个键弹起时触发


js异步api：
- setInterval（function，time）：添加间隔触发器
- clearinterval（'intervalname'）：删除触发器
- settimeout（function，time）：设置定时器 
- Promise对象：保证数据返回
- Promise语法：
- 创建promise方法对象：
- Let myPromise = new Promise（function（myResolve，myReject））{  
	myResolve（）；//执行成功
	myReject（）；//执行失败	
	}
	myPromise.then(
		function(value){"表达式"} //执行成功返回
		function(error){"表达式"}	//执行失败返回
	)
- jsAsync：用async标示Promise函数，用await充当function().then()部分
- 模板：async function func1(){ let x = await value}

jsfetchapi：
- 通过let x = await fetch(file)异步获取服务器文件，
- javascript获取web上的json格式数据注意点：
	- 可使用let {y} = x.json()直接获取
	- 赋值元素与json中的头元素对应
	- 后续元素可通过对象或数组直接访问


