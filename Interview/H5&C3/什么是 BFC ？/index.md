---
tags:
  - CSS
  - BFC
---
BFC（Block Formatting Context）是 CSS 中一个很重要的概念。它是指一个块级容器，其中的元素按照特定规则布局和渲染，同时也影响着其内部和外部元素的布局。

BFC 特点：

1. BFC 内部的元素会按照垂直方向一个接一个地排列，并且在水平方向上占据整个父容器的宽度。
2. BFC 内部元素的 margin 和 padding 不会与外部元素共享边框，而是互相独立，不会发生重叠。
3. 如果两个相邻的块级元素都属于同一个 BFC，那么它们之间的 margin 会产生折叠，即取两个 margin 的最大值作为最终的 margin 值。
4. BFC 可以包含浮动元素，并防止浮动元素溢出到容器外面。
5. BFC 内部的第一个子元素或最后一个子元素，可以通过设置 clear 属性来清除浮动。

如何创建BFC？

1. 使用 float 属性：给元素添加 float 属性可以使其成为一个 BFC。
2. 使用 position 属性：将元素使用 position 属性设置为 absolute 或 fixed 时，也可以使其成为一个 BFC。
3. 使用 display 属性：给元素添加 display 属性设置为 inline-block、table-cell、table-caption 等值，也可以变成 BFC。
4. 设置 overflow 属性：将元素的 overflow 属性设置为 auto、scroll 或 hidden，也可以创建一个 BFC。

应用场景：

1. 清除浮动：当一个父容器包含多个浮动元素时，可以将其设置为 BFC，防止浮动元素溢出到外面。
2. 解决 margin 重叠问题：当两个元素的 margin 发生重叠时，可以将其中之一包裹在一个 BFC 中，使其 margin 与外部元素分离。
3. 实现多列布局：使用 column-count 和 column-gap 属性可以让文本内容自动分为多列，但这需要在 BFC 中实现。

总结

BFC 是 CSS 中的一个重要概念，它对于页面布局及解决一些常见问题非常有帮助。了解 BFC 的概念、特点和创建方式，能够更好地掌握其应用场景，提高开发效率和代码质量。