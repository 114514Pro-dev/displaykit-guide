# 入门与第一块画布

DisplayKit 在服务端创建 UI 树，并将画布及变更同步给客户端。根节点是 `DisplayCanvas`，`DisplayElement` 用于容器，`DisplayText` 用于文字。先完成树的创建和样式设置，再调用 `Spawn`。

项目引用 DisplayKit 及其目标服务器所需程序集。使用部分样式类型时，还要引用 `UnityEngine.UIElementsModule` 和 `UnityEngine.TextRenderingModule`。先核对插件的现有引用和目标版本。

## 最小例子

```csharp
using DisplayKit.Elements;
using UnityEngine;
using UnityEngine.UIElements;

DisplayCanvas canvas = DisplayCanvas.Create();
canvas.DefaultVisibility = CanvasVisibility.Visible;
canvas.SortOrder = 100;
canvas.Align.AlignItems = Align.Center;
canvas.Align.JustifyContent = Justify.Center;

DisplayText message = canvas.AddText("欢迎来到服务器");
message.Text.Color = Color.white;
message.Text.FontSize = 32f;
message.Text.Align = TextAnchor.MiddleCenter;

canvas.Spawn();
```

`Spawn()` 将同一画布送给当前玩家，并使之后加入的玩家也获得它。数值更高的 `SortOrder` 位于更上层。这个例子创建的是共享内容。若文字要因玩家而异，使用下一章的单人画布。

## 加入容器

```csharp
DisplayElement panel = canvas.AddElement();
panel.Flex.Direction = FlexDirection.Column;
panel.Align.AlignItems = Align.Center;
panel.Background.Color = new Color(0f, 0f, 0f, 0.75f);
panel.Spacing.PaddingLeft = 20f;
panel.Spacing.PaddingRight = 20f;
panel.AddText("当前任务");
```

父元素控制子元素的排列。把相关文字、图形和区域放在同一个容器，后续可以统一调整位置、背景与可见性。

继续阅读[画布作用域、更新与清理](02-lifecycle.md)。来源为官方 Wiki 的[入门](https://github.com/northwood-studios/LabAPI/wiki/DisplayKit)与[创建元素](https://github.com/northwood-studios/LabAPI/wiki/DisplayKit-CreatingElements)。
