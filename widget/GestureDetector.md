# GestureDetector

## 介绍

> A widget that detects gestures. [...]

## 简介

`GestureDetector`是Flutter的手势检测器，它会尝试识别与其非null的回调相对应的手势。如果此Widget组件具有子控件，那么它的大小调整行为将遵从该子控件件。如果它没有子控件，那么它将变大以适合父控件。

默认情况下，带有不可见子控件的手势检测器会忽略触摸；可以通过行为控制此逻辑。`GestureDetector`还监听可访问性事件，并将其映射到callback回调。若要忽略可访问性事件，请将ExcludeFromSemantics设置为true。
Flutter中的手势系统有两个独立的层。第一层为原始指针`(pointer)`事件，它描述了屏幕上指针（例如，触摸、鼠标和触控笔）的位置和移动。 第二层为手势，描述由一个或多个指针移动组成的语义动作，如拖拽、缩放、双击、长按等。

