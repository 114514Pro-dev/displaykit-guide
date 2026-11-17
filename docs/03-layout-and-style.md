# 布局与样式

DisplayKit 的布局使用 Unity UI Toolkit 风格的属性。先决定容器流向，再设置对齐、尺寸与边距。需要覆盖在固定位置的元素时再使用绝对定位。

## 流式布局

```csharp
DisplayElement row = canvas.AddElement();
row.Flex.Direction = FlexDirection.Row;
row.Align.AlignItems = Align.Center;
row.Align.JustifyContent = Justify.SpaceBetween;

row.AddText("目标");
row.AddText("3 / 5");
```

`FlexDirection.Row` 横向排列，`Column` 纵向排列。`JustifyContent` 控制主轴分配，`AlignItems` 控制交叉轴位置。`Flex.Grow` 可让一个子容器占据剩余空间。

## 尺寸与位置

```csharp
panel.Size.Width = 300f;
panel.Size.Height = Length.Percent(40f);
panel.Position.Position = Position.Absolute;
panel.Position.Top = 80f;
panel.Position.Right = 40f;
```

普通数值作为像素长度。百分比尺寸以父元素为参照。绝对定位时设置 `Position.Position` 和对应边距。屏幕分辨率变化时，要在不同宽高比下检查边缘区域和文本换行。

## 层次与文本

```csharp
panel.Background.Color = new Color(0f, 0f, 0f, 0.7f);
panel.Border.Color = Color.cyan;
panel.Border.Width = 2f;
panel.Border.Radius = 8f;
panel.Spacing.PaddingTop = 12f;
panel.Spacing.PaddingLeft = 16f;

DisplayText title = panel.AddText("行动指令");
title.Text.Color = Color.white;
title.Text.FontSize = 24f;
```

背景透明度、边框和留白共同决定可读性。字体、对齐、阴影、变换和更多字段见[官方样式属性表](https://github.com/northwood-studios/LabAPI/wiki/DisplayKit-StyleProperties)。具体枚举、字体及客户端显示效果以目标版本为准。

继续看[常见界面方案](04-patterns.md)。来源为官方 Wiki 的[创建元素](https://github.com/northwood-studios/LabAPI/wiki/DisplayKit-CreatingElements)和[样式属性](https://github.com/northwood-studios/LabAPI/wiki/DisplayKit-StyleProperties)。
