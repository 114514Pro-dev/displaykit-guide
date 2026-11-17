# 常见界面方案

## 全服公告

建立一块全局画布，初始状态设为 `CanvasVisibility.Hidden`。将标题和正文放入同一容器，`Spawn()` 后在事件发生时更新 `DisplayText.Content` 并调用 `Show()`。公告结束调用 `Hide()`。若期间收到新公告，先取消前一个计时任务，避免旧计时把新内容提前隐藏。

## 个人状态栏

每位玩家有独立画布。创建时把文字和填充条保存为字段。生命值变化时更新文字，并用 `Length.Percent` 更新填充条宽度。角色变化可能要求新建或重新配置内容，断线时销毁对应画布。

## 公共计分板

全局画布适合展示同一份排行榜。玩家加入或离开时重新计算行内容，删除过期行并创建新增行。长列表需要控制刷新频率和元素数量。若玩家各自看到不同分数或权限内容，改用个人画布。

## 实施检查

- 在画布发送前确定它是全局还是个人范围。
- 文本、宽度与颜色只在业务值变化时更新。
- 临时隐藏用 `Hide`，完全结束用 `Destroy`，单个子元素用 `Remove`。
- 在不同分辨率、后加入、断线、回合重启和插件停用时检查实际显示与清理。
- 对玩家展示的文字按服务器的语言要求编写。

更多完整实现见[官方示例](https://github.com/northwood-studios/LabAPI/wiki/DisplayKit-Examples)，API 成员可查[元素参考](https://github.com/northwood-studios/LabAPI/wiki/DisplayKit-ElementReference)。这份教程基于官方 Wiki 快照整理，针对具体版本编写插件时核对程序集。
