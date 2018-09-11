# Core Concepts

Imagine your app’s state is described as a plain object. For example, the state of a todo app might look like this:

想象你的应用的状态用纯对象来描述，举例来说，一个 todo 应用的状态可能是这样：

```js
{
  todos: [{
    text: 'Eat food',
    completed: true
  }, {
    text: 'Exercise',
    completed: false
  }],
  visibilityFilter: 'SHOW_COMPLETED'
}
```

This object is like a “model” except that there are no setters. This is so that different parts of the code can’t change the state arbitrarily, causing hard-to-reproduce bugs.

这个对象像一个 "model" 除了这里没有 setters，这样代码的不同部分不能随意地改变状态，从而导致难以重现的 bug。

To change something in the state, you need to dispatch an action. An action is a plain JavaScript object (notice how we don’t introduce any magic?) that describes what happened. Here are a few example actions:

为了修改状态中的某些值，你需要去发送一个 action，一个 action 是一个描述了什么会发生的纯 JavaScript 对象（注意我们怎么不介绍任何魔法？），这里有一些 action 的例子：

```js
{ type: 'ADD_TODO', text: 'Go to swimming pool' }
{ type: 'TOGGLE_TODO', index: 1 }
{ type: 'SET_VISIBILITY_FILTER', filter: 'SHOW_ALL' }
```

Enforcing that every change is described as an action lets us have a clear understanding of what’s going on in the app. If something changed, we know why it changed. Actions are like breadcrumbs of what has happened. Finally, to tie state and actions together, we write a function called a reducer. Again, nothing magical about it—it’s just a function that takes state and action as arguments, and returns the next state of the app. It would be hard to write such a function for a big app, so we write smaller functions managing parts of the state:

强迫每一个 change 被描述成 action 让我们对应用中什么将要发生有一个清晰的理解。如果某些状态改变了，我们知道它为什么会改变。action 就像发生了什么的面包屑。最后，为了把 state 和 action 联系起来，我们写了一个叫作 "reducer" 的函数。再次强调，它没有什么神奇的地方——它只是一个吧 state 和 action 作为参数的函数，同时返回应用的下一次状态。为大型应用书写这样的函数可能是困难的，因此我们写了一些更小的函数来管理局部的状态。

```js
function visibilityFilter(state = 'SHOW_ALL', action) {
  if (action.type === 'SET_VISIBILITY_FILTER') {
    return action.filter
  } else {
    return state
  }
}
​
function todos(state = [], action) {
  switch (action.type) {
    case 'ADD_TODO':
      return state.concat([{ text: action.text, completed: false }])
    case 'TOGGLE_TODO':
      return state.map(
        (todo, index) =>
          action.index === index
            ? { text: todo.text, completed: !todo.completed }
            : todo
      )
    default:
      return state
  }
}
```

And we write another reducer that manages the complete state of our app by calling those two reducers for the corresponding state keys:

我们还写了另一个通过调用对应的状态键来调用这两个 reducer 的管理了全部的应用状态的 reducer：

```js
function todoApp(state = {}, action) {
  return {
    todos: todos(state.todos, action),
    visibilityFilter: visibilityFilter(state.visibilityFilter, action)
  }
}
```

This is basically the whole idea of Redux. Note that we haven’t used any Redux APIs. It comes with a few utilities to facilitate this pattern, but the main idea is that you describe how your state is updated over time in response to action objects, and 90% of the code you write is just plain JavaScript, with no use of Redux itself, its APIs, or any magic.

这基本上是 redux 的全部概念。请注意我们还没有使用任何的 Redux API。它附带了一些实用工具来使这种模式变得容易，但主要的思想是还是描述如何状态如何随时间更新，以响应 action 对象，并且 90% 的代码只是普通的 JavaScript，没有使用 Redux 本身、它的 API 或任何魔术。