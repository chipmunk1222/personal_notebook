js特性：
- js对象特征：js会将符合语法规范的写法自动转为标准格式（语法糖），js的数组本质上是个对象，（包括length属性），js规范语法为中括号写法
- 隐式转换：js会隐式转换数据类型，可以通过隐式转换转换数据类型或字符串拼接
- 逻辑判断：短路规则，只有前面为真才判定后面的式子，返回最后一个判定的式子（非布尔），且NaN，undefined，null将判定为false
- 等于操作符： \=\=会进行强制类型转换，\=\=\=不进行强转，称为全等操作符
- 注释：通过@param {类型} 参数的注释方式进行类型提示
- 立即执行函数（防止全局污染）：(function)()，第一个括号声明函数表达式，第二个括号调用
- 浏览器重排、重绘：获取或修改页面元素时会对页面进行重排
- 当对象键值相同时，可以不写：，对象中的方法不用写function
- 标签语句：可以给语句加标签label：statement

js核心概念：
- 值和引用：只有对象属于引用类型，对象参数存放地址
- 数据作用域：js只有全局和函数两个作用域，内部访问外部作用域称为闭包，定义作用域的声明会提升到顶部（无视函数定义位置）
- 全局对象：window（浏览器），全局变量会被放入window全局对象中（跨文件使用参数，也称为全局污染）
- 构造函数：js所有对象本质上都是构造函数，使用new Object()创建，使用new Object()创建的数据本质是引用类型
- 原型：构造函数的默认构造，每个构造函数都有一个原型（prototype），每个实例都有一个隐式原型（\_\_proto__）,通过将方法写在构造函数原型上节省内存空间，使用in找到对象的所有属性，使用hasOwnProperty找到独有属性，使用instanceof确认原型
- 原型链：原型本身也是个对象，原型的对象是由object构造的，具有\_\_proto__指向object的原型，object的原型指向null，通过原型链可以影响到所有子对象，可以通过修改原型链来重构某些方法
- ![[Pasted image 20240527195545.png]]
- 事件冒泡：js监听子元素事件会在父元素触发，其分为捕获和冒泡两个阶段，addeventlistener第三个参数控制触发时机，默认false表示冒泡触发

js事件循环：
- 核心：单线程是异步的原因，事件循环是异步的实现方式
- 主要的浏览器进程：浏览器进程，网络进程，渲染进程（主要负责hmtl,css,js等代码 ）
- 事件循环本质：渲染进程中主线程的工作方式为无限for循环，每一次循环中使用消息队列进行事件任务排序
- 特点：任务没有优先级，消息队列有优先级，每个任务都有一个任务类型，同一类型必须分属同一队列，浏览器必须具备一个微队列，微队列必须先于其他队列执行
- 队列优先级：回调队列（中），交互队列（高），微队列（最高）

js函数技巧：
- js中函数的this指针指向函数的调用方式
- 改变this指向调用：js函数this指向取决于函数调用方式，可以使用call或apply改变this指向，调用方式为fn.call(this,a,b)，apply将参数写在一个数组里，bind用以创建函数实例时使用
- 防抖：使用不断清除定时器并重新设置的方式解决监听耗时事件重复触发问题

外部输入输出控制：
- document.write(\`表达式\`)：页面中打印输出(反括号表示模板字符串)
- 注：若要输出html指令，则必须加引号，引号内元素可用正则表达式${ }输出
- console.log（‘表达式’）：控制台输出日志
- alert（‘表达式’）：弹窗输出
- prompt（‘表达式’）：弹窗输入（可接收）


数组操作：
- 数组操作后会有返回值，返回值为新数组长度
- 数组后增、减：push（），pop（）
- 数组前增、减：unshift（），shift（）
- 自定义位置删除：splice（index，number，\[new array]）
- 自定义位置拷贝：slice（index，number）
- 数据filter方法：let res = array.filter(function(){})，用以对数组进行过滤操作，
- 数组map方法：let res = array.map(function(){})，用以对数组中所有相同元素做对应操作，数组长度不变
- 数组reduce方法 let res = array.reduce((acculator,item)=>acculator+item,initialvalue),用以对数组进行累加操作
- 数组find方法 let res = array.find(function(){})
- 数组some/every方法,寻找是否存在/全是 let res = array.some(function(){})
- 数组join方法 let res = array.join(“、”)合并数组并以字符串返回，以顿号拼接

匿名函数：
- 函数表达式语法：let fn=function（）{ }
- 特点：将函数赋值给对象，可以通过对对象的调用实现函数调用
- 立即执行函数：（function（）{ }）（）；或（function（）{ }（））

箭头函数：
- 语法：const fn=（参数）=>{函数体}
- 特点：极致的简洁写法，一个参数可以省略小括号，一行函数体可以省略大括号
- 箭头函数修改对象时在函数体大括号外再包一个小括号
- 箭头函数特性：只有在一个参数时才可省略小括号，只有在返回单行表达式时才可省略大括号和return，如果箭头函数用大括号包裹，则必须有return返回值，返回单行对象需要用小括号返回表达式，箭头表示this，无法使用call，apply重定义this
- 剩余参数列表：使用...args以数组的形式接收剩余参数

异步调用：
1、回调函数：
- 定义：function fn1（val1，val2，MyCallback）{表达式}，
- 调用：fn1(val1,val2,fn2)
- 概念：回调地狱：反复使用回调函数导致冗长的回调嵌套
2、Promise方法：
- 定义：Promise为一个对象，用来处理异步场景下任务结果的情况。
- 定义语法：function fn(){return new promise((resolve,reject)=>{'表达式'})//参数resolve、reject为函数
- 处理语法：fn.then((data)=>{},(reason)=>{})，一般只用于处理成功场景
- 处理语法：fn.catch((data)=>{}) == fn.then(null,(data)=>{})，一般只用于处理失败场景
- Promise的链式调用：Promise的处理结果返回的也是个Promise对象，也可进行状态处理，从而达到链式效果，若没有对应状态处理函数则继承上一个Promise的处理结果
3、async/await方法：
- async定义：Promise语法糖，确保函数返回值为Promise
- await定义：Promise语法糖，等待函数完成，必须放在async函数中
3、异步计时器调用：
- 定时器：setTimeout(myFunction, 3000)
- 计时器：setInterval（myFunction，1000)
- 定时器和计时器都有一个id，可通过赋值获取id，根据id清除

展开运算符：
- 将数组/对象内容展开
- 语法:\[...array] = array
- 用法：使用展开运算符对数组/对象进行api操作

解构赋值：
- 模板：let  {results}  = list
- 等效于：let results = list.results
- 用法：用于将对象中的同名属性直接赋值给变量，多用于api数据传递

属性表达式：
- 模板：let propkey = "foo" let obj = {\[propkey]:true} =>{foo:true}
- 作用：1、使用变量作为属性名，从而简化属性运用
- 2、使用.value将value值完全绑定，使用属性表达式则相当于动态绑定数据，可有效应用于多种需要动态传递数据的场景

try/catch基础用法：
- try{}
- catch(error){console.log(error)}

特殊属性：
- location.pathname：返回浏览器当前路径
- location.hash：返回当前浏览器目录的hash值