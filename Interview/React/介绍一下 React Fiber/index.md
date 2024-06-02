---
tags:
  - React
  - React-Fiber
---
React Fiber 是 React v16 中引入的一种新的协调算法，它被设计用来解决 React 在处理大型应用时可能出现的性能问题。本文将详细介绍 React Fiber 的背景、原理和优势。
# 背景

在 React v15 以及之前版本中，React 应用是通过递归遍历组件树实现的。当组件状态发生变化时，React 会重新计算并渲染整个组件树，然后将变化的部分更新到 DOM 上。这种算法虽然简单易懂，但是也存在一些缺点：

- 当组件树非常庞大时，递归遍历整个组件树的开销很大，导致应用性能下降。
- 如果某个组件在更新过程中发生了阻塞，那么整个组件树的更新也会被阻塞，用户体验不佳。

为了解决这些问题，React 团队在 v16 中引入了一种新的协调算法——React Fiber。

# 设计原理

- React Fiber 的核心思想是将组件树的遍历变成了可中断的异步任务。具体来说，React Fiber 会将整个组件树拆分成多个小的任务单元（Fiber），并按照优先级顺序依次执行这些任务单元。每当执行完一个任务单元时，React Fiber 就会检查当前是否有更高优先级的任务需要执行。如果有，则立即暂停当前任务，并开始执行更高优先级的任务，直到完成后再回来继续执行原来的任务。这样一来，React Fiber 可以让应用更加灵活地响应用户交互和其他事件。
- 在 React Fiber 中，每个任务单元都对应一个 Fiber 对象，该对象包含了当前组件的状态和相关信息。Fiber 对象还存储了组件所在的位置、子组件信息、副作用等信息。当某个任务单元执行时，React Fiber 会利用 Fiber 对象的信息进行 DOM 更新、事件处理等操作。
- React Fiber 还提供了一系列 API，用于控制任务单元的执行顺序、暂停和恢复任务等操作。这些 API 包括 `requestIdleCallback`、`cancelIdleCallback`、`setTimeout`、`setImmediate` 等。
- 为了支持可中断的异步任务，React Fiber 引入了一种新的数据结构——双缓存技术。具体来说，React Fiber 维护了两个 fiber 树：current fiber 树和 work in progress fiber 树。current fiber 树是当前渲染结果对应的 fiber 树，work in progress fiber 树则是正在进行的更新操作对应的 fiber 树。当更新操作完成后，React Fiber 会将 work in progress fiber 树替换为 current fiber 树，从而实现视图更新。
- 最后，React Fiber 的 diff 算法也有所改进。传统的 diff 算法是基于递归遍历的，而 React Fiber 则采用了迭代遍历算法。具体来说，React Fiber 会将更新操作转换成一系列指令（effect），然后将这些指令保存到 effect list 中。最后，React Fiber 会按照顺序执行 effect list 中的指令，从而完成页面渲染。

# 优势

相比于传统的递归遍历算法，React Fiber 具有以下优势：

- 更快的渲染速度：由于 React Fiber 可以将任务切分成小的单位执行，因此可以更加高效地渲染组件。
- 更好的用户体验：由于 React Fiber 可以随时中断和恢复任务，因此可以更加灵活地响应用户交互和其他事件。
- 更加可扩展：React Fiber 提供了一系列 API，使得其可以更加方便地集成进其他系统中。

总结来说，React Fiber 是一种全新的协调算法，它通过分离任务单元、采用双缓存技术、支持可中断的异步任务等方式，解决了 React 在处理大型应用时可能出现的性能问题。

# 相关链接

- [[React Fiber Architecture]]
