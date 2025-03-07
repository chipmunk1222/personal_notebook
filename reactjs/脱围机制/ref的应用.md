# ref引用
通过`state`绑定的状态在其改变时，会触发相应组件的重新渲染，使用`ref`绑定的组件不会重新渲染
## ref的使用
`ref`同样是`react`提供的一个钩子
```js
import {useRef} from 'react'

const ref = useRef(0)
```
`ref`内部结构为一个对象，它是以这种方式保存状态的
```js
{
current: 0
}
```
>通过`ref`绑定的状态被寄存在`current`属性名中，当然，寄存的对象可以是任意格式
>对比`ref`与`state`，由于`ref`用于表示一种“非刷新式”状态，所以被称作一种"脱围机制"，要注意其只能被用于不会刷新组件的状态存储

## 用ref操作dom
已知`ref`可以绑定任意元素，那么理所应当，`ref`也能绑定`DOM`元素，于是，通过绑定`DOM`我们就能直接操作`DOM`元素本身
```js
import {useRef} from 'react'

const ref = useRef(null)

<div ref={ref}>
```
基于以上特性，我们能够直接操纵这个`DOM`元素，包括浏览器`api`等，除此之外，如果绑定的是自定义组件，也可以直接调用组件方法等
```js
ref.current.focus()
ref.current.scrollIntoView()
```
如上述方法，第一个使`input`获得焦点，第二个使`inline`元素滚动至视口中间

