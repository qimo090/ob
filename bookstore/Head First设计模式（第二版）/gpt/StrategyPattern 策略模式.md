---
tags:
  - DesignPattern
  - StrategyPattern
type: 对象行为型
source: GPT
---
# 智谱清言
策略模式（Strategy Pattern）是一种行为设计模式，它定义了一系列的算法，把它们一个个封装起来，并且使它们可以互相替换。该模式让算法的变化独立于使用算法的客户。策略模式属于对象行为型模式，它通过对算法进行封装，把使用算法的责任和算法的实现分割开来，并委派给不同的对象对这些算法进行管理。

在策略模式中，通常会有以下几种角色：
1. **策略接口（Strategy）**：定义所有支持的算法的公共接口。任何实现了该接口的类都是一种策略。
2. **具体策略（Concrete Strategy）**：实现策略接口的类。具体策略封装了具体的算法和行为。
3. **上下文（Context）**：使用策略对象的类。上下文接受客户的请求，随后把请求委托给某一个策略对象。上下文并不知道具体策略对象所使用的是哪一个算法。

策略模式的主要优点：
- **算法可以自由切换**：策略模式提供了对开放-关闭原则的完美支持，用户可以在不修改原有系统的基础上选择算法或行为，也可以灵活地增加新的算法或行为。
- **避免使用多重条件转移语句**：多重条件转移语句不易维护，它把采取哪一种算法或采取哪一种行为的逻辑与算法或行为的逻辑混合在一起，统统列在一个多重条件语句里面，容易出错。而策略模式使用组合而非继承，把采取行为的逻辑放在环境类中，把不同策略的实现放在具体策略类中，从而使算法或行为改变的时候，系统仅仅需要引入新的策略类。
- **提供相同行为的不同实现**：策略模式提供了一种解决方案，我们可以定义一些策略类，每一个策略类中封装一种具体的算法。然后在环境类中定义一个策略接口类型的成员变量，在具体的环境类中，通过注入不同的策略对象，来使用不同的算法和行为。

策略模式的缺点：
- **客户端必须知道所有的策略类，并自行决定使用哪一个策略类**：这就意味着客户端需要理解这些算法的区别，以便选择合适的算法类。这也是策略模式的一个缺点，客户端需要理解它所选择的策略到底是怎样实现的。
- **策略模式将产生很多策略类**：任何细小的变化都可能需要增加一个新的策略类，这会使得系统中类的个数成倍增加。

策略模式在软件开发中应用非常广泛，特别是在需要根据不同条件选择不同算法的场景下，例如排序算法的切换、支付方式的选择等。通过使用策略模式，可以提高代码的灵活性和可维护性。

## 示例代码

下面是一个使用 TypeScript 实现的简单策略模式的示例代码。这个例子中，我们将实现一个文本格式化程序，它可以根据不同的策略来格式化文本：一种是转换为大写，另一种是转换为小写。
首先，我们定义策略接口和两个具体的策略类：
```typescript
// 策略接口
interface TextFormatterStrategy {
    format(text: string): string;
}
// 具体策略类：转换为大写
class ToUpperCase implements TextFormatterStrategy {
    format(text: string): string {
        return text.toUpperCase();
    }
}
// 具体策略类：转换为小写
class ToLowerCase implements TextFormatterStrategy {
    format(text: string): string {
        return text.toLowerCase();
    }
}
```
接下来，我们定义上下文类，它将使用策略对象来格式化文本：
```typescript
// 上下文类
class TextFormatter {
    private strategy: TextFormatterStrategy;
    constructor(strategy: TextFormatterStrategy) {
        this.strategy = strategy;
    }
    // 设置策略
    setStrategy(strategy: TextFormatterStrategy) {
        this.strategy = strategy;
    }
    // 格式化文本
    formatText(text: string): string {
        return this.strategy.format(text);
    }
}
```
最后，我们创建一个客户端代码来使用这些策略：
```typescript
// 客户端代码
const text = "Hello, World!";
const formatter = new TextFormatter(new ToUpperCase());
console.log(formatter.formatText(text)); // 输出: HELLO, WORLD!
formatter.setStrategy(new ToLowerCase());
console.log(formatter.formatText(text)); // 输出: hello, world!
```
在这个例子中，`TextFormatter` 是上下文类，它接受一个 `TextFormatterStrategy` 对象作为策略。客户端代码可以创建不同的策略对象（`ToUpperCase` 或 `ToLowerCase`），并通过 `TextFormatter` 类来使用这些策略。通过这种方式，我们可以轻松地切换文本格式化的策略，而无需修改 `TextFormatter` 类的实现。

# ChatGPT

策略模式（Strategy Pattern）是一种行为设计模式，用于定义一系列算法，使它们可以独立于客户端而相互替换。这种模式使得算法可以在不影响客户端的情况下单独变化。策略模式通常涉及三种角色：上下文（Context）、策略（Strategy）和具体策略（Concrete Strategy）。

