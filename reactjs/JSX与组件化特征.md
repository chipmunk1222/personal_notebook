[react官方网址]([在 JSX 中通过大括号使用 JavaScript – React 中文文档](https://zh-hans.react.dev/learn/javascript-in-jsx-with-curly-braces))
# react组件化
**react组件化vsVue的组件化**
现代框架绕不开的一点是基本都用组件化的思维来看待项目，这点在`React`和`Vue`这两个最流行的前端框架中尤为明显，但两者对组件的定义仍然有所区别：
1. `react`使用`JSX`来描述组件结构而`Vue`则使用`<template>`、`<style>`和`<script>`三部分来区分组件结构，这点应该`react`最为显著的特点，通常一个包含`JSX`的函数就能被看作一个组件
2. `react`中使用单向数据流（`props`）来进行父子组件间的通讯，虽然`Vue`中也保留了这一点，但这点在`react`中将更加显著
以这段代码为例，`Avatar`就可以被视为一个组件，`<Profile>`当然也是
```js
function Avatar() {
  return (
    <img
      className="avatar"
      src="https://i.imgur.com/1bX5QH6.jpg"
      alt="Lin Lanying"
      width={100}
      height={100}
    />
  );
}
  
export default function Profile() {
  return (
    <Avatar />
  );
}
```
# JSX规则
`JSX`和`html`非常相似，甚至看起来就是`html`外套一层`()`，但实际上`JSX`是一种`javascript`，也因此，它还有许多看不见的"规范"

如果需要，可以使用转化器实现`JSX`和`html`之间的转化[JSX转化器]([Transform](https://transform.tools/))

## `JSX`只允许有一个根元素
 `JSX`只允许有一个根元素，如果要想在一个组件中包含多个元素，需要用一个父标签把它们包裹起来
```js
<div>  
	<h1>海蒂·拉玛的待办事项</h1>  
	<img  
	src="https://i.imgur.com/yXOvdOSs.jpg"  
	alt="Hedy Lamarr"  
	class="photo"  
	>  
	<ul>  
	...  
	</ul>  
</div>
```
如上述例子，多个标签需要一个根元素来包裹
同时，如果不想引入额外的元素，在`JSX`中可以使用`“<> </>”`来作为根元素，这被称为`fragment`

## `JSX`中的标签必须闭合
- 自闭合标签如`<img>`必须写成`<img />`
- 非自闭合标签则必须闭合

## JSX动态插值
动态插值，这一点再次佐证了在`react`中，`JSX`是描述组件构成的基本结构
一般来说，在函数使用`{ }`的都是动态绑定或插值的内容（在参数中使用`{ }`往往用作解构），如果加上`" "`则会使一切插值常量化

在`Vue`中是如何实现这种动态插值的呢
1. 使用`{{ }}`实现文本的插值
2. 使用`v-bind`实现标签属性的动态绑定

`react`中的`{ }`即同时涵盖了以上两个功能，包括：
1. 可以动态绑定变量和文本
2. 可以动态绑定变量和标签属性
3. 使用`{{ }}`来动态绑定*对象*甚至
4. `{ }`也可以动态绑定*函数*，以作为事件触发媒介
同时也要遵守一些规范
1. 不允许在文本中直接绑定对象，因为会引发渲染错误
2. 使用标签属性的动态绑定时使用驼峰命名法
3. 不能直接动态绑定标签
总而言之，加上`{ }`基本就意味着对相应数据添加动态绑定了

>这里还有其他需要注意的规则，例如`class`要在`JSX`中写成`className`，因为`JSX`本质上仍是`javascript`
>在`JSX`中命名一般使用小驼峰命名法等
# 组件数据流
## 使用props进行数据传递
我们说在`react`中一个组件的基本结构是一个包含`JSX`的函数，而作为一个函数自然就有参数的使用空间
这个参数的位置正是实现`react`数据流的位置，即父组件通过这个参数(`props`)向子组件进行数据传递，从而使得我们可以在父组件中动态定义子组件的`JSX`标签信息

介绍两个非常常用的数据流特性，一是解构赋值，而是展开运算符
**解构赋值**
在子组件中直接提取参数，从而使参数统一
```js
function Avatar({ person, size }) {  
// 在这里 person 和 size 是可访问的  
}
```
**展开运算符**
父组件要同时传递多个数据时，使用展开运算符可以简化传递参数的写法
如下案例：
```js
function Profile({ person, size, isSepia, thickBorder }) {  
	return (  
		<div className="card">  
			<Avatar  
			person={person}  
			size={size}  
			isSepia={isSepia}  
			thickBorder={thickBorder}  
			/>  
		</div>  
	);  
}
```
以上跨层级数据流案例中，处于中间位置的`Profile`并没有对参数的再加工，所以直接展开能极大地简化写法

可以写成：
```js
function Profile(props) {  
	return (  
		<div className="card">  
			<Avatar {...props} />  
		</div>  
	);  
}
```
同时，`<Avatar>`组件中也可以直接解构参数

## 事件冒泡与回调触发
从上述介绍来看，`react`和`vue`在单向数据流层面有许多共同点，区别在于`Vue`中往往需要预先定义一个`props`配置项，取而代之的是`react`中通过直接解构的方式获取参数

另外，这么看貌似`react`中没有类似`emit`的事件触发机制，但这点同样可以用`props`来实现，即通过传递函数的`props`并通过回调来实现父组件中的触发

```js
// 父组件
import React, { useState } from 'react';
import ChildComponent from './ChildComponent';

function ParentComponent() {
  const [message, setMessage] = useState('');

  const handleMessage = (msg) => {
    setMessage(msg);
  };

  return (
    <div>
      <h1>Parent Component</h1>
      <p>Message from Child: {message}</p>
      <ChildComponent onSendMessage={handleMessage} />
    </div>
  );
}

export default ParentComponent;

// 子组件
import React, { useState } from 'react';

function ChildComponent({ onSendMessage }) {
  const [inputValue, setInputValue] = useState('');

  const handleClick = () => {
    onSendMessage(inputValue);
  };

  return (
    <div>
      <h2>Child Component</h2>
      <input
        type="text"
        value={inputValue}
        onChange={(e) => setInputValue(e.target.value)}
      />
      <button onClick={handleClick}>Send Message</button>
    </div>
  );
}

export default ChildComponent;
```

**取消默认事件**
有时事件触发时，我们想要阻止其一些默认行为，因此需要添加一些阻止代码
1. `e.stopPropagation()`：阻止事件向上层冒泡
2. `e.preventDefault()`：阻止表单类事件的默认提交
## 将组件作为props参数
类似于`Vue`中`slot`的用处，可以将组件（`JSX`）作为参数传递，从而实现组件嵌套
```js
import Avatar from './Avatar.js';

function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}

export default function Profile() {
  return (
    <Card>
      <Avatar
        size={100}
        person={{
          name: 'Katsuko Saruhashi',
          imageId: 'YfeOqp2'
        }}
      />
    </Card>
  );
}
```
