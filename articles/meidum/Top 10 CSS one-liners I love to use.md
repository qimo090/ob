---
created: 2024-07-25T23:10
updated: 2024-07-26T23:23
tags:
  - CSS
url: https://levelup.gitconnected.com/top-10-css-one-liners-i-love-to-use-5825a5c91d04
---
> 我最喜欢使用的 10 大 CSS 单行代码

# 1. Aspect Ratio

https://developer.mozilla.org/zh-CN/docs/Web/CSS/aspect-ratio

第一句定义了元素的长宽比。这样就可以轻松地根据定义的宽度自动调整高度（反之亦然）。

```css file:aspect-radio
.box {
  width: 90%;
  aspect-ratio: 16/9;
}
```

# 2. Logical Properties

```css file:margin
.box {  
  margin-block: 5px 10px; /* 5px top margin, 10px bottom margin */  
  margin-inline: 20px 30px; /* 20px left margin, 30px right margin */  
}
```

```css file:padding
.box {  
  padding-block: 10px 20px; /* 10px top/bottom padding, 20px bottom padding */  
  padding-inline: 15px 25px; /* 15px left padding, 25px right padding */  
}
```

这些属性会根据文本方向（例如从左到右或从右到左）自动调整，从而使您的代码更易读、更简短、更灵活且更适合国际。

```css file:RTL
.element {
	margin-inline: 10px 15px; /* 在 RTL 模式下，10px 是右边距，15px 是左边距 */ 
	padding-inline: 5px 10px; /* 在 RTL 模式下，5px 是右内边距，10px 是左内边距 */ 
}
```

# 3. Universal box sizing

```css file:border-box
*, *::before, *::after {  
	box-sizing: border-box;  
}
```

# 4. Smooth Scroll

```css file:scroll-behavior
html {  
	scroll-behavior: smooth;  
}
```

# 5. Vertical Writing Mode

```css file:writing-mode
.vertical-text {  
	writing-mode: vertical-rl;  
}
```

# 6. Truncating Text with Ellipsis

溢出省略打点

```css
.ellipsis {  
	white-space: nowrap;  
	overflow: hidden;  
	text-overflow: ellipsis;  
}
```

# 7. Place-items

```css file:place-items
.box {  
	display: grid;  
	place-items: center;  
}
```

# 8. Limit the width of text within the content

`ch` 单位是一个相对长度单位，它的值等于元素中字体的 “0” 字符的宽度。这个单位非常适合用来创建与字体宽度相关的布局或间距。

## 基本概念

- 1 `ch` = 当前元素字体中的 “0” 字符的宽度。
- 因为它是基于字体的宽度，所以 `ch` 单位会根据字体的变化而变化。

## 使用场景

- **文本输入框宽度**：使输入框宽度与字符数相关联。
- **固定宽度布局**：创建与字体宽度成比例的布局元素。
- **间距和内边距**：根据字体的宽度设置元素的外边距和内边距。

```css
p {  
	max-width: 100ch;  
}
```

## 优势

- **与字体一致**：`ch` 单位使得元素宽度、内边距和外边距与字体宽度相匹配，这在设计与文本相关的布局时非常有用。
- **响应性**：在不同字体和字体大小下，`ch` 单位可以自动调整，从而保持一致的视觉效果。

## 注意事项

- **字体依赖性**：由于 `ch` 单位是基于当前字体的 "0" 字符的宽度，因此不同的字体和字体大小会导致 `ch` 单位的实际像素值不同。
- **浏览器兼容性**：现代浏览器普遍支持 `ch` 单位，但在使用之前，仍然建议测试目标浏览器的兼容性。

### 总结

`ch` 单位是一个强大的工具，适用于根据字体宽度进行布局和设计。在创建需要与字符数成比例的输入框、间距或其他布局元素时，使用 `ch` 单位可以带来更一致和响应良好的用户体验。

# 9. Styling Placeholder Text

https://developer.mozilla.org/zh-CN/docs/Web/CSS/::placeholder

```css file:placeholder
::placeholder {  
	color: #999;  
	font-style: italic;  
}
```

# 10. Accent color

https://developer.mozilla.org/zh-CN/docs/Web/CSS/accent-color

```css
body {  
	accent-color: green;  
}
```
