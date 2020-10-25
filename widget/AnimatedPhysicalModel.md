# AnimatedPhysicalModel

## 介绍

> Animated version of PhysicalModel. [...]

## 简介

`AnimatedPhysicalModel`控件表示一个具有阴影背景动画的控件

## 构造函数

```dart

const AnimatedPhysicalModel({
    Key key,
    @required this.child,
    @required this.shape,
    this.clipBehavior = Clip.none,
    this.borderRadius = BorderRadius.zero,
    @required this.elevation,
    @required this.color,
    this.animateColor = true,
    @required this.shadowColor,
    this.animateShadowColor = true,
    Curve curve = Curves.linear,
    @required Duration duration,
})

```

- child：子控件
- shape：阴影的形状
- clipBehavior：阴影的裁剪方式

  - Clip.none：无模式
  - Clip.hardEdge：裁剪速度稍快，但容易失真，有锯齿
  - Clip.antiAlias：裁剪边缘抗锯齿，使得裁剪更平滑，这种模式裁剪速度比antiAliasWithSaveLayer快，但是比hardEdge慢
  - Clip.antiAliasWithSaveLayer：裁剪后具有抗锯齿特性并分配屏幕缓冲区，所有后续操作在缓冲区进行

- borderRadius：背景的边框
- elevation：阴影颜色值的深度
- color：背景色
- animateColor：背景色是否用动画形式展示
- shadowColor：阴影的动画值
- animateShadowColor：阴影是否用动画形式展示
- curve：动画的插值器
- duration：动画的时长

```dart
Widget _buildColumn() {
  return Center(
    child: AnimatedPhysicalModel(
      curve: Curves.fastOutSlowIn,
      color: Colors.grey.withOpacity(0.2),
      clipBehavior: Clip.antiAliasWithSaveLayer,
      borderRadius: BorderRadius.circular(12.0),
      animateColor: true,
      animateShadowColor: true,
      shape: BoxShape.rectangle,
      shadowColor: _shadowColor,
      elevation: 20.0,
      duration: Duration(seconds: 1),
      child: FlutterLogo(
        style: FlutterLogoStyle.horizontal,
        size: 200,
      ),
    ),
  );
}
```