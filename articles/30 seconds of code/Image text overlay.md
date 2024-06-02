# Image text overlay

Tags: CSS, Visual
URL: https://www.30secondsofcode.org/css/s/text-backdrop-overlay
Source: 30 seconds of code
Created: July 8, 2023 9:48 AM
Last edited time: July 8, 2023 9:48 AM

Displays a text on top of an image using an overlay.

- Use `backdrop-filter` to apply a `blur(14px)` and `brightness(80%)` effect. This makes text readable regardless of background image and color.

```html
<div>
  <h3 class="text-overlay">Hello, World</h3>
  <img src="<https://picsum.photos/id/1050/1200/800>" />
</div>
```

```css
div {
  position: relative;
}

.text-overlay {
  position: absolute;
  top: 0;
  left: 0;
  padding: 1rem;
  font-size: 2rem;
  font-weight: 300;
  color: white;
  backdrop-filter: blur(14px) brightness(80%);
}
```

[https://codepen.io/grimm110-the-lessful/pen/QWVjWrx](https://codepen.io/grimm110-the-lessful/pen/QWVjWrx)