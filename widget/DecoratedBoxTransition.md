# DecoratedBoxTransition

## 介绍

> Animated version of a DecoratedBox that animates the different properties of its Decoration. [...]

## 简介

`DecoratedBoxTransition`表示一个边框动画，可以通过控制器去控制动画边框值的改变，从而控制动画边框

## 构造函数

```dart
DecoratedBoxTransition({
    Key key,
    this.decoration,           
    this.position,             
    this.child,               
})
```

- decoration：动画属性值的变化，注意这里的类型是`Animation<Decoration>`
- position：动画的控制器
- child：子控件

## 例子

```dart
class AnimatorTransition extends StatelessWidget {
  final Widget child;
  final Animation<Decoration> animation;

  AnimatorTransition({this.child, this.animation});

  @override
  Widget build(BuildContext context) {
    return Center(
      child: DecoratedBoxTransition(
        position: DecorationPosition.background,
        decoration: animation,
        child: Container(
          child: this.child,
        ),
      ),
    );
  }
}
```