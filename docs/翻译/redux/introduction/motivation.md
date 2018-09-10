# Motivation

As the requirements for JavaScript single-page applications have become increasingly complicated, our code must manage more state than ever before. This state can include server responses and cached data, as well as locally created data that has not yet been persisted to the server. UI state is also increasing in complexity, as we need to manage active routes, selected tabs, spinners, pagination controls, and so on.

由于 JavaScript 单页应用日益复杂，我们的代码将会需要管理比以前更多的状态。状态可能包含服务端的响应、缓存的数据，以及本地创建的没有被持久化到服务端的数据。UI 状态的复杂性也在增加，因为我们需要去管理激活的路由、选中的标签、分页器控制等。

Managing this ever-changing state is hard. If a model can update another model, then a view can update a model, which updates another model, and this, in turn, might cause another view to update. At some point, you no longer understand what happens in your app as you have lost control over the when, why, and how of its state. When a system is opaque and non-deterministic, it's hard to reproduce bugs or add new features.

管理这些千变万化的状态是很困难的，如果一个 model 可以更新另一个 model，然后一个 view 也可以更新一个 model，该 model 又可以更新另一个 model，这个 model 反过来可能会导致另一个视图去更新。在某一时刻，你将会不再理解在你的应用中到底发生了什么，因此你已经失去了对其状态的时间、原因和方式的的控制。当一个系统不透明且不确定时，重新问题和增加新特性将会十分困难。

As if this wasn't bad enough, consider the new requirements becoming common in front-end product development. As developers, we are expected to handle optimistic updates, server-side rendering, fetching data before `performing route transitions`, and so on. We find ourselves trying to manage a complexity that we have never had to deal with before, and we `inevitably` ask the question: is it time to give up? The answer is no.

好像这还不足够糟糕，考虑新需求在前端产品开发中变得普遍。作为开发者，我们被期待去管理乐观的更新、服务端渲染、在`执行路由切换`之前获取数据，等等。我们发现自己尝试去管理以前从未有过的复杂性，我们`不得不`提出这个问题；是时候放弃了吗？答案是否。

This complexity is difficult to handle as we're mixing two concepts that are very hard for the human mind to `reason about`: mutation and asynchronicity. I call them `Mentos` and `Coke`. Both can be great in separation, but together they create a mess. Libraries like React attempt to solve this problem in the view layer by removing both asynchrony and direct DOM manipulation. However, managing the state of your data is left up to you. This is where Redux enters.

这个复杂度非常难以控制，因为我们混合了两个人类非常难以`推理`的概念——"突变"和"异步"。我将他们称之为`曼妥思`和`可乐`，他们俩在独立时都很好，但是在一起就会带来混乱。像 React 这样的库尝试图通过在视图层移除异步和直接的 DOM 操作来解决这一问题。然后，管理你数据的状态还是由你自己决定，这便是 Redux 所进入的领域。

Following in the steps of Flux, CQRS, and Event Sourcing, Redux attempts to make state mutations predictable by `imposing certain restrictions` on how and when updates can happen. These restrictions `are reflected in` the three principles of Redux.

跟随 Flux、CQRS 以及事件源的脚步，Redux 尝试着通过对更新的方式和时机`施加某些限制`来达到状态突变的可预测。这些限制`被反映在` Redux 的三个原则中。
