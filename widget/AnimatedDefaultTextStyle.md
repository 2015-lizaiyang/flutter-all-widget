# AnimatedDefaultTextStyle

## 介绍

> Animated version of DefaultTextStyle which automatically transitions the default text style (the text style to apply to descendant Text widgets without explicit style) over a given duration whenever the given style changes. [...]

## 简介

- AnimatedDefaultTextStyle控件表示一个具有变化文本样式的动画控件
- AnimatedDefaultTextStyle通过修改组件的style属性，系统将会通过动画的方式自动切换到新的style样式

## 构造函数

```dart
AnimatedDefaultTextStyle({
    Key key,
    @required this.child,
    @required this.style,
    this.textAlign,
    this.softWrap = true,
    this.overflow = TextOverflow.clip,
    this.maxLines,
    Curve curve = Curves.linear,
    @required Duration duration,
    Duration reverseDuration,
})
```

- child：子控件，通常用Text组件
- style：子控件的样式，用于动画变化
- textAlign：如果文本超过1行时，所有换行的字体的对齐方式，可以是左对齐、右对齐
- softWrap：文本是否应该在软换行符处换行，软换行和硬换行是word用法，具体自阅
- overflow：超过文本行数区域的裁剪方式
- maxLines：文本最大行数，默认是1
- curve：动画插值器
- duration：动画播放时长
- reverseDuration：倒退动画播放时长