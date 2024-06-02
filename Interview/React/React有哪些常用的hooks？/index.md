React Hooks 是在 React 16.8.0 版本中首次引入的。

React v16.8 中引入了 Hooks ，是 React 一种全新的状态管理方式，它提供了一些可以让函数组件拥有类组件同样功能的 API。

其中最常用的 Hook API 包括：

1. [`useState`](https://react.dev/reference/react/useState)：该 Hook 用于在函数组件中添加一个状态管理器。通过 `useState`，可以创建一个状态变量及其更新函数，并在组件内使用该变量来保存和更新组件的状态。
2. [`useEffect`](https://react.dev/reference/react/useEffect)：该 Hook 用于在组件渲染完成后执行一些副作用操作（例如订阅数据、更新 DOM 等）。通过 `useEffect`，可以在组件加载、更新和卸载时设置和清理副作用操作，并且可以在副作用操作之间共享状态。
3. [`useContext`](https://react.dev/reference/react/useContext)：该 Hook 用于在组件之间共享一些全局的状态或函数，以避免通过多层嵌套的 Props 传递进行数据传输。通过 `useContext`，可以让组件在全局状态或函数的上下文中运行，并让它们能够方便地读取或更新全局状态或函数。
4. [`useReducer`](https://react.dev/reference/react/useReducer)：该 Hook 用于在组件中使用一种“状态容器”模式，以避免通过多层 Props 传递或 Context 共享进行状态管理。通过 `useReducer`，可以创建一个状态容器及其更新函数，并在组件内使用该容器来保存和更新组件的状态。
5. [`useMemo`](https://react.dev/reference/react/useMemo)：该 Hook 用于在组件渲染完成后缓存一些计算结果，以避免因为重复计算导致的性能问题。通过 `useMemo`，可以创建一个缓存变量，并在组件内使用该变量来保存计算结果并缓存。
6. [`useCallback`](https://react.dev/reference/react/useCallback)：该 Hook 用于在组件渲染完成后，将一些函数进行缓存，以避免因函数重复创建导致的性能问题。通过 `useCallback`，可以创建一个缓存函数，并在组件内使用该函数来代替重复创建的函数。
7. [`useRef`](https://react.dev/reference/react/useRef)：该 Hook 用于在组件渲染完成后创建一个引用，以便在组件多次渲染时能够保留上一次渲染中的值。通过 `useRef`，可以创建一个引用变量，并在组件内使用该变量来保存一些持久化的数据。
8. [`useImperativeHandle`](https://react.dev/reference/react/useImperativeHandle)：该 Hook 用于在组件中实现一些自定义的 Ref 对象，并且要求将一些组件内部的方法或状态暴露给父组件使用。通过 `useImperativeHandle`，可以创建一个自定义的 Ref 对象，并在组件内指定一些公开的方法或属性。
9. [`useLayoutEffect`](https://react.dev/reference/react/useLayoutEffect)：该 Hook 与 `useEffect` 类似，但它会在浏览器渲染更新之前同步执行副作用操作，以确保 React 组件与浏览器同步更新。通常情况下，应该使用 `useEffect`，但在需要直接操作 DOM 元素或进行测量布局界面时，应当使用 `useLayoutEffect`。
10. [`useDebugValue`](https://react.dev/reference/react/useDebugValue)：该 Hook 可以帮助开发者在调试工具中显示额外的信息，以便更好地理解 Hook 的使用和行为。通常情况下，这个 Hook 只用于调试过程中，而不是实际的应用程序代码中。