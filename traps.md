
常见问题
----

### ListView 使用 Immutable Data

ListView 使用的是特殊的语法, Immutable 数据注意特殊处理.

https://medium.com/front-end-hacking/react-native-immutable-listview-example-78662fa64a15#.1p6osls66

### 实体机怎样调试 iOS

iPhone 上调试 React Native 会有比较啰嗦的问题.
按照文档走, 不清楚的步骤可以参考下网上的文章, 比如:

http://blog.bigbinary.com/2015/08/25/how-to-test-react-native-app-on-real-iphone.html

### 非 Simulator 调试需要修改 IP

iOS 当中, `RCTWebSocketExecutor.m` 和 `AppDelegate.m` 的 `localhost` 为 IP.
前者修改 remote JavaScript debugging, 后者修改静态资源

### 不存在 `zIndex`

使用 `transform` 处理浮层(并不完整的方案)

```js
transform: [
  {translate: [0,0,1]}
],
```

还是建议通过 virtual DOM 结构入手解决问题.

### offline bundle 报错 code sign 问题

iOS 存在限制, 不像是 Android 能随意安装应用. 除了开发环境, 打包的应用需要开发者账号才能安装.
需要购买开发者账号或者加入付费的团队, 并且更改包名与团队对应 `me.ele.XXX`, 然后才能安装.

开发者账号通过证书验证, 具体证书申请和安装步骤 http://www.jianshu.com/p/9d9e3699515e

### Android trace

`systracy.py` 生成的 HTML 文件直接打开会报错, 要用 `chrome://tracing/` 去加载.
操作说明点击右边角落的 `?`.

### `_RCTSetLogFunction` 报错

在 `Build Setting -> Linking ->  Dead Code Stripping` 中设置为 No 就可以了。

### Android 提示 `locale[0]` 报错, 生产环境不要用 hmr 之类的

可能在 Dev Settings 里误选了开发环境, 改过了就好了.
