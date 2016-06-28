
数据流
----

### Navigator

对应 Web 中的路由, 主要通过 `navigator.push(route)` `navigator.pop()` API 进行页面的切换.

详细介绍 http://blog.paracode.com/2016/01/05/routing-and-navigation-in-react-native/

React Native 提供的 `Navigator` 组件借助了私有状态.
Redux 场景当中可以借助 `react-native-router-flux`.

### Immutable

React 性能优化依赖 Immutable Data. 移动端由于性能问题,
`shouldComponentUpdate` 是否优化性能的差距非常明显, 特别是在长列表.

Immutable 官方文档非常晦涩, 如果之前并不熟悉概念也许难上手,
教程篇幅也不多, 可以 Google, 比如:

http://www.zsoltnagy.eu/introduction-to-immutable-js/

### Redux

Redux 是模仿 Elm 制作的类 Flux 的数据管理工具.
一些新的术语:

* action

一般是一个对象, 比如 `{type: "DO_SOMETHING"}`.
有参数时可以写成 `{type: "DO_X", a: 'a', b: 'b'}`.

* store

App 的 Model 更新过程的一种状态, 通过 reducer 来定义:

```js
const todoApp = combineReducers({
  todos,
  visibilityFilter
})

let store = createStore(todoApp)
```

* reducer

一个纯函数的 Model 更新的纯函数, 同时也用于定义初始值:

```js
const visibilityFilter = (state = 'SHOW_ALL', action) => {
  switch (action.type) {
    case 'SET_VISIBILITY_FILTER':
      return action.filter
    default:
      return state
  }
}
```

* container

Redux 中顶层的 state 和 action creator 都通过 `connect` 强制绑定到 props 上的.

```js

const mapStateToProps = (state, ownProps) => {
  return {
    active: ownProps.filter === state.visibilityFilter
  }
}

const mapDispatchToProps = (dispatch, ownProps) => {
  return {
    onClick: () => {
      dispatch(setVisibilityFilter(ownProps.filter))
    }
  }
}

const FilterLink = connect(
  mapStateToProps,
  mapDispatchToProps
)(Link)

export default FilterLink
```

* 例子

前面的术语说明只能给一些大概的说明, 不能解释清楚概念.
书写的完整的例子比较绕, 需要参照文档的代码:

http://redux.js.org/docs/basics/ExampleTodoList.html

### Redux DevTools

复杂应用可接借助它来调试:

https://github.com/gaearon/redux-devtools
