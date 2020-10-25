# Hero

## 介绍

> A widget that marks its child as being a candidate for hero animations. [...]

## 简介

Hero控件属于Android里的共享元素动画，它可以在不同的页面跳转时，复用同一个控件，且带有动画效果

## 构造函数

```dart
const Hero({
    Key key,
    @required this.tag,
    this.createRectTween,
    this.flightShuttleBuilder,
    this.placeholderBuilder,
    this.transitionOnUserGestures = false,
    @required this.child,
})
```

- tag：共享元素的Tag
- createRectTween：定义目标从起点到终点的边界变化动画
- lightShuttleBuilder：自定义跳转时候运动轨迹动画的控件
- placeholderBuilder：自定义跳转时候的占位符
- transitionOnUserGestures：支持iOS的返回滑动手势
- child：子控件

## 例子

设置点击加号图标跳转到太阳图标的页面，在跳转的时候用相机快门图标做轨迹运动，同时会有加载占位符

```dart
class WeWidgetState extends State<WeWidget> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("day8"),
      ),
      body: GestureDetector(
        child: _buildColumn(),
        onTap: () {
          _pushToNewPage();
        },
      ),
    );
  }

  Widget _buildColumn() {
    return Hero(
      tag: "mmm",
      transitionOnUserGestures: true,
      placeholderBuilder: (context, size, widget) {
        return CircularProgressIndicator();
      },
      flightShuttleBuilder: (flightContext, animation, flightDirection,
          fromHeroContext, toHeroContext) {
        return Icon(
          Icons.camera,
          size: 70.0,
        );
      },
      child: Icon(
        Icons.add,
        size: 70.0,
      ),
    );
  }

  void _pushToNewPage() {
    Navigator.of(context).push(
      MaterialPageRoute(builder: (context) {
        return Scaffold(
            appBar: AppBar(
              title: Text('Hero'),
            ),
            body: Center(
              child: Hero(
                tag: "mmm",
                child: Icon(
                  Icons.wb_sunny,
                  size: 70.0,
                ),
              ),
            ));
      }),
    );
  }
}
```