1. **上下文（Context）**：上下文是持有策略对象的类。上下文通过将请求委托给策略对象，将客户端和策略对象解耦。上下文类通常会包含一个指向抽象策略的引用，可以在运行时动态地更改具体策略对象。

2. **策略（Strategy）**：策略是一个接口或抽象类，定义了算法的通用接口。它是所有具体策略类的基类，声明了一个公共方法或一组方法，用于执行算法。

3. **具体策略（Concrete Strategy）**：具体策略是实现策略接口的类。每个具体策略类都实现了策略接口，并提供了其具体的算法实现。

策略模式的核心思想是将算法的实现与使用算法的客户端代码分离开来。这样，客户端就可以独立于具体的算法进行变化，只需选择合适的策略即可。策略模式通常用于解决某个问题有多种解决方案的情况，或者在不同情况下需要采取不同的行为。通过使用策略模式，可以使系统更灵活、可扩展，同时也更容易进行单元测试和维护。

策略模式有许多优点，但也存在一些缺点。下面是策略模式的主要优点和缺点：

**优点：**

1. **增强代码可读性和可维护性：** 策略模式将不同的算法封装到独立的策略类中，使得代码结构更清晰，易于理解和维护。
2. **灵活性和扩展性：** 策略模式允许在运行时动态地切换算法，甚至可以动态地增加新的策略类，而无需修改上下文类的代码，从而提高了系统的灵活性和扩展性。
3. **避免使用条件语句：** 策略模式避免了使用大量的条件语句来选择不同的算法，使得代码更加简洁和可维护。
4. **单一责任原则：** 策略模式遵循单一责任原则，每个具体策略类都只负责自己的算法实现，使得类的设计更加符合面向对象的设计原则。
5. **提高代码复用性：** 策略模式将算法封装到独立的策略类中，可以在不同的上下文中复用相同的策略。

**缺点：**

1. **增加类的数量：** 策略模式会导致系统中出现大量的策略类，如果策略较多，可能会增加系统的复杂性。
2. **客户端必须了解所有的策略：** 客户端必须了解所有的策略类，以便在运行时选择合适的策略，这可能会增加客户端的复杂性。
3. **可能会导致性能损失：** 在运行时动态切换策略可能会导致一定程度的性能损失，因为需要额外的代码来进行策略选择。

总的来说，策略模式是一种非常有用的设计模式，可以使系统更灵活、可扩展，提高代码的可读性和可维护性。然而，在使用策略模式时，需要根据具体情况权衡其优缺点，并遵循设计原则来设计和实现策略类。

## 示例代码

策略模式（Strategy Pattern）是一种行为设计模式，它定义了一系列算法，将每个算法封装起来，并使它们可以相互替换。策略模式可以使算法独立于客户端而独立变化。

在 TypeScript 中实现策略模式，你可以首先定义一个接口或抽象类来表示策略，然后创建不同的具体策略类，最后在客户端中使用这些策略类。下面是一个简单的 TypeScript 实现：

```typescript
// 定义策略接口
interface PaymentStrategy {
    pay(amount: number): void;
}

// 具体策略：支付宝支付
class AlipayStrategy implements PaymentStrategy {
    pay(amount: number): void {
        console.log(`支付宝支付：￥${amount}`);
    }
}

// 具体策略：微信支付
class WechatPayStrategy implements PaymentStrategy {
    pay(amount: number): void {
        console.log(`微信支付：￥${amount}`);
    }
}

// 具体策略：信用卡支付
class CreditCardStrategy implements PaymentStrategy {
    pay(amount: number): void {
        console.log(`信用卡支付：￥${amount}`);
    }
}

// 上下文类
class PaymentContext {
    private paymentStrategy: PaymentStrategy;

    constructor(paymentStrategy: PaymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    // 设置支付策略
    setPaymentStrategy(paymentStrategy: PaymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    // 执行支付
    doPayment(amount: number) {
        this.paymentStrategy.pay(amount);
    }
}

// 使用示例
const paymentContext = new PaymentContext(new AlipayStrategy());

paymentContext.doPayment(1000); // 输出：支付宝支付：￥1000

// 切换支付策略
paymentContext.setPaymentStrategy(new WechatPayStrategy());

paymentContext.doPayment(800); // 输出：微信支付：￥800
```

在这个示例中，我们定义了一个 `PaymentStrategy` 接口，表示支付策略。然后我们实现了几种具体的支付策略类，如 `AlipayStrategy`、`WechatPayStrategy` 和 `CreditCardStrategy`。最后，我们定义了一个 `PaymentContext` 类，它持有一个 `PaymentStrategy` 对象，并提供了方法来设置和执行支付策略。

这样，客户端可以根据需要选择不同的支付策略，并且可以很容易地切换策略而不影响客户端的代码。