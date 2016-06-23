
开发
----

### 调试

开发环境运行的思路是 `react-native start` 命令启动一个服务器,
然后移动端通过网络和端口连接到服务器上获取 JavaScript 资源.
React Native 开发工具中封装了一个 Webpack(推测是修改版) 用于处理打包和热替换.

手机或者模拟器当中需要安装对应的 App,
一般通过 `react-native run-ios` 或者 `react-native run-android` 直接完成.
iOS 真机当中安装需要借助 XCode.

Android 模拟器可以用 Android Studio. 也有第三方的模拟器比如 GenyMotion, 但是我没有安装成功.

Android USB 调试的情况下可以用 `adb reverse tcp:8081 tcp:8081` 进行网络代理.
或者在调试菜单的 `Dev Settings` 里手动填写局域网的 IP 以及端口, 如 `192.168.0.66:8081`.

iOS 真机调试需要修改文件来指定 HTTP 服务器的 IP, 参考文档:

* https://facebook.github.io/react-native/docs/running-on-device-ios.html
* https://facebook.github.io/react-native/docs/running-on-device-android.html

### 查看日志

远程调试 js 时 log 在 DevTools Console 可以直接看.

Simulator 的 Log 可以在 Safari 的 `Develop > Simulator` 当中查看.

iOS 实体机的 log:

```bash
brew install libimobiledevice
idevice_id --list // list available device UDIDs
idevicesyslog -u <device udid>
```

Android 实体机的 log:

```bash
adb logcat -T 10
```

### 注意

一次只能连接一个 hot reloading. 一次只能连接一个 js remote debug.

iOS 的 offline bundle 需要开发者账号, 直接调试则不用.

### 调用调试菜单

* iOS Simulator

`Hardware >  Shake Gesture`

* Android Simulator

某些情况没有 Shake 按钮, 通过 adb 工具模拟键盘事件:

```bash
adb shell input keyevent 82
```

* iOS 实体机

摇一摇

* Android 实体机

摇一摇

### 查看网络请求

* HTTP 请求

远程调试 js 并不能看到网络请求, 可以通过 WIFI 设置代理到电脑上指定端口,
然后从 Charles 等网络调试工具查看. 参考:

http://bo1.me/2015/04/01/charles-android/

前端开发者推荐用基于 DevTools 开发的 [Betwixt](https://github.com/kdzwinel/betwixt). 默认端口 `8008`.


* HTTPS 请求

(需要补充)

