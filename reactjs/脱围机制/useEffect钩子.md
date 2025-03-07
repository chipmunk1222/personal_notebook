# 什么是Effect
`Effect`即副作用，指的是一些涉及组件外部的行为逻辑，包括定时器，异步函数等

`Effect`使用`useEffect`钩子触发，其特点是在组件每次渲染时触发一次内部的功能逻辑，并且可以返回一个函数，设置对副作用的清理

编写`Effect`按照以下几步进行
1. 声明`Effect`
2. 指定`Effect`依赖
3. 必要时添加依赖清理函数

## 声明Effect
使用`useEffect`钩子触发`Effect`
```js
import { useEffect } from 'react';
function MyComponent() {  
	useEffect(() => {  
	// 每次渲染后都会执行此处的代码  
	});  
	return <div />;  
}
```
在这个例子中，每次`MyComponent`组件的重新渲染都会导致`Effect`里的副作用被重复执行
## Effect的触发时机
虽说`useEffect`钩子里的逻辑是随着组件渲染而触发的，但具体到底在什么时机呢？

实际上，`Effect`副作用更准确的触发时机应该是组件每次渲染完后，接着`React`将运行`Effect`执行其中逻辑

在下列例子中，每次点击按钮（首次渲染）会刷新`State`中的`isPlaying`状态，从而触发`Effect`改变`ref`绑定元素的状态
>这里还有一个要点，如果在`Effect`中改变`State`状态会导致两者无限循环，值得引起注意
```js
import {
    useState,
    useRef,
    useEffect
}
from 'react';

function VideoPlayer({
    src,
    isPlaying
}) {
    const ref = useRef(null);

    useEffect(() = >{
        if (isPlaying) {
            ref.current.play();
        } else {
            ref.current.pause();
        }
    });

    return < video ref = {
        ref
    }
    src = {
        src
    }
    loop playsInline / >;
}

export default
    function App() {
        const[isPlaying, setIsPlaying] = useState(false);
        return ( < ><button onClick = { () = >setIsPlaying(!isPlaying)
        } > {
            isPlaying ? '暂停': '播放'
        } < /button>
      <VideoPlayer
        isPlaying={isPlaying}
        src="https:/ / interactive - examples.mdn.mozilla.net / media / cc0 - videos / flower.mp4 "
      />
    </>
  );
}
"
```
# 指定Effect依赖
如果每次组件重新渲染都会导致`Effect`中的副作用被反复运行，有时会造成逻辑混乱以及资源浪费，因此可以添加`Effect`的依赖以避免这个情况

对于`Effect`的依赖分三种情况
1. 任何情况下重新运行
2. 只在初次渲染时运行
3. 指定触发项
分别对应下列情况：
```js
useEffect(() = >{
    // 这里的代码会在每次渲染后运行
});

useEffect(() = >{
    // 这里的代码只会在组件挂载（首次出现）时运行
},
[]);

useEffect(() = >{
    // 这里的代码不但会在组件挂载时运行，而且当 a 或 b 的值自上次渲染后发生变化后也会运行
},
[a, b]);
```
>总的来说，`useEffect`的作用就是同步一些东西，怎么同步，看挂载、更新、卸载时的状态

## 添加副作用清理函数cleanup
一些副作用会带有延时的情况，如果不清理这类涉及外部的副作用可能会导致其不断累积，从而严重影响资源利用
比如下列情况：
```js
  useEffect(() => {
    const connection = createConnection();
    connection.connect();
  }, []);
```
当用户退出某个导航时组件被卸载但连接并未销毁，当下次再进入该导航，连接会不断累积

于是，`Effect`提供一个清理函数来应对这种情况，即下例返回函数
```js
useEffect(() = >{
    const connection = createConnection();
    connection.connect();
    return () = >{
        connection.disconnect();
    };
},
[]);
```
以上例子将保证组件卸载时连接中断，从而避免副作用的累积
>除了处理副作用的问题，还可以用清理函数设置某些值变回初始值以及打印日志等（完全可以将其使用场景与`onMounted`和`watch`类比）

# 使用useMemo优化性能
`useEffect`在组件每次重新渲染时都会重新触发其中的副作用，然而，如果我们并不需要处理一些需要清理副作用的行为，此时，可以使用`useMemo`替代`useEffect`

`useMemo`是一个缓存钩子，它具有和`useEffect`类似的结构，不同的是，`useMemo`返回的是基于参数的缓存，如果参数并未发生改变，则组件重新渲染时不会触发`useMemo`的更新，从而优化性能

如以下例子：
```js
import {
    useMemo,
    useState
}
from 'react';

function TodoList({
    todos,
    filter
}) {
    const[newTodo, setNewTodo] = useState('');
    const visibleTodos = useMemo(() = >{
        // ✅ 除非 todos 或 filter 发生变化，否则不会重新执行
        return getFilteredTodos(todos, filter);
    },
    [todos, filter]);
    // ...
}
```