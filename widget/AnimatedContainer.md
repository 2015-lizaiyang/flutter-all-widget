# AnimatedContainer

## 介绍

> Animated version of Container that gradually changes its values over a period of time. [...]

## 简介

`AnimatedContainer`表示一个动画容器，只要更改容器的值，就能表现出对应的动画效果

## 构造函数

```dart
AnimatedContainer({
    Key key,
    this.alignment,
    this.padding,
    Color color,
    Decoration decoration,
    this.foregroundDecoration,
    double width,
    double height,
    BoxConstraints constraints,
    this.margin,
    this.transform,
    this.child,
    Curve curve = Curves.linear,
    @required Duration duration,
})
```

- alignment

  - `alignment`表示子元素child相对于容器的对其方式
  - child在`AnimatedContainer`中默认位于居中位置
  - 用坐标表示`child`当前的aligament方式，则为(0,0)
  - 用坐标表示`AnimatedContainer`的四个顶点，则为(-1,-1)(-1,1)(1,-1)(1,1)
  - 通过`AlignmentDirectional`控制child在X、Y轴的偏移，

- padding：可以对子元素child进行内边距位置偏移
- color：容器的背景色，通过`decoration`也能设置背景色，两者不可共存
- decoration：容器的边框修饰，通过`color`也能设置背景色，两者不可共存
- foregroundDecoration：容器的前景边框修饰，在这里做边框修饰，则会挡住`decoration`或`color`的颜色
- width：容器的宽度
- height：容器的高度
- constraints：容器的大小约束，可以指定最小宽高和最大宽高，整个容器遵循这个约束
- margin：容器的外边距
- transform：容器的Matrix变换，可以进行矩阵的旋转，缩放，运算等操作
- child：子元素在容器中的位置默认是居中显示
- curve：容器的动画插值器
- duration：容器的动画时长

## 例子

```dart
var time = 0;
var _color = Colors.red[200];
var _borderColor = Colors.transparent;
var _width = 200.0;
var _height = 200.0;
var _borderWidth = 0.0;
var _scaleX = 1.0;
var _scaleY = 1.0;
var _rotate = 0.0;
var _padding = 0.0;
var _margin = 0.0;
var _alignmentY = 0.0;

class WeWidgetState extends State<WeWidget> {
  WeWidgetState() {
    Timer.periodic(Duration(milliseconds: 1000), (timer) {
      setState(() {
        switch (time % 10) {
          case 0:
            _width = 300;
            _height = 100;
            break;
          case 1:
            _width = 100;
            _height = 300;
            _borderWidth = 4.0;
            _borderColor = Colors.brown[200];
            break;
          case 2:
            _borderWidth = 8.0;
            _borderColor = Colors.pink[200];
            _color = Colors.blue[200];
            break;
          case 3:
            _width = 300;
            _height = 300;
            _color = Colors.deepPurple[200];
            break;
          case 4:
            _scaleX = 0.2;
            _scaleY = 0.2;
            break;
          case 5:
            _scaleX = 0.5;
            _scaleY = 0.5;
            _rotate = math.pi / 6;
            break;
          case 6:
            _scaleX = 1.0;
            _scaleY = 1.0;
            _rotate = 0.0;
            _padding = 200.0;
            break;
          case 7:
            _padding = 0.0;
            break;
          case 8:
            _margin = 80.0;
            _alignmentY = 0.5;
            break;
          case 9:
            _margin = 0.0;
            _alignmentY = 0.0;
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
        title: Text("day6"),
      ),
      resizeToAvoidBottomPadding: false,
      body: _buildColumn(),
    );
  }

  Widget _buildColumn() {
    return Column(
      children: <Widget>[
        AnimatedContainer(
          transform: Matrix4.identity().scaled(_scaleX, _scaleY)
            ..rotateZ(_rotate),
          alignment: AlignmentDirectional(0.0, _alignmentY),
          constraints: BoxConstraints(
            minWidth: 0.0,
            minHeight: 0.0,
            maxWidth: 500.0,
            maxHeight: 500.0,
          ),
          margin: EdgeInsets.only(left: _margin),
          padding: EdgeInsets.only(left: _padding),
          width: _width,
          height: _height,
          duration: Duration(milliseconds: 1000),
          curve: Curves.fastOutSlowIn,
          child: Icon(
            Icons.android,
            color: Colors.lightGreenAccent,
            size: 40,
          ),
          foregroundDecoration: BoxDecoration(
            border: Border.all(
              color: _borderColor,
              width: _borderWidth,
            ),
          ),
          //color 和 decoration两者不可共存
          //color: _color,
          decoration: BoxDecoration(
            color: _color,
            borderRadius: BorderRadius.circular(12),
            boxShadow: [
              BoxShadow(
                color: _color,
                offset: Offset(5.0, 5.0),
                blurRadius: 6.0,
              )
            ],
          ),
        ),
      ],
    );
  }
}
```