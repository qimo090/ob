---
tags:
  - JavaScript
  - 继承
  - 原型链
---
# 建议回答

- 1、**原型链继承**：将父类的实例作为子类的原型，通过 prototype 进行继承
- 2、**构造继承**：将父类的实例属性复制给子类，通过 call 进行继承
- 3、**实例继承**：为父类实例添加新特性，作为子类实例返回
- 4、**拷贝继承**：将父类实例通过循环拷贝给子类
- 5、**组合继承**：就是 原型链继承 和 构造继承，一起使用
- 6、**寄生组合继承**：通过寄生方式，砍掉父类的实例属性，避免了 组合继承中，在调用两次父类的构造时，初始化两次实例方法/属性 的缺点

# 技术详解

在JavaScript中，实现继承的方式有以下几种：

1. 原型链继承：通过将子类的原型指向父类的实例来实现继承。这种方式存在的问题是，所有子类实例共享同一个父类实例，容易造成属性共享和修改父类属性的问题。
```js
function Parent() {
  this.name = "parent";
}

Parent.prototype.sayName = function () {
  console.log(this.name);
};

function Child() {
  this.type = "child";
}

Child.prototype = new Parent();

var child = new Child();
child.sayName(); // 'parent'
```

2. 借用构造函数继承：通过在子类构造函数中调用父类构造函数来实现继承。这种方式可以避免属性共享的问题，但是无法继承父类原型上的方法。
```js
function Parent() {
  this.name = 'parent';
}

function Child() {
  Parent.call(this);
  this.type = 'child';
}

var child = new Child();
console.log(child.name); // 'parent'
```

3. 组合继承：将原型链继承和借用构造函数继承结合起来，既可以继承父类原型上的方法，又可以避免属性共享的问题。
```js
function Parent() {
  this.name = 'parent';
}

Parent.prototype.sayName = function() {
  console.log(this.name);
}

function Child() {
  Parent.call(this);
  this.type = 'child';
}

Child.prototype = new Parent();
Child.prototype.constructor = Child;

var child = new Child();
child.sayName(); // 'parent'
console.log(child.name); // 'parent'
```

4. 原型式继承：通过创建一个临时构造函数并将其原型设置为父类实例来实现继承。这种方式类似于原型链继承，但是可以避免创建不必要的父类实例。
```js
function createObject(obj) {
  function F() {}
  F.prototype = obj;
  return new F();
}

var parent = {
  name: 'parent',
  sayName: function() {
    console.log(this.name);
  }
};

var child = createObject(parent);
child.name = 'child';
child.sayName(); // 'child'
```

5. 寄生式继承：在原型式继承的基础上，增强新对象，返回构造函数的方式来实现继承。
```js
function createObject(obj) {
  function F() {}
  F.prototype = obj;
  return new F();
}

function createChild(parent) {
  var child = createObject(parent);
  child.name = 'child';
  child.sayName = function() {
    console.log(this.name);
  };
  return child;
}

var parent = {
  name: 'parent',
  sayName: function() {
    console.log(this.name);
  }
};

var child = createChild(parent);
child.sayName(); // 'child'
```

6. 寄生组合式继承：在组合继承的基础上，使用Object.create()方法来创建父类原型的副本，避免了调用父类构造函数时创建不必要的实例。
```js
function inherit(child, parent) {
  var prototype = Object.create(parent.prototype);
  prototype.constructor = child;
  child.prototype = prototype;
}

function Parent() {
  this.name = 'parent';
}

Parent.prototype.sayName = function() {
  console.log(this.name);
}

function Child() {
  Parent.call(this);
  this.type = 'child';
}

inherit(Child, Parent);

var child = new Child();
child.sayName(); // 'parent'
console.log(child.name); // 'parent'
```
