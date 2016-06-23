
Native 代码
----

大致提供了两类方案可以封装 Native 代码到 js 环境当中:

* Native Modules -- 代码模块
* Native UI Component -- UI Widgets

大致提供属性事件等等.. 由于是 Objective-C 代码, 不大可能 js 前端去写.
之前和 iOS 开发讨论认为 React Native 做应用, 原因 API 严重不足, 只适合界面.

官方提供的 API 大致梳理:

* `ActionSheetIOS` -- iOS 从下方显示的弹出框
* `Alert`
* `AlertIOS`
* `Animated` -- js 实现的动画 API
* `AppRegistry`
* `AppState` -- 获取当前 App 的显示隐藏状态
* `AsyncStorage` -- 基于平台数据库封装的类似 localStorage 的异步 API
* `BackAndroid` -- 监听 Android 的返回按钮
* `CameraRoll` -- 获取图片, 得到各种信息用于显示
* `Clipboard` -- 剪切板
* `DatePickerAndroid`
* `Dimensions` -- 获取 App 渲染区域的尺寸的
* `IntentAndroid` -- 用 `Linking`
* `InteractionManager` -- 听说类似 `requestAnimationFrame`
* `LayoutAnimation` -- 自动生成组件的渐变, iOS
* `Linking` -- 与传入和传出的 App 链接进行交互的 API
* `NativeMethodsMixin` -- 直接访问原生组件的命令式 API, 包括 `measure measureLayout setNativeProps focus blur`
* `NetInfo` -- 当前网络状态
* `PanResponder` -- 处理手势
* `PixelRatio` -- 根据像素密度获取指定大小的图片
* `PushNotificationIOS`
* `StatusBarIOS` -- 控制状态栏的 Component
* `StyleSheet` -- 计算 css-layout
* `TimePickerAndroid`
* `ToastAndroid` -- 悬浮的提示信息
* `VibrationIOS`
* `Vibration`

从 Web 开发对照看 API 算是不少了. 大概相比 Native 平台不行.
