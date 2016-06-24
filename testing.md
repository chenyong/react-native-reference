
单元测试
----

测试框架一般用 Mocha, 是跑在 Node.js 环境的, 所以很多的组件和 API 需要 Mock.
React Virtual DOM 使用 Enzyme 来 Mock, React Native 用 `react-native-mock` 来 Mock.

Redux 相关的测试方案参考的例子比较明确. 组件部分涉及到原生组件, 会遇到比较多问题.

### 一些常用链接

* https://github.com/airbnb/enzyme/blob/master/docs/guides/react-native.md
* https://blog.formidable.com/unit-testing-react-native-with-mocha-and-enzyme-51518f13ba73
* https://medium.com/@thisbejim/testing-react-native-components-with-enzyme-d46bf735540
* https://github.com/airbnb/enzyme/blob/master/docs/api/shallow.md
* https://semaphoreci.com/community/tutorials/getting-started-with-tdd-in-react

### `node_modules/` 中存在 JSX 模块, Babel 漏掉编译

添加一个文件改写 Babel register, 对某些组件做特殊处理:

http://stackoverflow.com/a/35045012/883571

```bash
require('babel-core/register')({
  ignore: /node_modules\/(?!react-native-vector-icons|react-native-tab-navigator)/
});
```

### `require('./react-native')` failed

某个模块里奇怪的 bug, 模块本身已经修复:

https://github.com/oblador/react-native-vector-icons/pull/208

### `ReactDefaultPerf` not found

版本问题, 确认一下 React 的版本 `react@15.0.2`.

https://github.com/brunch/brunch/issues/1349

### 测试 `reducer`

模板参考:

http://pebblecode.com/blog/react-redux-unit-testing/

### mock 网络请求

Use `node-fetch` for fetching and use `nock` to mock requests.

https://github.com/node-nock/nock

### 引用文件报错

Babel 遇到图片是会报错的, 所以要把图片 Mock 掉.
使用 `asset-require-hook` 修改 `require.extensions` 来达成:

https://github.com/aribouius/asset-require-hook

```js
require('asset-require-hook')({
  extensions: ['jpg', 'jpeg', 'png']
})
```

### `ProgressBarAndroid` 不存在

Twitter 上问了下, 说是要从 `react-native-mock` 模块手动添加对应文件给 Mock 掉.

https://github.com/lelandrichardson/react-native-mock/tree/master/src/components
