---
tags:
  - JavaScript
  - JavaScript/Object
create time: 2024-05-29T23:08:00
update time: 2024-05-29T23:08:00
url: https://www.30secondsofcode.org/js/s/observable-proxy/
created: 2024-05-29T23:04
updated: 2024-06-10T13:43
---
观察者模式是一种设计模式，其中对象（称为主体）维护一个从属项（观察者）列表，这些从属项（观察者）在对象状态的任何更改时都会收到通知。只要稍加聪明，我们就可以利用`EventTarget`接口和`Proxy`对象在 JavaScript 中实现 Observer 模式。

> [!Note]
> 我正在使用该`EventTarget`接口，因为它在浏览器和 Node.js 环境之间很常见。如果您只使用 Node.js，它会 `EventEmitter` 提供更强大的解决方案，但您必须进行一些调整。

Observer 模式的核心是一个简单的发布/订阅（[发布-订阅](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern)）系统。我们可以创建一个扩展接口的`Observable``EventTarget`类，并使用一个`Proxy`对象通过`set`陷阱拦截属性更改。

当属性发生更改时，将创建一个 a `CustomEvent` 来通知任何观察者，并将属性的名称作为其`type`，将新值作为其 `detail`.最后，事件将通过 [`EventTarget.dispatchEvent()`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/dispatchEvent)调度，通知所有已注册的听众。

```javascript
class Observable extends EventTarget {
  constructor() {
    super();
    return new Proxy(this, {
      set: (target, property, value) => {
        target[property] = value;
        this.dispatchEvent(new CustomEvent(property, { detail: value }));
        return true;
      },
    });
  }
}

const subject = new Observable();

subject.addEventListener('name', event => {
  console.log(`Name changed to ${event.detail}`);
});

subject.name = 'Alice'; // Name changed to Alice
```

> [!bug] 警告
> 该段代码不能在浏览器或 NodeJS 环境运行
> `TypeError: Illegal invocation`

虽然此代码非常简单，但可以轻松扩展以处理更复杂的用例，例如嵌套对象或数组。它甚至可以用来创建一个可观察的存储，类似于 Redux。尝试一下，看看你能走多远！