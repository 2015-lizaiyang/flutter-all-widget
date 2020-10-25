# AnimatedOpacity

## 介绍

> Animated version of Opacity which automatically transitions the child's opacity over a given duration whenever the given opacity changes. [...]

## 简介

`AnimatedOpacity`控件表示一个具有透明度变化的动画控件

## 构造函数

```dart
const AnimatedOpacity({
    Key key,
    this.child,
    @required this.opacity,
    Curve curve = Curves.linear,
    @required Duration duration,
})
```

- child：子控件
- opacity：透明度动画变化值
- curve：动画的插值器
- duration：动画的时长

## 例子

通过定时器改变透明度的大小


```dart

class WeWidgetState extends State<WeWidget> {
  WeWidgetState() {
    Timer.periodic(Duration(milliseconds: 1000), (timer) {
      setState(() {
        switch (time % 2) {
          case 0:
            _opacity = 0.3;
            break;
          case 1:
            _opacity = 1.0;
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
        title: Text("day21"),
      ),
      body: _buildColumn(),
    );
  }

  Widget _buildColumn() {
    return Center(
      child: AnimatedOpacity(
        curve: Curves.fastOutSlowIn,
        opacity: _opacity,
        duration: Duration(seconds: 1),
        child: FlutterLogo(
          style: FlutterLogoStyle.horizontal,
          size: 200,
        ),
      ),
    );
  }
}

```