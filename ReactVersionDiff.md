## Fiber

链表结构
可中断可继续

## Hooks

每次渲染都会执行hooks
根据hooks的执行顺序来判断该进行什么操作

> React 保持对当先渲染中的组件的追踪，每个组件内部都有一个「记忆单元格」列表。它们只不过是我们用来存储一些数据的 JavaScript 对象。当你用 useState() 调用一个Hook的时候，它会读取当前的单元格（或在首次渲染时将其初始化），然后把指针移动到下一个。这就是多个 useState() 调用会得到各自独立的本地 state 的原因。
> 
> 之所以不叫createState，而是叫useState，因为 state 只在组件首次渲染的时候被创建。在下一次重新渲染时，useState 返回给我们当前的 state。


参考链接
[React16源码之React Fiber架构](https://juejin.im/post/5b7016606fb9a0099406f8de)
[完全理解React Fiber](http://www.ayqy.net/blog/dive-into-react-fiber/)
[React Fiber架构](https://zhuanlan.zhihu.com/p/37095662)
[React Fiber](https://juejin.im/post/5ab7b3a2f265da2378403e57)

[React16：Hooks总览，拥抱函数式 (这大概是最全的React Hooks吧)](https://juejin.im/post/5cb5705ee51d456e6e38921d)