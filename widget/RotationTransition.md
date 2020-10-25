# RotationTransition

## 介绍

> Animates the rotation of a widget. [...]

## 简介

`RotationTransition`表示一个旋转动画，可以通过控制器去控制动画旋转值的改变，从而控制动画的旋转

## 构造函数


```dart
RotationTransition({
    Key key,
    this.turns,
    this.alignment,
    Widget child,
})
```

- turns：动画旋转值的变化，注意这里的类型是`Animation<num>`
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
      child: RotationTransition(
        //旋转的锚定坐标
        alignment: Alignment.center,
        turns: animation,
        child: this.child,
      ),
    );
  }
}
```