
部署
----

### Android 打包

(需要补充) 配置 key_strore 作为证书, 通过命令打包

文档 https://facebook.github.io/react-native/docs/running-on-device-android.html

### iOS 打包

iOS 环境安装 offline bundle 需要有开发者账号.
由于开发者账号需要购买, 一般还是加入开发团队比较好.
开发者账号之后需要配置证书, 开发者账号通过证书验证, 具体证书申请和安装步骤参考:

http://www.jianshu.com/p/9d9e3699515e

打包通过 Xcode 操作 `Product > Scheme > Edit Scheme` 设置 `release`.
修改 `AppDelegate.m` 中的 `jsCodeLocation` 到对应地址(也可能是 CodePush).
然后点击运行.

* 使用 Archive

Archive 功能可以生成发布到 App Store 的包, 也不用手动改配置, 似乎比较方便...

(需要补充)

通过 Xcode 操作 `Product > Archive` 可以生成一个 `.xarchive` 文件.
拖动该文件到 iTunes 当中, 然后可以通过 iTunes 的图形界面安装应用.
