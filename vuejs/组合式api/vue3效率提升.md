客户端渲染效率比vue2提升了1.3~2倍
SSR效率提升2~3倍

静态提升：
- 原理：通过将静态元素、属性提出render函数，使得这些节点只需要被创建一次
- 提出静态元素，使静态节点只被渲染一次
- 提出静态属性

预字符串化：
- 将大量静态节点整合为字符串，使得渲染节点数量大大减少
- 当编译器遇到大量连续静态元素，会将其编译为一个普通字符串节点

缓存事件处理函数：
- 对事件处理函数进行缓存
- 保证事件处理函数只生成一次

block tree：
- vue3会标记动态节点，在根节点中记录，循环遍历记录，寻找动态节点比较，跳过树的遍历

patchflag：
- 根据节点信息记录动态信息，后续只根据记录比对相关信息