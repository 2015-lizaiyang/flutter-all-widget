# FadeTransition

## 介绍

> Animates the opacity of a widget. [...]

## 简介

`FadeTransition`表示一个透明度动画，可以通过控制器去控制动画透明度值的改变，从而控制动画的透明度

## 构造函数

```dart
FadeTransition({
    Key key,
    this.opacity,
    this.alwaysIncludeSemantics,
    Widget child,
})
```

- opacity：动画属性值的变化，注意这里的类型是`Animation<num>`
- alwaysIncludeSemantics：是否包含子语义而不管不透明度
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
      child: FadeTransition(
        //是否包含子语义而不管不透明度
        alwaysIncludeSemantics: false,
        opacity: animation,
        child: this.child,
      ),
    );
  }
}
```