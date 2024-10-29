# 认知负荷的重要意义

## 简介(Introduction)

这世上有如此多的“流行语”和“最佳实践”，但是让我们来关注一些更基础的东西。那就是——开发人员在浏览代码时的“困惑程度”。

困惑是以时间和金钱为代价的。困惑是由高*认知负荷*造成的。这不是什么花哨的抽象概念，而是一种**人类的基本限制因素**。

由于我们花在阅读和理解代码上的时间远远多于编写代码的时间，所以我们应该不断地问自己，我们是否在代码中嵌入了过多的认知负荷。

## 认知负荷(Cognitive load)

> “认知负荷”（Cognitive load）指的是开发人员为了完成一项任务而需要进行思考的量。

在阅读代码时，你会将诸如变量值、控制流逻辑和调用序列等内容放入你的脑海中。

一般人在[工作记忆](https://baike.baidu.com/item/%E5%B7%A5%E4%BD%9C%E8%AE%B0%E5%BF%86/5197761)中大约可以保存[四个这样的块](https://github.com/zakirullin/cognitive-load/issues/16)。一旦认知负荷达到这个临界值，理解事物就变得更加困难。

*假设我们被要求对一个完全陌生的项目进行一些修复。并被告知在此之前，有一位非常聪明的开发人员在项目中贡献了代码。使用了许多炫酷的架构、花哨的库和前沿的技术。换句话说*，**作者给我们带来了很高的认知负担。**

![Cognitive Load](/img/cognitiveloadv5.png)

我们应该尽可能地减少我们项目中的认知负荷。

## 认知负荷的类型(Types of cognitive load)

**内在的** - 任务本身固有的难度造成的。它无法被降低，是软件开发的核心要素。

**与任务无关的** - 由信息所呈现的方式促成。通常由与任务不直接相关的因素引起，例如：聪明人的“骚操作”。这些是可以避免的。我们将关注这种类型的认知负荷。

![Intrinsic vs Extraneous](/img/smartauthorv13.png)

让我们直接来看看一些“与任务无关的”认知负荷的具体实际例子。

---

我们将认知负荷的“困惑程度”定义如下：

`🧠`: 刚初始化的“工作记忆”，没有认知负荷

`🧠++`: 在我们的“工作记忆”中放入了两项内容，认知负荷增加（`+`越多，负荷越多）

`🤯`:在我们的“工作记忆”中放入了超过4项内容，“工作记忆”“溢出了”

> 我们的大脑实际要更加复杂而神秘，但是我们可以用这个简单模型来简要描述。

## 复杂的条件控制(Complex conditionals)

```go
if val > someConstant // 🧠+
    && (condition2 || condition3) // 🧠+++, 前一个条件必须是 true, c2 和 c3 中的任意一个应该为 true
    && (condition4 && !condition5) { // 🤯, 然后我们就被这个地方整懵逼了
    ...
}
```

## 嵌套的 ifs (Nested ifs)

```go
if isValid { // 🧠+, 这一步我们目前只关心 isValid 这一个变量（是否有效）
    if isSecure { // 🧠++, 这一步我们要同时关心 isValid 和 isSecure 两个变量（是否有效并且安全）
        stuff // 🧠+++
    }
} 
```

和“提早返回”做对比：

```go
if !isValid
    return

if !isSecure
    return

// 🧠, 我们不用去关心已经返回的东西，走到这一步代表所有校验已经通过

stuff // 🧠+
```

我们可以只专注于所我们关心的内容，从而将我们的“工作记忆”从各种先决条件中解放出来。

## 多继承噩梦 (Inheritance nightmare)

我们被要求为我们的管理员用户更改一些内容 `🧠`：

`AdminController extends UserController extends GuestController extends BaseController`

todo
