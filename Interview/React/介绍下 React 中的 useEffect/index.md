- 在 React 中，`useEffect` 是一个用于处理副作用的 Hook。
- ’副作用是指在组件生命周期中的某些特定时刻需要执行的操作，例如数据获取、订阅事件、手动操作 DOM 等。
- `useEffect` 的作用就是在组件渲染完成后执行这些副作用操作。

**`useEffect` 接收两个参数：一个副作用函数和一个依赖数组。**

副作用函数是一个函数，它会在组件渲染之后执行。它可以包含任何副作用操作，如订阅、网络请求、DOM 操作等。示例代码如下：

```jsx
import { useEffect } from 'react';

function MyComponent() {
  useEffect(() => {
    // 执行副作用操作
    console.log('Component rendered');

    // 清理副作用
    return () => {
      console.log('Component unmounted');
    };
  }, []);

  return <div>My Component</div>;
}
```

在上述示例中，我们定义了一个 `MyComponent` 组件，并在其中使用了 `useEffect`。在副作用函数中，我们打印了一条消息来表示组件已经渲染完成。此外，我们还提供了一个返回函数，用于清理副作用。该函数将在组件卸载之前执行，以便做一些清理工作，如取消订阅或清除定时器。

第二个参数是一个依赖数组，用于指定副作用函数的依赖项。当依赖项发生变化时，副作用函数将重新执行。如果依赖数组为空，副作用函数只会在组件首次渲染时执行，并在组件卸载时执行清理操作。示例代码如下：

```jsx
import { useEffect, useState } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log(`Count changed: ${count}`);
  }, [count]);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <p>Count: {count}</p>
    </div>
  );
}
```

在上述示例中，我们定义了一个 `MyComponent` 组件，并使用 `useState` 来保存一个计数器 `count`。在 `useEffect` 中，我们传入了 `count` 作为依赖项，这意味着只有当 `count` 发生变化时，副作用函数才会被触发。每次点击增加按钮时，`count` 都会发生变化，`useEffect` 会记录这个变化并打印相应的消息。

通过使用 `useEffect`，我们可以在 React 组件中处理各种副作用操作，并且可以在需要时进行清理。这使得我们能够更好地管理组件的生命周期和状态。