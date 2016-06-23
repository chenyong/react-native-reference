
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

(需要补充)
