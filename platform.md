
平台差异
----

通过 `x.android.js` 和 `x.ios.js` 进行区分然后自动加载.
确实会增加维护方面的成本.

通过 `require('react-native').Platform.OS` 可以区别操作系统.

### Sticky Header

仅在 iOS 中实现.

### scroll position

### 文本居中

### Status bar

iOS 中滚动界面区域包含 status bar, Android 当中不包括.
当前的做法是手工在 iOS 里设置了 `paddingTop` 来低消影响.

另外通过 `Dimensions` API 查询屏幕大小时也要注意这一点带来的影响.

### Loading spinner

Android 当中是 `ProgressBarAndroid`, iOS 当中是 `ActivityIndicatorIOS`,
界面和参数不一致, 但是可以引用社区的组件写法:

https://github.com/FaridSafi/react-native-gifted-spinner
