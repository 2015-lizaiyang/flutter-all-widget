# AnimatedCrossFade

## 介绍

> A widget that cross-fades between two given children and animates itself between their sizes. [...]

## 简介

- `AnimatedCrossFade`存放着两个动画的容器，只要切换动画的状态，就能表现出对应的动画效果
- `AnimatedCrossFade`本质就是一个`Stack`分别存放有两个组件和两个动画

## 构造函数

```dart
const AnimatedCrossFade({
    Key key,
    @required this.firstChild,
    @required this.secondChild,
    this.firstCurve = Curves.linear,
    this.secondCurve = Curves.linear,
    this.sizeCurve = Curves.linear,
    this.alignment = Alignment.topCenter,
    @required this.crossFadeState,
    @required this.duration,
    this.layoutBuilder = defaultLayoutBuilder,
})
```

- firstChild：第一个动画元素的控件
- secondChild：第二个动画元素的控件
- firstCurve：第一个动画元素的插值器
- secondCurve：第二个动画元素的插值器
- sizeCurve：动画切换时候的尺寸变化插值器
- alignment：动画在切换到第二个状态的时候，当前alignment的参数会应用在第二个动画元素中
- crossFadeState：动画当前的状态，当状态变化时，动画也会随之切换到对应的元素上
- duration：动画时长
- layoutBuilder：动画布局的构造器，可以构建两个动画元素之间的布局关系

## 例子

通过定时器更改变量的值，让控件切换布局，从而开启动画

```dart
var time = 0;
var _first = true;

class WeWidgetState extends State<WeWidget> {
  WeWidgetState() {
    Timer.periodic(Duration(seconds: 1), (timer) {
      setState(() {
        switch (time % 4) {
          case 0:
            _first = false;
            break;
          case 2:
            _first = true;
            break;
        }
        time++;
      });
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("day7"),
      ),
      body: _buildColumn(),
    );
  }

  Widget _buildColumn() {
    return Column(
      children: <Widget>[
        AnimatedCrossFade(
          //layoutBuilder: ,
          alignment: AlignmentDirectional(0.0, 1.0),
          duration: Duration(seconds: 1),
          firstCurve: Curves.fastOutSlowIn,
          secondCurve: Curves.fastOutSlowIn,
          sizeCurve: Curves.fastOutSlowIn,
          firstChild: FlutterLogo(
            style: FlutterLogoStyle.horizontal,
            size: 100.0,
          ),
          secondChild: FlutterLogo(
            style: FlutterLogoStyle.stacked,
            size: 200.0,
          ),
          crossFadeState:
              _first ? CrossFadeState.showFirst : CrossFadeState.showSecond,
        ),
      ],
    );
  }
}
```
