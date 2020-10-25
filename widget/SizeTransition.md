# SizeTransition

## 介绍

> Animates its own size and clips and aligns its child. [...]

## 简介

`SizeTransition`表示一个尺寸动画，可以通过控制器去控制动画尺寸值的改变，从而控制动画的尺寸

## 构造函数

```dart
SizeTransition({
    Key key,
    this.sizeFactor,
    this.axis,
    this.axisAlignment,
    Widget child,
})

```

- sizeFactor：动画属性值的变化，注意这里的类型是Animation<num>
- axis：表示动画出现的方式

  - Axis.vertical：垂直方向
  - Axis.horizontal：横轴方向

- axisAlignment：表示动画出现的原始位置偏移量，如果是在垂直方向指的是y，如果是横轴方向指的是x
- child：子控件

## 例子

```dart
class AnimatorTransition extends StatelessWidget {
  final Widget child;
  final Animation<num> animation;
  final Axis axis;

  AnimatorTransition({this.child, this.animation, this.axis = Axis.vertical});

  @override
  Widget build(BuildContext context) {
    return Center(
      child: SizeTransition(
        axisAlignment: 2.0,
        axis: axis,
        sizeFactor: animation,
        child: this.child,
      ),
    );
  }
}
```