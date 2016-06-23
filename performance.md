
性能
----

### 环境变量

注意 `DEV` 环境变量是否开启对性能会有直接的影响.

### 线程

分为三种 UI Thread, JS Thread, Native Modules Thread.

由于 js 性能差距, 一般性能问题都在 js 中查找. 调试的方案在文档中有写:

https://facebook.github.io/react-native/docs/android-ui-performance.html

### ListView

一方面是首次渲染的性能, 一方面是更新时的性能.

首次渲染通过 ListView 可以控制只渲染一屏多的内容, 节省时间.

更新过程通过 `shouldComponentUpdate` 就可以节省大部分的时间.
另外用 `ListView` 的话, row 更新的判断逻辑通过不可变数据也许可以加快:

```js
let dataSource = new ListView.DataSource({
  rowHasChanged: (r1, r2) => r1 !== r2
});
```

### 图片懒加载

React Native 当中的默认列表挂载时会抓取全部的图片.

Demo 中对 Android 做了手工处理, 只渲染可见区域的图片, 其他图片位置用空的 `View` 代替.

网上有找到一个组件, 在组件中遍历组件树加载可见的图片. 但不清楚是否会导致副作用.

https://github.com/IskenHuang/react-native-scrollview-lazyload

### 性能调试

对于 JavaScript 线程可以连接到 Chrome DevTools 当中通过 Timeline 查看.

对于 Android 性能, 可以参考文档用 `systrace.py` 抓取数据通过 `chrome://tracing` 查看.
不过没有比较多经验从 Android 的图表中大看不到什么, 一般性能问题应该在 JavaScript 里.

https://facebook.github.io/react-native/docs/android-ui-performance.html

调试菜单中开启 `Perf Monitor` 能显示帧率.
