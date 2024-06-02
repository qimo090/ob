- **官方说法**：闭包就是指有权访问另一个函数作用域中的变量的函数。
- **[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures) 说法**：闭包是一种特殊的对象。它由两部分构成：函数，以及创建该函数的环境。环境由闭包创建时在作用域中的任何局部变量组成。
- **深度回答**：浏览器在加载页面会把代码放在栈内存（ ECStack ）中执行，函数进栈执行会产生一个私有上下文（ EC ），此上下文能保护里面的使用变量（ AO ）不受外界干扰，并且如果当前执行上下文中的某些内容，被上下文以外的内容占用，当前上下文不会出栈释放，这样可以保存里面的变量和变量值，所以我认为闭包是一种保存和保护内部私有变量的机制。

# 技术详解
闭包是 JavaScript 中一种常见的编程概念，它允许函数访问其定义时的作用域外部变量。在实际开发中，我们会经常使用到闭包来封装一些变量或函数，以保证其不被外界直接访问和修改。本文将对闭包的概念、特点以及使用场景进行详细介绍。
## 概念
闭包指的是函数与其创建时所处的词法环境（lexical environment）的组合。简单地说，闭包就是能够读取其他函数内部变量的函数。这个特性是由 JavaScript 的词法作用域实现的，因为函数在创建时会保存其所处的词法环境。

 ### 特点
1. **可以访问父级作用域中的变量**：在函数内部通过闭包可以访问并修改父级作用域的变量，而且这些变量在函数执行完毕后依然存在。
2. **可以将变量私有化**：使用闭包可以将某些变量私有化，避免全局变量污染和变量冲突问题，同时也增加了代码的可维护性。
3. **可以实现模块化**：使用闭包可以将一些相关方法或属性封装在一个作用域内，形成一个独立的模块，从而提高代码的复用性和可读性。

### 使用场景  

闭包在 JavaScript 中有广泛的应用场景，以下是几种常见的使用场景：

1. **私有变量和方法**：使用闭包可以将某些变量或方法私有化，在外界无法直接访问或修改，从而保证数据的安全性。
```js
function createCounter() {
  let count = 0;
  return function() {
    count++;
    console.log(count);
  };
}

const counter = createCounter();
counter(); // 1
counter(); // 2
```

2. **延迟执行**：使用闭包可以实现定时器的延迟执行，从而避免了异步回调带来的代码逻辑混乱问题。
```js
function delay(func, time) {
  return function() {
    setTimeout(func, time);
  };
}

const sayHello = function() {
  console.log('Hello');
};

const delayedSayHello = delay(sayHello, 1000);
delayedSayHello();
```

3. **实现模块化**：使用闭包可以实现类似于模块化的功能，将一些相关方法或属性封装在一个作用域内，从而提高代码的复用性和可读性。
```js
const myModule = (function() {
  let privateVariable = 0;

  function privateMethod() {
    // ...
  }

  return {
    publicMethod: function() {
      privateVariable++;
      privateMethod();
      console.log(privateVariable);
    }
  };
})();

myModule.publicMethod(); // 1
myModule.publicMethod(); // 2
```
在上述代码中，myModule 是一个自执行函数，该函数返回了一个包含 publicMethod 方法的对象，公共方法可以访问并修改私有变量和方法。