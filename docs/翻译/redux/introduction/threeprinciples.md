# Three Principles

Redux can be described in three fundamental principles:

Redux 可以被描述成 3 个基本的原则：

## Single source of truth (单一事件源)

**The state of your whole application is stored in an object tree within a single store.**

**整个应用的状态以一个单一的 store 存储在一个对象树中。**

This makes it easy to create universal apps, as the state from your server can be serialized and hydrated into the client with no extra coding effort. A single state tree also makes it easier to debug or inspect an application; it also enables you to persist your app's state in development, for a faster development cycle. Some functionality which has been traditionally difficult to implement - Undo/Redo, for example - can suddenly become trivial to implement, if all of your state is stored in a single tree.

这会让创建同构应用变得简单，因为服务端的状态可以没有任何额外的代码成本，就被序列化并水合到客户端中。单一状态树也会使调试和检查应用变得容易。它还使您可以在开发中持久化应用程序的状态，从而获得更快的开发周期。一些传统上难以实现的功能，如：撤销/重做，受益于单一的状态树，以前难以实现的如“撤销/重做”这类功能也变得轻而易举。