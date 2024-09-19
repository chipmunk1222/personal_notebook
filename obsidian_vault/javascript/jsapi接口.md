javascript api组成：
DOM：操作文件内容
BOM：操作浏览器内容

获取DOM元素：
- 语法：const res=document.querySelector('css选择器')
- 返回匹配的第一个元素
- document.queryselectorall（）：获取全部元素，存入伪数组（推荐）

修改DOM属性：
- .innerHTML：修改标签内容（识别标签）.innerText修改标签内内容
- 修改样式：.style.属性=new 属性值
- 修改类名：.classname=‘类名’ 后缀名：.add('类名') .remove('类名') .toggle（'类名'）
- .classList:在原有类的基础上修改类名，不会覆盖原有类名
- .classList.add\/remove(’‘)：添加/移除类名，注：不能加.
- document.createElement('<>')：添加标签
- .appendChild()：添加元素


js方法：
- split（‘符号’）：以符号作为结束符，将子数据段用字符保存
- filter（function(item,index,arr)）：过滤数组，返回符合函数的数组
- 简写：filter(item=>item.function()）
- trim(‘字符串‘)：消除字符串两边空格
- map(function(item,index,arr)) ：按照函数处理数组，支持箭头函数简写

jsapi：
- 对象名.clientHeight：返回元素当前高度

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


