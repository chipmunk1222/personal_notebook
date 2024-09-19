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
- 自定义位置删除：splice（index，number）
- 数据filter方法：let res = array.filter(function(){})，用以对数组进行过滤操作，
- 数组map方法：let res = array.map(function(){})，用以对数组中所有相同元素做对应操作，数组长度不变
- 数组reduce方法 let res = array.reduce((acculator,item)=>acculator+item,initialvalue),用以对数组进行累加操作
- 数组join方法 let res = array.join(“、”)合并数组并以字符串返回，以顿号拼接

匿名函数：
- 函数表达式语法：let fn=function（）{ }
- 特点：将函数赋值给对象，可以通过对对象的调用实现函数调用
- 立即执行函数：（function（）{ }）（）；或（function（）{ }（））

箭头函数：
- 语法：const fn=（参数）=>{函数体}
- 特点：极致的简洁写法，一个参数可以省略小括号，一行函数体可以省略大括号
- 箭头函数修改对象时在函数体大括号外再包一个小括号

异步调用：
1、回调函数：
- 定义：function fn1（val1，val2，MyCallback）{表达式}，
- 调用：fn1(val1,val2,fn2)
2、异步调用：
- 单次延时调用：setTimeout(myFunction, 3000)
- 间隔调用：setInterval（myFunction，1000)

解构赋值：
- 模板：let  {results}  = list
- 等效于：let results = list.results
- 用法：用于将对象中的同名属性直接赋值给变量，多用于api数据传递