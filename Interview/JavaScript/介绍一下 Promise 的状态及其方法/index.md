Promise是一种用于异步编程的技术，它将异步操作转换成类似于同步操作的代码形式，提供了一种更加优雅和可读性强的方式来处理异步任务。

在JavaScript中，Promise对象包含**三种状态**：**Pending**（进行中）、**Fulfilled**（已成功）和**Rejected**（已失败）。

> Promise的方法如下：

1. Promise对象可以通过 **then**() 方法添加成功（Fulfilled）和失败（Rejected）时的回调函数。then() 方法可以链式调用，每次返回一个新的 Promise 对象，因此可以很容易地实现异步任务的连续执行。
2. Promise对象还提供了 **catch**() 方法用于捕获错误和 finally() 方法用于在 Promise 被解析后运行代码块。
3. Promise.**all**() 方法接收一个 Promise 数组作为参数，返回一个新的 Promise，只有当所有 Promise 都解析成功时才会被解析，否则该 Promise 会被拒绝。
4. Promise.**race**() 方法接收一个 Promise 数组作为参数，返回一个新的 Promise，只要有一个 Promise 被解析或拒绝就会被解析或拒绝。
5. Promise.**resolve**() 和 Promise.**reject**() 方法分别返回一个已解析和一个已拒绝的 Promise 对象，可以用于快速创建 Promise。