
界面布局
----

采用标签声明界面元素, 类似 React. 界面布局系统采用 Flexbox 加上绝对定位, 和 Web 开发体验大体一致.

### 盒子模型

和 Web 一样, 可以通过 `margin`, `border`, `padding` 来控制布局跟盒子样式.

可以设置 `backgroundColor`, 然而没有 `backgoundImage` 属性, 需要通过 `Image` 元素组合(参考 http://stackoverflow.com/q/29322973/883571 ).

### Flexbox

Flexbox 和 Web 基本一致, 主要的区别是默认 `flexDirection: column`.
Demo 当中布思路基本上和 Web 端布局一致.

教程 http://www.ruanyifeng.com/blog/2015/07/flex-examples.html

### 默认样式

https://github.com/facebook/css-layout#default-values

```css
div, span {
  box-sizing: border-box;
  position: relative;

  display: flex;
  flex-direction: column;
  align-items: stretch;
  flex-shrink: 0;
  align-content: flex-start;

  border: 0 solid black;
  margin: 0;
  padding: 0;
  min-width: 0;
}
```

### 绝对定位

支持 `position: absolute`, 默认根据父节点定位, 不需要在外层元素声明 `position: relative`.

不支持 `position: fixed`, 不支持 `zIndex`, 如果有绝对定位的元素, 需要通过组件顺序控制遮盖关系.

### 图片显示

图片必须使用具体大小, 不能使用百分比的写法, 自动伸缩的图片可以借助 Flexbox 配合 `resizeMode` 使用.

参考 http://wiki.jikexueyuan.com/project/react-native/image.html

### 文字居中

水平方向 `textAlign: center`, 垂直方向建议使用 Flexbox 控制.
`fontSize` 和 `lineHeight` 控制不清晰, Demo 开发过程中出现过垂直居中平台样式差异.

### `scrollView`

可以通过属性控制水平竖直方向. `.scrollTo` API 调用能够设置是否使用动画.

```flow
scrollTo(options: {x: number = 0; y: number = 0; animated: boolean = true})
// or
scrollTo(y: number | { x?: number, y?: number, animated?: boolean }, x: number, animated: boolean)
```

注意平台差异, iOS 中可以设置滚动的值超出限定的区域, Android 不可以.

### `ListView`

基于 `scrollView` 封装的, 继承了全部属性. 超出可视区域的元素不会立即渲染.

注意平台差异, 直接滚动到下方, iOS 中直接滚动到像素位置, Android 滚动到已有内容底部.

Sticky Header 只在 iOS 中生效.

### 点击区域

React Native 将点击区域封装成了 `TouchableHighlight` 元素.
其他元素没有 `onPress` 或者 `onClick` 事件.
