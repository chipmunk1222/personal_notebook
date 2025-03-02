# State组件记忆
**问题场景描述**
当`react`组件中的数据发生改变时，`react`会重新渲染组件，然而重新渲染时`react`不能记忆修改的数据，就造成了每次都会将数据初始化
类比`vue`就好理解，因为`vue`将组件拆分为了`template`和`script`，因此`script`中的数据不会因模板的改变而受到影响，`react`中两者是一体的，因此就会受影响

## 使用state记忆数据
在`react`中引入的`state`的概念，用来存储需要持久化的数据
```js
import { useState } from 'react';
//替换
//let index = 0;
const [index, setIndex] = useState(0);
```
在`useState`这个`Hook`中，变量以数组的形式存放，需要使用时使用*数组解构*，即上述案例中的`const [index, setIndex] = useState(0);`

其中`index`和`setIndex`可以说分别代表`getter`和`setter`，`index`可以直接使用，如果需要改变则套上`setIndex(index+1)`
`useState()`中的值则为变量的默认值
>`State`的作用“只限于”最近的组件，也就是只能在最近的顶层组件中使用，也就是说在渲染了多个相同组件时，他们的`State`是相互独立的

## react渲染机制
`react`渲染一个组件分为三步，分别是触发、渲染和挂载
1. 触发：经由一系列事件或机制触发
2. 渲染：渲染组件
3. 挂载：将组件挂载到相应`DOM`上

**触发渲染**
组件在下列两种状态下会触发一次渲染
1. 初次渲染：当应用启动时，`react`会触发一次初次渲染
2. （组件或父组件）状态更新：这个状态包括*数据变量*、*UI状态*、*用户输入等*，当这些数据发生变化，组件会重新渲染
在初次渲染时，通过调用`createRoot`方法创建要渲染的节点
**渲染过程**
即`react`内部将组件渲染成能够挂载的`DOM`模板
本质为调用`render()`函数
**挂载组件**
`react`通过`appendChild()`方法将组件挂载到浏览器上下文中
只有渲染内容有区别时，才会触发重复的挂载功能

挂载单个节点代码示例：
```js
import Image from './Image.js';
import { createRoot } from 'react-dom/client';

const root = createRoot(document.getElementById('root'))
root.render(<Image />);
```
## state快照渲染
从上一节中我们得知`react`在状态变化时会重新渲染组件，当然也会追踪`state`中的变量

但我们说`state`是将变量状态持久化的一个工具，这里就有一些比较有趣的现象：
1. 无论重复调用几次变化的函数，`state`只记录最后一次变化
2. `state`的值在组件重新渲染后变化
分别对应以下样例：
```js
const [number, setNumber] = useState(0);

  <button onClick={() => {
	setNumber(number + 1);
	setNumber(number + 1);
	setNumber(number + 1);
  }}>+3</button>

// 相当于
<button onClick={() => {  
	setNumber(0 + 1);  
	setNumber(0 + 1);  
	setNumber(0 + 1);  
}}>+3</button>
```
在这个样例中`number`的值会变成1

```js
import { useState } from 'react';

export default function Counter() {
  const [number, setNumber] = useState(0);

  return (
    <>
      <h1>{number}</h1>
      <button onClick={() => {
        setNumber(number + 5);
        alert(number);
      }}>+5</button>
    </>
  )
}
```
在这个样例中`alert`的值为0

总结来说就是：
- `state`以快照的形式变化，只有组件渲染之后，`state`的值才会相应变化，否则都保持不变

## setState的本质
`setState`在先前的解释中相当于一个`setter`函数，但它相当于是对数据的套壳，就像`Vue`中套了一层`ref`就赋予数据响应式一样，但`setState`的本质仍是个函数，也由此产生一些新的特性：
- `setState(state+1)`的写法相当于一种简写，实际写法应当是`setState(state=>state+1)`
- 相对于“套壳”只在最后一次触发时改变，函数化的写法是可以继承的（这其实也好理解，只需要知道`state`是快照式的，那么函数化就能明显看出后一次是对前一次的覆盖）

因此，当我们想要连续做一些变化时，就可以写成如下形式
```js
setNumber(n => n + 1);  
setNumber(n => n + 1);  
setNumber(n => n + 1);
```
## 避免state突变mutation
突变`mutation`指的是绕过`setter`函数直接设置`state`的值，这样并不能在重新渲染时改变`state`的值（还是从快照理解），因此要在`setter`函数中完整写下新的值，而这在对象和数组中还有一些别的讲究
**展开对象**
保证包含了对象的全部成员，主要是不变的成员
```js
setPerson({  
	...person, // 复制上一个 person 中的所有字段  
	firstName: e.target.value // 但是覆盖 firstName 字段  
});
```
**嵌套对象**
```js
const [person, setPerson] = useState({  
	name: 'Niki de Saint Phalle',  
	artwork: {  
		title: 'Blue Nana',  
		city: 'Hamburg',  
		image: 'https://i.imgur.com/Sd1AgUOm.jpg',  
	}  
});

// setter
const nextArtwork = { ...person.artwork, city: 'New Delhi' };
const nextPerson = { ...person, artwork: nextArtwork };  
setPerson(nextPerson);

//等价于
setPerson({  
	...person, // 复制其它字段的数据  
	artwork: { // 替换 artwork 字段  
		...person.artwork, // 复制之前 person.artwork 中的数据  
		city: 'New Delhi' // 但是将 city 的值替换为 New Delhi！  
	}  
});
```

## 使用immer来兼容mutation
使用`immer`库可以兼容`mutation`
尝试使用 Immer:
1. 运行 `npm install use-immer` 添加 Immer 依赖
2. 用 `import { useImmer } from 'use-immer'` 替换掉 `import { useState } from 'react'`
这样就可以直接更改变量而不会导致渲染无效，从而可以减少拷贝

## 数组的改变
由于直接插入修改数组也会引起突变，因此用一些替代方案做相应操作

|      | 避免使用             | 推荐使用             |
| ---- | ---------------- | ---------------- |
| 添加元素 | push、unshift     | concat、\[...ary] |
| 删除元素 | pop、shift、splice | filter、slice     |
| 修改元素 | splice、赋值        | map              |
| 排序   | sort、reverse     | 复制一份数组           |
或者直接使用`immer`来解决上述问题

