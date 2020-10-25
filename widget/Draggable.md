# Draggable

## 介绍

> A widget that can be dragged from to a DragTarget. [...]

## 简介

Draggable 是Flutter中的一个可以拖拽到DragTarget的Widget。并且，他可以把自己携带的数据传递给DragTarget。当Draggable被拖动到DragTarget的时候，DragTarget会判断是不是需要接收传递过来的数据，在接收后做相应的状态改变。

## 继承关系

Object -> Diagnosticable -> DiagnosticableTree -> Widget ->StatefulWidget -> Draggable

## 构造函数

```dart
Draggable({Key key, 
 @required Widget child,
 @required Widget feedback,
 T data, 
 Axis axis,
 Widget childWhenDragging,
 Offset feedbackOffset: Offset.zero, 
 DragAnchor dragAnchor: DragAnchor.child, 
 Axis affinity, 
 int maxSimultaneousDrags,
 VoidCallback onDragStarted, 
 DraggableCanceledCallback onDraggableCanceled, 
 DragEndCallback onDragEnd, 
 VoidCallback onDragCompleted, 
 bool ignoringFeedbackSemantics: true }) 
```

[例子连接🔗](https://juejin.im/post/6844903928396513288)