---
tags:
  - HTML
  - DOM加载时间线
---
# [渡一](https://ke.qq.com/course/231577/1731614849861785#term_id=100273169)
1. 创建Document对象，开始解析web页面。这个阶段 `document.readyState = 'loading'`.
2. 遇到 `link` 外部 css，创建线程，进行异步加载，并继续解析文档。
3. 遇到 `script` 外部 js，并且没有设置 `async`、`defer`，浏览器同步加载，并阻塞，等待 js 加载完成并执行该脚本，然后继续解析文档。
4. 遇到 `script` 外部 js，并且设置有 `async`、`defer`，浏览器创建线程异步加载，并继续解析文档。（异步禁止使用 `document.write()`）
5. 遇到 `img` 等（带有 `src`），先正常解析 dom 结构，然后浏览器异步加载 src，并继续解析文档。看到标签直接生产 dom 树，不用等着 img 加载完 src。
6. 当文档解析完成（`domTree` 建立完毕，不是加载完毕，解析在加载之前），`document.readyState = 'interactive'`。
7. 文档解析完成后，所有设置有 `defer` 的脚本会按照顺序执行。（注意与 `async` 的不同,但同样禁止使用 `document.write()`）;
8. 文档解析完成后，document 对象触发 `DOMContentLoaded` 事件，这也标志着程序执行从同步脚本执行阶段，转化为事件驱动阶段。
9. 当所有 `async` 的脚本加载完成并执行后、`img` 等加载完成后（页面所有的都执行加载完之后），`document.readyState = 'complete'`，`window` 对象触发 `load` 事件。
10. 从此，以异步响应方式处理用户输入、网络事件等。

# [智谱清言](https://chatglm.cn/)
DOM 加载时间线：
HTML
1. **开始解析HTML文档**：
   - 浏览器开始从网络或缓存中获取HTML文档，并解析HTML，构建DOM树。
   - 文档状态为`loading`。
2. **遇到同步脚本**：
   - 如果HTML文档中遇到没有`async`或`defer`属性的`<script>`标签，浏览器会暂停HTML解析，加载并执行脚本。
   - 文档状态仍为`loading`。
3. **遇到异步脚本（async）**：
   - 如果HTML文档中遇到带有`async`属性的`<script>`标签，浏览器会异步加载脚本，不会阻塞HTML解析。
   - 文档状态仍为`loading`。
   - 脚本加载完成后立即执行，可能在`DOMContentLoaded`事件之前或之后执行。
4. **遇到延迟脚本（defer）**：
   - 如果HTML文档中遇到带有`defer`属性的`<script>`标签，浏览器会异步加载脚本，不会阻塞HTML解析。
   - 文档状态仍为`loading`。
   - 脚本异步加载后，脚本的执行会被推迟到HTML解析完成之后，DOMContentLoaded事件触发之前。
1. **加载样式表和异步/延迟脚本**：
   - 浏览器继续加载内联和外部样式表，以及异步和延迟脚本。
   - 文档状态仍为`loading`。
2. **HTML解析完成**：
   - 一旦HTML文档解析完成，浏览器会准备触发`DOMContentLoaded`事件。
   - 文档状态从`loading`变为`interactive`。
3. **执行延迟脚本**：
   - 在`DOMContentLoaded`事件触发之前，按照它们在文档中的出现顺序执行所有延迟脚本。
   - 文档状态仍为`interactive`。
4. **触发DOMContentLoaded事件**：
   - 当HTML文档被完全加载和解析完成，并且所有延迟脚本执行完毕后，浏览器会触发`DOMContentLoaded`事件。
   - 文档状态仍为`interactive`。
5. **加载图片等外部资源**：
   - 在`DOMContentLoaded`之后，浏览器继续加载图片、视频等外部资源。
   - 文档状态仍为`interactive`。
6. **触发`window.onload`事件**：
    - 当所有的DOM、样式表、脚本、图片等资源都完全加载完成后，浏览器会触发`window`对象的`load`事件。
    - 文档状态从`interactive`变为`complete`。
7. **交互**：
    - 用户可以与页面进行交互，事件处理程序可以响应交互。
    - 文档状态仍为`complete`。
8. **卸载（Unload）**：
    - 当用户离开页面时，如点击链接或关闭浏览器窗口，页面将卸载。
    - 文档状态可能会变为`unloading`，但这不是一个正式的文档状态，而是一个过程中的状态。
在整个加载时间线中，可以通过`document.readyState`属性来检查文档的状态。这个属性可以返回以下三个值：
- `loading`：文档正在加载。
- `interactive`：文档已加载，文档与用户可以开始交互。
- `complete`：文档和所有子资源都已加载完成。
了解这个详细的时间线对于前端开发人员来说非常重要，因为它帮助他们理解代码的执行时机，从而优化页面性能，确保良好的用户体验。


> [!NOTE] 阻塞
> 普通的 `<script>` 同步脚本的加载和执行都会阻塞 HTML 解析和页面渲染
> 
> 异步的 `<script async>` 和 `<script defer>` 的加载不会阻塞 HTML 解析和页面渲染，但是执行有可能会阻塞HTML解析和页面渲染，如果 async 脚本在执行的时候，HTML 未完成解析，那么它就会阻塞 HTML 解析和页面渲染

[ ] 延迟脚本执行的时候，document.readyState = "interactive" 吗，为什么
