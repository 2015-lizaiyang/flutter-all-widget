# AnimatedListState

## 介绍

> The state for a scrolling container that animates items when they are inserted or removed. [...]

## 简介

- `AnimatedListState`控件表示一个具有动画的列表控件
- `AnimatedListState`控件作为`AnimatedList`控件的`key`进行使用，可以控制列表动画和增删操作

2、构造函数

```dart
const AnimatedList({
    Key key,
    @required this.itemBuilder,
    this.initialItemCount = 0,
    this.scrollDirection = Axis.vertical,
    this.reverse = false,
    this.controller,
    this.primary,
    this.physics,
    this.shrinkWrap = false,
    this.padding,
})
```
- itemBuilder：列表条目的构建者
- initialItemCount：列表初始化条目的个数
- scrollDirection：滚动的方向
- reverse：是否翻转
- controller：滚动控制器
- primary：是否当用户点击状态栏时，该视图会滚动到顶部，只适用于iOS，默认支持
- physics：控制用户滚动视图的交互

  - AlwaysScrollableScrollPhysics：列表总是可滚动的
  - PageScrollPhysics：一页一页的列表滑动，一般用于PageView控件用的滑动效果，滑动到末尾会有比较大的弹起
  - ClampingScrollPhysics：滚动时没有回弹效果
  - NeverScrollableScrollPhysics：就算内容超过列表范围也不会滑动
  - BouncingScrollPhysics：不论什么平台都会有回弹效果
  - FixedExtentScrollPhysics：仅滚动到子项而不存在任何偏移，必须与使用FixedExtentScrollController的可滚动对象一起使用
- shrinkWrap：是否根据子widget的总长度来设置ListView的长度
- padding：父控件的内边距

## 例子

通过点击加号随机生成字符串，对列表进行增加操作，通过点击条目的删除图标，对列表进行删除操作

```dart
class WeWidgetState extends State<WeWidget> {
  var data = <String>[];
  var tween = Tween<Offset>(begin: Offset(1, 0), end: Offset(0, 0));
  final animatedKey = GlobalKey<AnimatedListState>();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('day19'),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          var str = Random().nextInt(1000).toString();
          data.add(str);
          var index = data.lastIndexOf(str);
          animatedKey.currentState.insertItem(index);
        },
        child: Icon(Icons.add),
      ),
      body: AnimatedList(
        physics: BouncingScrollPhysics(),
        padding: EdgeInsets.all(12.0),
        scrollDirection: Axis.vertical,
        primary: true,
        reverse: false,
        shrinkWrap: false,
        key: animatedKey,
        initialItemCount: data.length,
        itemBuilder: (context, int index, Animation<double> animation) {
          return animationListItem(data[index], animation);
        },
      ),
    );
  }

  Widget animationListItem(String str, animation) {
    return SlideTransition(
      position: animation.drive(tween),
      child: listItem(str),
    );
  }

  Widget listItem(String str) {
    return ListTile(
      title: Text('$str', style: TextStyle(fontSize: 30)),
      trailing: IconButton(
        icon: Icon(Icons.delete_forever),
        onPressed: () {
          var index = data.indexOf(str);
          data.remove(str);
          animatedKey.currentState.removeItem(
              index, (context, animation) => animationListItem(str, animation));
        },
      ),
    );
  }
}
```
