

* https://medium.com/front-end-hacking/react-native-immutable-listview-example-78662fa64a15#.1p6osls66

ListView 使用的是特殊的语法, Immutable 数据注意特殊处理.

* http://blog.bigbinary.com/2015/08/25/how-to-test-react-native-app-on-real-iphone.html

iPhone 真机上调试 React Native 会有比较啰嗦的问题

* 真机调试修改 IP

`RCTWebSocketExecutor.m` 和 `AppDelegate.m` 的 `localhost` 为 IP.
前者修改 remote JavaScript debugging, 后者修改静态资源

* 不存在 `zIndex`, 使用 `transform` 处理浮层(并不完整的方案)

```js
transform: [
  {translate: [0,0,1]}
],
```

* offline bundle 报错 code sign 问题

需要开发者账号, 并且更改包名与团队对应 `me.ele.XXX`

* 平台差异

status bar, iOS 是隐形的, Android 是不计算在应用内的.

纯文本内容 lineHeight 在 iOS 不生效, padding 在 Android 不生效, 尽量用 flexbox center.

文本框在 Android 当中需要加上 `padding:0` 否则看不到文字部分.

* Android trace

`systracy.py` 生成的 HTML 文件直接打开会报错, 要用 `chrome://tracing/` 去加载.
操作说明点击右边角落的 `?`.

* `_RCTSetLogFunction` 报错

在 Build Setting -> Linking ->  Dead Code Stripping 中设置为 No 就可以了。

* Android 提示 `locale[0]` 报错, 生产环境不要用 hmr 之类的

可能在 Dev Settings 里误选了开发环境, 改过了就好了.

* log

```bash
brew install libimobiledevice
idevice_id --list // list available device UDIDs
idevicesyslog -u <device udid>
```

```bash
adb logcat -T 10
```
