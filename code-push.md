
React Native CodePush
----

### 概览

CodePush 是微软提供的代码推送服务, 用于 React Native 和 Codova 的代码更新.
大致似乎是在 Native 代码里加入 SDK, 通过 API 自动检查和下载安装新版本 js 代码.

使用 CodePush 需要往 Native 代码当中插入 SDK, 在 js 中调用 API.
不需要定制 UI 的情况下, 可以直接用 `sync` API 自动处理更新:

```bash
codePush.sync(); // 静默更新

codePush.sync({ updateDialog: true, installMode: codePush.InstallMode.IMMEDIATE });
```

### 层级

```text
App > Deployment > Release
```

App 创建后有默认的两个 `deploymentName`: `Staging`, `Production`, 也可以在发布时指定新的.
App 的更新通过 deployment key 进行识别, 名字可以随意更改.

运行 `release` 子命令可以在对应的 deployment 当中增加版本.
可以通过 `history` 子命令查看所有版本.

### 概念

* package

每次 release 都会往 CodePush 服务器上传一个包,
这个包当中包含的内容主要是 js 文件打的一个 bundle, 以及一些图片.
文件内容在更新时做 differential updates, 只下载需要的文件(需要更多细节).

* target binary version

js 代码对 Native 版本可能存在依赖. 所以发布时需要和 binary 代码的版本号指定对应.
默认会去 Xcode 或者 gradle 的配置文件里读取当前版本.

* rollout

这个参数指定多少比例的用户进行更新, 灰度发布.

* mandatory

强制更新. 比如一些涉及安全性的更新, 可以指定强制更新.

* rollback

回滚. `rollback` 命令会生成一个新的版本的 release, 内容为回滚一个版本的代码.
更新机制里会检查 Hash 所以回滚的情况不需要下载新的代码进行更新.

* release

版本的管理主要有 `release` `patch` `promote` `rollback`.

`release` 子命令用于发布版本, `patch` 子命令只能修改版本的描述, 不能修改内容.
`promote` 可以用于提升 `Staging` 为 `Production`.

* `InstallMode`

默认有三种安装模式可以选择: `IMMEDIATE` `ON_NEXT_RESTART` `ON_NEXT_RESUME`.

### 使用

大致的步骤包括:

* 安装 `code-push` 命令行工具
* 注册
* 创建 app, 或者 Staging 的 deployment key
* 在 Native 代码中加入 CodePush 代码
* 配置  deployment key
* 在 js 代码中增加 CodePush 配置的代码, 以便应用启动时检查更新
* 安装 app 到 OS 当中
* ...更新版本时通过 `release-react` 命令更新版本
* ...App 重启, 自动检查下载更新

配置步骤比较繁琐, 需要依据官方文档的步骤:

* https://github.com/Microsoft/code-push/blob/master/cli/README.md
* https://github.com/Microsoft/react-native-code-push

一些中文翻译的资源:

* http://hammercui.github.io/post/react-native-android实战：4-CodePush/
* http://bbs.reactnative.cn/topic/725/code-push-热更新使用详细说明和教程
* https://senpng.github.io/2016/03/23/code-push/

### 关于 log

CodePush 运行状态需要从 Logs 中获取, iOS 需要安装文档提示开启 Logs:

https://github.com/Microsoft/react-native-code-push#debugging--troubleshooting

Android 查看 Logs: `adb logcat`.
iOS 查看 Logs, 模拟器可以在 Safari 的 Develop 菜单找到入口.
打印的是全部 log, CodePush 相关的可以通过 `[CodePush]` 标识找到.

从 `0.12.0-beta` 开始, 可以通过 debug 命令查看 log:

```bash
code-push debug android
code-push debug ios
```

真机可以用数据线连接然后通过命令行查看:

```bash
brew install libimobiledevice
idevice_id --list // list available device UDIDs
idevicesyslog -u <device udid>
```

### 求助

官方提供的求助渠道, 包括聊天室(注意时差...)和 GitHub:

* https://discordapp.com/channels/102860784329052160/107883037156466688
* https://github.com/Microsoft/react-native-code-push/issues
