# Motivation

As the requirements for JavaScript single-page applications have become increasingly complicated, our code must manage more state than ever before. This state can include server responses and cached data, as well as locally created data that has not yet been persisted to the server. UI state is also increasing in complexity, as we need to manage active routes, selected tabs, spinners, pagination controls, and so on.

由于 JavaScript 单页应用日益复杂，我们的代码将会需要管理比以前更多的状态。状态可能包含服务端的响应、缓存的数据，以及本地创建的没有被持久化到服务端的数据。UI 状态的复杂性也在增加，因为我们需要去管理激活的路由、选中的标签、分页器控制等。

Managing this ever-changing state is hard. If a model can update another model, then a view can update a model, which updates another model, and this, in turn, might cause another view to update. At some point, you no longer understand what happens in your app as you have lost control over the when, why, and how of its state. When a system is opaque and non-deterministic, it's hard to reproduce bugs or add new features.

管理这些千变万化的状态是很困难的，如果一个 model 可以更新另一个 model，然后一个 view 也可以更新一个 model，该 model 又可以更新另一个 model，这个 model 反过来可能会导致另一个视图去更新。在某一时刻，你将会不再理解在你的应用中到底发生了什么，因此你已经失去了对其状态的时间、原因和方式的的控制。当一个系统不透明且不确定时，重新问题和增加新特性将会十分困难。