
部署
----

### Android 打包

(需要补充) 配置 key_strore 作为证书, 通过命令打包

文档 https://facebook.github.io/react-native/docs/running-on-device-android.html

### iOS 打包

* `release` 环境

通过 Xcode 操作 `Product > Scheme > Edit Scheme` 设置 `release`.
修改 `AppDelegate.m` 中的 `jsCodeLocation` 到对应地址(也可能是 CodePush).
然后点击运行.

* `release` 环境 Archive

(需要补充)

通过 Xcode 操作 `Product > Archive` 可以生成一个 `.xarchive` 文件.
拖动该文件到 iTunes 当中, 然后可以通过 iTunes 的图形界面安装应用.
