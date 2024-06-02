React Hooks 是 React 16.8 引入的新特性，允许你在不编写类的情况下使用 state 以及其他的 React 特性。Hooks 的设计目的在于让你能够在函数组件中“钩入”React state 及生命周期等特性。
React Hooks 依赖于组件渲染时的调用顺序来确保 state 和其他状态的正确性。当你在组件中多次渲染时，Hooks 必须按照相同的顺序被调用，这样才能保证每次渲染都能获取到正确的状态。
如果将 Hook 放到条件语句中，那么在组件的多次渲染之间，该 Hook 可能会被跳过或者多次执行，导致调用顺序发生变化。这样就会导致状态错乱，出现难以预料和调试的问题。
例如，下面的代码是错误的：
```jsx
if (someCondition) {
  const [state, setState] = useState(0);
}
```
在上面的代码中，`useState` 的调用取决于 `someCondition` 的值。如果 `someCondition` 在组件的不同渲染间改变，那么 `useState` 的调用可能会被跳过，或者在不同的渲染中调用不同的 `useState` 实例，这会导致状态的不一致。
因此，为了保证 Hooks 的正确性，React 强制规定 Hooks 必须在组件的最顶层使用，或者在自定义 Hooks 中使用，这样可以确保 Hooks 的调用顺序在每次渲染时都是相同的。
