---
tags:
  - 资源提示符
  - HTML
---
# 常用的资源提示符
+ [async](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/script#async)
+ [defer](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/script#defer)
+ [preload](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Attributes/rel/preload)
+ [prefetch](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Attributes/rel/prefetch)
# async & defer
[[async & defer]]

`async`和`defer`是`<script>`标签的两种属性，它们用于控制外部脚本的加载和执行方式，以避免阻塞页面渲染。它们的区别主要在于脚本加载和执行的时间点以及执行顺序。
1. **异步加载（async）**：
   - `async`属性告诉浏览器，脚本应该在页面加载的任何时候异步下载，但不会等待脚本下载和执行，也不会影响页面的渲染。
   - 当脚本下载完成后，浏览器会中断渲染，执行该脚本。由于执行是异步的，所以脚本可能会在DOMContentLoaded事件之前或之后执行，也有可能页面已经渲染完毕后执行，执行时机是不确定的。
   - `async`脚本之间不会有执行顺序，它们将按照它们在HTML中出现的顺序进行加载和执行，但浏览器可能会根据当前的渲染状况和网络状况来决定执行的顺序。
2. **延迟执行（defer）**：
   - `defer`属性告诉浏览器，脚本应该在文档解析完成后延迟执行，但在DOMContentLoaded事件之前执行。
   - 设置`defer`的脚本不会阻塞页面的初始渲染，但在DOMContentLoaded事件触发前，它们会被加载并按顺序执行。
   - 如果多个`<script>`标签都设置了`defer`，那么它们将按照在HTML中出现的顺序执行。
3. **示例**：
   - `async`的用法：
     ```html
     <script src="script.js" async></script>
     ```
   - `defer`的用法：
     ```html
     <script src="script.js" defer></script>
     ```
4. **总结**：
   - `async`用于无需等待即可执行的脚本，适合用于非渲染阻塞的脚本，如统计脚本或第三方库。
   - `defer`用于需要在DOM加载完成后执行的脚本，确保脚本按照顺序执行，适合用于需要在页面加载后但DOMContentLoaded之前执行的脚本。
在实际应用中，选择使用`async`还是`defer`属性，应根据具体需求来决定。如果脚本的执行对页面加载至关重要，且需要按照特定的顺序执行，则应该使用`defer`。如果脚本执行不影响页面渲染，且需要在页面加载完成后尽快执行，则使用`async`更为合适。在复杂的应用中，可能需要同时使用这两个属性，以确保关键脚本的顺序执行和优化页面加载性能。
# preload & prefetch
[[preload & prefetch]]

preload 和 prefetch 是HTML中用于资源优化的两个不同的属性，它们都用于`<link>`标签，目的是为了提高网页加载速度和性能。它们的主要区别在于加载资源和处理这些资源的方式。
1. **加载时机和行为**：
   - `preload`：它是一种声明式的加载，告诉浏览器页面立即需要的资源，并强制浏览器在不阻塞`document`的`onload`事件的情况下开始加载这些资源。这意味着浏览器会立即开始获取这些资源，但它们可能不会立即执行，例如下载的JavaScript脚本。`preload`可以指定资源的类型，如`as="style"`或`as="script"`，这有助于浏览器确定资源的优先级。
   - `prefetch`：它是一种提示浏览器在空闲时候下载可能需要的资源。这并不是强制性的，浏览器可能会根据其策略和网络状况决定是否加载这些资源。`prefetch`同样可以指定资源的类型，但其优先级比`preload`低。
2. **资源优先级**：
   - 使用`preload`时，资源被赋予最高的优先级，意味着浏览器会尽可能早地下载这些资源。
   - 使用`prefetch`时，资源被赋予较低的优先级，浏览器可能会在完成当前任务和网络空闲时才下载。
3. **使用场景**：
   - `preload`通常用于那些页面加载后立即需要的资源，比如JavaScript脚本或样式表，以确保它们能够快速可用，而不影响页面的初始渲染。
   - `prefetch`则用于那些未来可能在页面中使用的资源，比如用户即将访问的页面的资源。在单页面应用（SPA）或服务器端渲染（SSR）的页面中，这非常有用，可以预先加载下一个路由可能需要的资源。
4. **示例**：
   - `preload`的用法：
     ```html
     <link rel="preload" href="main.js" as="script">
     ```
   - `prefetch`的用法：
     ```html
     <link rel="prefetch" href="nextpage.js">
     ```
5. **兼容性和测试**：
   - 虽然这两个属性被广泛支持，但最好通过网络性能测试工具来验证它们的行为，因为实际效果可能会根据不同的浏览器和网络条件有所不同。
综上所述，`preload`和`prefetch`都是用来提升页面加载速度和用户体验的，它们通过不同的方式指示浏览器如何以及何时加载资源。选择使用哪一个属性取决于资源是否真的需要立即加载，以及是否希望浏览器在空闲时预先下载资源。