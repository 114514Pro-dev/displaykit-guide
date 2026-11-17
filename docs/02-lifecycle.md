# 画布作用域、更新与清理

先确定内容由谁看到，再决定画布的生命周期。同一块全局画布上的内容更新会到达所有观察者。个人数据需要为每名玩家创建独立画布。

## 发送范围

| 需求 | 创建与发送 | 后续更新 |
| --- | --- | --- |
| 全服公告或公共倒计时 | 创建一次，调用 `canvas.Spawn()` | 所有观察者看到相同内容，后加入者也会收到 |
| 个人生命值或私有任务 | 每名玩家创建一块，调用 `canvas.Spawn(connectionId)` | 只更新该玩家的画布 |

目标版本也提供按 `ReferenceHub` 发送的重载。按 `Player` 操作的重载要以安装版本的 API 为准。不要修改共享画布上的文本来发送私有信息。

## 修改与显示

```csharp
message.Content = "任务已更新";
panel.Background.Color = Color.cyan;
panel.Size.Width = 320f;

canvas.Hide();
canvas.Show();
```

已发送的画布在属性变化后自动同步，DisplayKit 只传输发生变化的属性。使用 `canvas.Show(connectionId)` 与 `canvas.Hide(connectionId)` 可控制指定观察者的可见性。构建前设置 `DefaultVisibility`，决定新观察者最初看到什么。

按需更新实际变化的值。让文字和尺寸每帧保持相同值只会增加服务端工作。角色状态或数值发生改变时更新对应元素。

## 清理

```csharp
message.Remove(); // 移除单个元素
canvas.Hide();    // 暂时隐藏画布
canvas.Destroy(); // 销毁整块画布
```

插件持有创建的画布。为个人 UI 保存玩家到画布的映射，断线时销毁对应画布，并从映射移除。回合重启和插件停用时销毁仍由插件持有的全局及个人画布，停止驱动更新的协程。清理时核对画布是否已经销毁，避免旧回调继续写入。

接着看[布局与样式](03-layout-and-style.md)。来源为官方 Wiki 的[发送给玩家](https://github.com/northwood-studios/LabAPI/wiki/DisplayKit-SendingToPlayers)、[修改元素](https://github.com/northwood-studios/LabAPI/wiki/DisplayKit-ModifyingElements)和[删除元素](https://github.com/northwood-studios/LabAPI/wiki/DisplayKit-DeletingElements)。
