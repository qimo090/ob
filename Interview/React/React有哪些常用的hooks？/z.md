React 提供了一系列内置的 Hooks，这些 Hooks 可以让你在不编写类的情况下使用 React 的特性。以下是一些常用的 React Hooks：
1. `useState`：允许你在函数组件中添加 state。
```jsx
const [state, setState] = useState(initialState);
```
2. `useEffect`：在函数组件中执行副作用操作，类似于类组件中的 `componentDidMount`，`componentDidUpdate` 和 `componentWillUnmount` 的组合。
```jsx
useEffect(() => {
  // 执行副作用操作
  return () => {
    // 清理副作用
  };
}, [dependencies]);
```
3. `useContext`：让你能够使用 React 的 Context 功能来访问父组件提供的数据，而不必通过 props 层层传递。
```jsx
const value = useContext(MyContext);
```
4. `useReducer`：提供了一个替代 `useState` 的方案，适用于 state 逻辑较复杂且包含多个子值，或者下一个 state 依赖于前一个 state 的情况。
```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```
5. `useCallback`：返回一个 memoized 回调函数，只有在依赖项改变时才会更新。
```jsx
const memoizedCallback = useCallback(
  () => {
    // 回调函数
  },
  [dependencies]
);
```
6. `useMemo`：返回一个 memoized 值，只有在依赖项改变时才会重新计算。
```jsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```
7. `useRef`：返回一个可变的 ref 对象，其 `.current` 属性被初始化为传入的参数（initialValue）。返回的 ref 对象在组件的整个生命周期内保持不变。
```jsx
const refContainer = useRef(initialValue);
```
8. `useImperativeHandle`：在使用 ref 时自定义暴露给父组件的实例值。
```jsx
useImperativeHandle(ref, () => ({ focus }), [focus]);
```
9. `useLayoutEffect`：其函数签名与 `useEffect` 相同，但它会在所有的 DOM 变更之后同步调用 effect。可以使用它来读取 DOM 布局并同步触发重渲染。
```jsx
useLayoutEffect(() => {
  // 执行同步的副作用操作
  return () => {
    // 清理副作用
  };
}, [dependencies]);
```
10. `useDebugValue`：用于在 React 开发者工具中显示自定义 Hook 的标签。
```jsx
useDebugValue(value);
```
这些 Hooks 为你在函数组件中实现类组件的功能提供了强大的工具。每个 Hook 都有其特定的用途，合理使用这些 Hooks 可以使你的组件更加简洁和可维护。
