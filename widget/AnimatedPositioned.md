# AnimatedPositioned

## 介绍

> Animated version of Positioned which automatically transitions the child's position over a given duration whenever the given position changes. [...]

## 简介

`AnimatedPositioned`控件表示一个具有位置变化动画的控件

## 构造函数

```dart
const AnimatedPositioned({
    Key key,
    @required this.child,
    this.left,
    this.top,
    this.right,
    this.bottom,
    this.width,
    this.height,
    Curve curve = Curves.linear,
    @required Duration duration,
})
```

- child：子控件
- left：左边距离
- top：上边距离
- right：右边距离
- bottom：下边距离
- width：控件的宽度
- height：控件的高度
- curve：动画的插值器
- duration：动画的时长

## 例子

通过改变左上角位置和宽高进行动画播放

```dart
class WeWidgetState extends State<WeWidget> {
  WeWidgetState() {
    Timer.periodic(Duration(milliseconds: 1000), (timer) {
      setState(() {
        switch (time % 2) {
          case 0:
            _width = 100.0;
            break;
          case 1:
            _width = 200.0;
            break;
        }
        time++;
      });
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("day23"),
      ),
      body: _buildColumn(),
    );
  }

  Widget _buildColumn() {
    return Stack(
      children: <Widget>[
        AnimatedPositioned(
          curve: Curves.fastOutSlowIn,
          width: _width,
          height: _width,
          top: _width,
          left: _width,
          duration: Duration(seconds: 1),
          child: FlutterLogo(
            style: FlutterLogoStyle.horizontal,
            size: 200,
          ),
        ),
      ],
    );
  }
}
```