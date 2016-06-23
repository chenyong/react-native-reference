
事件处理
----

事件系统没有冒泡机制, 所以思路要换一换了.

### `onPress`

React Native 中不是每个节点都可以添加事件的, 似乎内部实现比较复杂.
逻辑都封装在了 `TouchableHighlight` 当中, 所有处理点击都用这个或者同类的组件:

```js
TouchableHighlight
TouchableNativeFeedback
TouchableOpacity
TouchableWithoutFeedback
```

### input

`TextInput` 组件有两个事件, `onTextChange` 才是获取内容的. `onChange` 返回事件.

### 定制事件

(需要补充)

http://gold.xitu.io/entry/55fa202960b28497519db23f

http://www.jianshu.com/p/935e5c6a5064
