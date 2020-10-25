# PositionedTransition

## 介绍

> Animated version of Positioned which takes a specific Animation<RelativeRect> to transition the child's position from a start position to an end position over the lifetime of the animation. [...]

## 简介

`PositionedTransition`表示一个矩形位置的动画，可以通过控制器去控制动画矩形值的改变，从而控制动画的矩形位置

## 构造函数

```dart
PositionedTransition({
    Key key,
    this.rect,
    Widget child,
})
```

- rect：动画属性值的变化，注意这里的类型是`Animation<RelativeRect>`
- child：子控件

## 例子

::: tip
这里需要注意的是`PositionedTransition`的父控件必须是`Stack`
:::

```dart
class AnimatorTransition extends StatelessWidget {
  final Widget child;
  final Animation<RelativeRect> animation;

  AnimatorTransition({this.child, this.animation});

  @override
  Widget build(BuildContext context) {
    //绝对定位的动画实现, 需要Stack包裹
    return Stack(
      children: <Widget>[
        PositionedTransition(
          rect: animation,
          child: this.child,
        ),
      ],
    );
  }
}
```

