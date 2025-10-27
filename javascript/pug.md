官方文档链接：[pug官方文档]([Pug 模板引擎简介 | Pug 模板引擎中文文档 | Pug中文网](https://www.pugjs.cn/))
安装：
```node
npm install pug 
```
# pug是什么，做了什么
pug是一个基于javascript的高性能模板引擎·，其作用也就是使得开发更加高效，它的高效体现在以下几个方面
- 语法层面：pug是一门空格敏感的语法，通过空格替代html标签可以使开发更高效
- 文件层面：pug提供了一套文件编译方法，可以将一个模板编译成一个可多次使用、可传入不同局部变量渲染的函数

# pug模板编译
首先在项目中引入pug：
```js
import pug from 'pug'
```

1. pug.compile(source,?options)：把一个pug模板编译成一个可多次使用的模板，可传入不同参数
```js
/*
 * @param {string} source 需要编译的代码
 * @param {object} options （可选）选项
 * @returns {function} 模板函数 
 */
let fn = pug.compile("string of the pug",options)

let html = fn(args)
```
2. pug.compileFile(path,?options)：把一个pug文件编译成一个可多次使用的模板，可传入不同参数
```js
/*
 * @param {string} path 需要编译的代码的路径
 * @param {object} options （可选）选项
 * @returns {function} 模板函数 
 */
let fn = pug.compileFile("path of the pug",options)

let html = fn(args)
```
3. pug.render(source,?options)：传入一段pug代码，返回渲染出来的字符串
```js
/*
 * @param {string} source 需要编译的代码模板
 * @param {object} options （可选）选项
 * @returns {string} 渲染出来的html字符串 
 */
let html = pug.render("source of the pug",options)
```
4. pug.renderFile(path,?options)：传入一个pug文件，返回渲染出来的字符串
```js
/*
 * @param {string} path 需要编译的代码文件
 * @param {object} options （可选）选项
 * @returns {string} 渲染出来的html字符串 
 */
let html = pug.render("source of the pug",options)
```
5. pug.compileClient(source,options)：将pug文件编译成一个可以生成js文件的模板函数

>pug.compile()用于生成可复用的模板，pug,render()用作一次渲染

# 语法习惯
1. 插值语法`#{attr}`实现嵌入，`!{}`表示不转意嵌入
2. 在标签中可以直接使用所有js表达式
3. 使用管道符`|`表示纯文本
4. 样式属性`style`可以是一个字符串或一个对象
5. 类属性`class`可以是一个字符串或一个数组，或可以是映射`true`or`false`的对象(条件判断语法)
6. 类可以直接用`.`表示，`<div>`标签可以省略
7. 用`-`前缀表示不输出的代码，如变量定义等
8. 可以使用`include`来直接插入模板文件，也可以插入非`pug`文件

## 条件语法
if条件：
```js
- var user = { description: 'foo bar baz' }
- var authorised = false
#user
  if user.description
    h2.green 描述
    p.description= user.description
  else if authorised
    h2.blue 描述
    p.description.
      用户没有添加描述。
      不写点什么吗……
  else
    h2.red 描述
    p.description 用户没有描述
```
分支条件：
```js
- var friends = 0
case friends
  when 0
  when 1
    p 您的朋友很少
  default
    p 您有 #{friends} 个朋友
```

## 继承语法
通过extned和block实现子文件对父模板的填充
父模板：
```js
//- layout.pug
html
  head
    title 我的站点 - #{title}
    block scripts
      script(src='/jquery.js')
  body
    block content
    block foot
      #footer
        p 一些页脚的内容
```
子文件：
```js
//- page-a.pug
extends layout.pug

block scripts
  script(src='/jquery.js')
  script(src='/pets.js')

block content
  h1= title
  - var pets = ['猫', '狗']
  each petName in pets
    include pet.pug
```
>被block段声明的部分会替代模板中的内容

使用`append、prepend`实现添补
```js
//- layout.pug
html
  head
    block head
      script(src='/vendor/jquery.js')
      script(src='/vendor/caustic.js')
  body
    block content
```

```js
//- page.pug
extends layout.pug

block append head
  script(src='/vendor/three.js')
  script(src='/game.js')
```

## 迭代语法
普通迭代
```js
- var values = [];
ul
  each val in values
    li= val
  else
    li 没有内容
```
使用表达式：
```js
- var values = [];
ul
  each val in values.length ? values : ['没有内容']
    li= val
```
while语法：
```js
- var n = 0;
ul
  while n < 4
    li= n++
```

## 混入语法
混入使得代码中可以直接使用一整个代码块
模板：
```js
//- 定义
mixin list
  ul
    li foo
    li bar
    li baz
//- 使用
+list
+list
```
加参数：
```js
mixin article(title)
  .article
    .article-wrapper
      h1= title
      if block
        block
      else
        p 没有提供任何内容。

+article('Hello world')

+article('Hello world')
  p 这是我
  p 随便写的文章
```