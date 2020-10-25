# SlideTransition

## 介绍

> Animates the position of a widget relative to its normal position. [...]

## 简介

`SlideTransition`表示一个平移动画，可以通过控制器去控制动画尺寸值的改变，从而控制动画的平移位置

## 构造函数

```dart
SlideTransition({
    Key key,
    this.position,
    this.transformHitTests,
    this.textDirection,
    Widget child,
})

```

- position：动画属性值的变化，注意这里的类型是Animation<Offset>
- transformHitTests：表示点击事件是否落在动画后的控件上
- textDirection：表示动画执行的位置关系

  - TextDirection.rtl：左到右
  - TextDirection.ltr：右到左

- child：子控件

## 例子

```dart
class AnimatorTransition extends StatelessWidget {
  final Widget child;
  final Animation<Offset> animation;

  AnimatorTransition({this.child, this.animation});

  @override
  Widget build(BuildContext context) {
    return Center(
      child: SlideTransition(
        transformHitTests: true,
        textDirection: TextDirection.rtl,
        position: animation,
        child: this.child,
      ),
    );
  }
}
```