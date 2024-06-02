---
tags:
  - React
  - HOC
---
React中常用的高阶组件HOC有很多，以下是一些常见的HOC：

1. `withRouter`：将路由信息注入到组件中，使它们能够访问到路由对象（如`location`、`history`和`match`等）。
2. `connect`：将React组件与Redux Store连接起来，并将State和Dispatch作为Props传递给组件。这使得组件能够直接从Store中读取和操作数据。
3. `memo`：对于纯函数组件，使用`memo`可以缓存组件输出，以提高性能。
4. `withStyles`：用于添加CSS样式到组件中。
5. `redux-thunk`：使Action Creator返回一个函数而不是一个Action对象，从而可以执行异步操作并dispatch新的Action。
6. `recompose`：提供了一组高阶功能，用于增强函数式React组件。例如，`compose`函数可以将多个HOC组合在一起。
7. `react-redux`：提供了一组基于Redux Store的React组件，并简化了React与Redux之间的集成。

总之，React中的HOC提供了许多灵活且有用的功能，可以帮助我们更好地组织和重用代码。开发者可以使用这些HOC来封装通用的逻辑和功能，并使组件更加可复用。