## useState

## useEffect

## useContext

React16中更新了Context API，Context主要用于爷孙组件的传值问题，新的Context API使用订阅发布者模式方式实现在爷孙组件中传值。

useContext Hook接收一个 context 对象（React.createContext 的返回值）并返回该 context 的当前值。当前的 context 值由上层组件中距离当前组件最近的 <MyContext.Provider> 的 value prop 决定。

## useReducer

## useCallback

useCallback可以认为是对依赖项的监听，把接受一个回调函数和依赖项数组，返回一个该回调函数的memoized(记忆)版本，该回调函数仅在某个依赖项改变时才会更新。

## useMemo

useMemo和useCallback很像，唯一不同的就是

> useCallback(fn, deps) 相当于 useMemo(() => fn, deps

## useRef

useRef返回一个可变的ref对象，useRef接受一个参数绑定在返回的ref对象的current属性上，返回的ref对象在整个生命周期中保持不变。

然而，useRef() 比 ref 属性更有用。它可以很方便地保存任何可变值，其类似于在 class 中使用实例字段的方式。

请记住，当 ref 对象内容发生变化时，useRef 并不会通知你。变更 .current 属性不会引发组件重新渲染。如果想要在 React 绑定或解绑 DOM 节点的 ref 时运行某些代码，则需要使用回调 ref 来实现。

### 等等....