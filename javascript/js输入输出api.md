# 输入
读取一行输入：readline()
至多读取1024个字符

读取多行：while((line = readline())!='')
使用 let arr = line.split(‘ ’)接收

读取n个字符：gets(n)

读取一个长整数：readInt()
读取一个浮点型：readDouble()

```js
var a, b; 
var solveMeFirst = (a,b) => a+b; 
while((a=readInt())!=null && (b=readInt())!=null){ 
	let c = solveMeFirst(a, b); 
	console.log(c); 
}
```

```js
var line; 
var solveMeFirst = (a,b) => a+b;
while((line = read_line()) != ''){ 
	let arr = line.split(' ');
	let a = parseInt(arr[0]); 
	let b = parseInt(arr[1]); 
	let c = solveMeFirst(a, b); 
	console.log(c); 
}
```
# 输出
不加回车的输出：print(sth,...)
空格分隔参数

带回车的输出：console.log(sth,...)、print(sth,...)
