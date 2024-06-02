# Open all links in an HTML document in a new tab

Tags: HTML
URL: https://www.30secondsofcode.org/html/s/open-all-links-in-new-tab/
Source: 30 seconds of code
Created: March 18, 2024 10:35 PM
Last edited time: March 18, 2024 10:53 PM

在新选项卡中打开 HTML 文档中的所有链接

较少使用的 HTML 元素之一，是使用 `<base>` 元素。此元素的用途是指定文档中所有相对 URL 的基本 URL。这意味着，如果文档中有一堆链接，则可以用 `<base>` 元素来指定所有这些链接都应具有基本的 `href` 或 `target` 

利用此元素，我们可以将 `target` 属性设置为 `_blank` 以使文档中的所有链接在新选项卡中打开。只需在 HTML 文档的 `<head>` 中添加一行即可实现此目的。

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_blank">
  </head>
  <body>
    <a href="https://www.example.com">Example</a>
  </body>
</html>
```

<aside>
⚠️ **Warning**
在新选项卡中打开链接存在一些安全风险。请务必阅读有关[保护 `target="_blank"` 链接的提示](https://www.30secondsofcode.org/html/s/target-blank/)，以了解如何保护您的用户免受恶意网站的侵害。

</aside>

---

[<base>：文档根 URL 元素 - HTML（超文本标记语言） | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/base)

HTML 中的 `<base>` 元素指定了一个文档中所有相对URL的根URL。这意味着，当你使用相对路径链接到页面中的其他资源（如样式表、脚本、图片等）时，`<base>` 元素会告诉浏览器如何将这些相对路径转换为完整的URL。
`<base>` 元素是空元素，它只包含属性，没有闭合标签。它通常放置在 `<head>` 元素中，并且在一个文档中只能出现一次。如果存在多个 `<base>` 元素，只有第一个会被使用。
`<base>` 元素有两个主要的属性：

1. `href`：指定了基本的URL，用于解析文档中的相对URL。
2. `target`：指定了所有带有target属性的超链接和表单的默认目标框架或窗口。
下面是一个使用 `<base>` 元素的例子：

```html
<!DOCTYPE html>
<html>
<head>
    <base href="http://www.example.com/pages/" target="_blank">
    <title>示例页面</title>
</head>
<body>
    <img src="images/logo.png" alt="公司Logo">
    <a href="contact.html">联系我们</a>
    <form action="submit.php">
        <!-- 表单内容 -->
    </form>
</body>
</html>
```

在上面的例子中：

- `<base href="http://www.example.com/pages/">` 告诉浏览器所有相对URL都相对于 `http://www.example.com/pages/`。
- 因此，`<img src="images/logo.png">` 实际上会从 `http://www.example.com/pages/images/logo.png` 加载图片。
- `<a href="contact.html">` 链接实际上会指向 `http://www.example.com/pages/contact.html`。
- `<form action="submit.php">` 表单数据将会被提交到 `http://www.example.com/pages/submit.php`。
- `target="_blank"` 属性使得所有超链接在新的浏览器窗口或标签页中打开。
需要注意的是，`<base>` 元素不会影响绝对URL。只有相对URL会受到 `<base>` 元素的影响。
其实就是算是绝对URL，如果没有指定 `target` ，那么还是会受到 `<base>` 元素的影响。