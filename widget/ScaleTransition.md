# ScaleTransition

## 介绍

> Animates the scale of a transformed widget. [...]

## 简介

`ScaleTransition`表示一个缩放动画，可以通过控制器去控制动画缩放值的改变，从而控制动画的缩放

## 构造函数

``` dart
ScaleTransition({
    Key key,
    this.scale,
    this.alignment,
    Widget child,
})
```

- scale：动画属性值的变化，注意这里的类型是Animation<num>
- alignment：旋转的锚定坐标
- child：子控件

## 例子

```dart
class AnimatorTransition extends StatelessWidget {
  final Widget child;
  final Animation<num> animation;

  AnimatorTransition({this.child, this.animation});

  @override
  Widget build(BuildContext context) {
    return Center(
      child: ScaleTransition(
        //缩放的锚定坐标
        alignment: Alignment.topLeft,
        scale: animation,
        child: this.child,
      ),
    );
  }
}
```