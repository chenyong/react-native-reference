
开发
----

### 调试

开发环境运行的思路是 `react-native start` 命令启动一个服务器,
然后移动端通过网络和端口连接到服务器上获取 JavaScript 资源.

手机或者模拟器当中需要安装对应的 App,
一般通过 `react-native run-ios` 或者 `react-native run-android` 直接完成.
iOS 真机当中安装需要借助 XCode.
Android 模拟器可以用 Android Studio. 也有第三方的模拟器但是我没有安装成功.

Android USB 调试的情况下可以用 `adb reverse tcp:8081 tcp:8081` 进行网络代理.
iOS 真机调试需要修改文件来指定 HTTP 服务器的 IP, 参考文档:

https://facebook.github.io/react-native/docs/running-on-device-ios.html
https://facebook.github.io/react-native/docs/running-on-device-android.html

### 注意

一次只能连接一个 hot reloading. 一次只能连接一个 js remote debug.

iOS 的 offline bundle 需要借助开发者账号, 直接调试则不用.
