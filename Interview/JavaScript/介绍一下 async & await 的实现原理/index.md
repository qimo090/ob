在 JavaScript 引擎中，async/await 函数的实现原理是**基于 Promise 对象**和**生成器函数**（Generator Function）的协作。

- 具体来说，async/await 函数内部会将其代码块转换为一个状态机，并使用生成器函数返回的迭代器来进行状态的管理和切换，从而实现异步的调用和处理。
- 当 async 函数被调用时，它会立即返回一个 Promise 对象，并且开始执行其中的代码。当遇到 await 表达式时，async 函数会暂停执行并将控制权转交给生成器函数返回的迭代器对象，该对象会执行一个 next() 方法来将获取到的 Promise 对象进一步传递。
- 在等待的过程中，async 函数会依次执行其代码块中下一个 await 表达式之前的所有同步操作。当等待的 Promise 对象状态变为 resolved 时，async 函数会再次被调用并继续执行，直到代码块执行结束或者抛出异常。
---
 ~~需要注意的是，async/await 函数的实现原理并不是原生的 JavaScript 语法规范所支持的，而是通过编译工具（如 Babel 等）将其代码转换为符合 JavaScript 语法规范的代码实现。~~

上述这句话不完全正确。`async` 和 `await` 是 JavaScript 的原生语法，它们是在 ES2017（ECMAScript 2017）规范中引入的，而不需要通过编译工具转换。现代 JavaScript 引擎已经原生支持 `async` 和 `await`，因此你可以直接在支持 ES2017 的环境中使用它们。
然而，对于那些不支持 ES2017 及以上版本的旧浏览器或环境，你需要使用像 Babel 这样的编译工具将使用了 `async` 和 `await` 的现代 JavaScript 代码转换为旧版本 JavaScript 代码，这样就可以在不支持这些新特性的环境中运行了。这个转换过程通常涉及到将 `async` 函数转换为生成器函数（`function*`），并将 `await` 表达式转换为 `yield` 表达式，以及添加额外的 Promise 包装代码来模拟 `async` 和 `await` 的行为。
总结来说，`async` 和 `await` 是 JavaScript 的原生语法，但在不支持这些特性的环境中，你可能需要使用编译工具来转换代码。
