
动画
----

官方提供 `Animated` 和 `LayoutAnimation`, 主要使用 `Animated` 来编写动画.

### `Animated`

一个例子比如, 通过 `Animated.Value` 初始化一个动画的对象,
通过 `Animated.timing()` 开始操作在对象上做插值,
然后 `Animated.View` 内部使用这个对象(...内部处理了组件的重绘):

```jsx
class FadeInView extends React.Component {
  state: any;

  constructor(props) {
    super(props);
    this.state = {
      fadeAnim: new Animated.Value(0), // opacity 0
    };
  }
  componentDidMount() {
    Animated.timing(       // Uses easing functions
      this.state.fadeAnim, // The value to drive
      {
        toValue: 1,        // Target
        duration: 2000,    // Configuration
      },
    ).start();             // Don't forget start!
  }
  render() {
    return (
      <Animated.View   // Special animatable View
        style={{
          opacity: this.state.fadeAnim,  // Binds
        }}>
        {this.props.children}
      </Animated.View>
    );
  }
}
```

启动动画有几个方法:

```js
Animated.timing
Animated.spring
Animated.decay
```

对动画进行组合的一些方法:

```bash
Animated.sequence
Animated.parallel
Animated.stagger
Animated.delay
```

监听事件作为动画的方法:

```bash
Animated.event
```

动画进行组合的例子(下方链接的文章里抠的仅供参考):

```jsx
componentDidMount() {
    var timing = Animated.timing;
    Animated.sequence([
        Animated.stagger(200, this.state.anim.map(left => {
            return timing(left, {
                toValue: 1,
              });
            }).concat(
                this.state.anim.map(left => {
                    return timing(left, {
                        toValue: 0,
                    });
                })
            )), // 三个view滚到右边再还原，每个动作间隔200ms
            Animated.delay(400), // 延迟400ms，配合sequence使用
            timing(this.state.anim[0], {
                toValue: 1
            }),
            timing(this.state.anim[1], {
                toValue: -1
            }),
            timing(this.state.anim[2], {
                toValue: 0.5
            }),
            Animated.delay(400),
            Animated.parallel(this.state.anim.map((anim) => timing(anim, {
                toValue: 0
            }))) // 同时回到原位置
        ]
    ).start();
}
```

具体需要参考教程:

* http://browniefed.com/react-native-animation-book/
* http://www.alloyteam.com/2016/01/reactnative-animated/
* http://browniefed.com/blog/react-native-animated-api-basic-example/
* http://blog.huynh.io/2015/08/06/react-native-animations/

### `LayoutAnimation`

大致上是在 iOS 平台自动对 `setState` 的性能进行处理, 直接生成渐变.

(需要补充)

https://medium.com/@Jpoliachik/react-native-s-layoutanimation-is-awesome-4a4d317afd3e
