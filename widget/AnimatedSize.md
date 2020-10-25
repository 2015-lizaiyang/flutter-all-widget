# AnimatedSize

## 介绍

> Animated widget that automatically transitions its size over a given duration whenever the given child's size changes. [...]

## 简介

`AnimatedSize`控件表示一个具有尺寸变化动画的控件

## 构造函数

```dart
const AnimatedSize({
    Key key,
    Widget child,
    this.alignment = Alignment.center,
    this.curve = Curves.linear,
    @required this.duration,
    this.reverseDuration,
    @required this.vsync,
})
```

- child：子控件
- alignment：子控件的对齐方式
- curve：动画的插值器
- duration：动画的时长
- reverseDuration：翻转动画的时长
- vsync：是否开启垂直同步

## 例子

```dart
class WeWidgetState extends State<WeWidget>
    with SingleTickerProviderStateMixin {
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
        title: Text("day24"),
      ),
      body: _buildColumn(),
    );
  }

  Widget _buildColumn() {
    return Center(
      child: AnimatedSize(
        alignment: Alignment.center,
        curve: Curves.fastOutSlowIn,
        vsync: this,
        duration: Duration(seconds: 1),
        reverseDuration: Duration(seconds: 2),
        child: FlutterLogo(
          style: FlutterLogoStyle.horizontal,
          size: _width,
        ),
      ),
    );
  }
}
```
