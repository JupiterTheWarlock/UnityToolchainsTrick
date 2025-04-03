# Unity多窗口层级管理系统

这个示例展示了如何在Unity编辑器中实现一个完整的多窗口管理系统，用于控制和管理多个编辑器窗口的层级关系。

## 功能特点

- 统一管理多个编辑器窗口
- 支持窗口优先级控制
- 自动管理窗口焦点
- 支持重复弹出窗口的管理
- 提供完整的窗口生命周期管理
- 窗口列表自动排序

## 使用方法

1. 创建新窗口时继承 `EditorWindowBase` 基类
2. 使用 `EditorWindowMgr` 类管理窗口：
   - `AddEditorWindow`: 添加普通窗口
   - `AddRepeateWindow`: 添加可重复弹出的窗口
   - `RemoveEditorWindow`: 移除窗口
   - `FoucusWindow`: 聚焦最上层窗口
   - `DestoryAllWindow`: 关闭所有窗口

## 技术细节

- 使用优先级系统管理窗口层级
- 维护窗口缓存列表
- 自动处理窗口焦点
- 支持窗口的批量管理
- 提供窗口排序机制

## 文件说明

- `EditorWindowMgr.cs`: 窗口管理器核心实现
- `EditorWindowBase.cs`: 编辑器窗口基类
- `MainWindow.cs`: 主窗口示例实现
- `RepeateWindow.cs`: 可重复弹出窗口示例

## 代码示例

```csharp
// 添加一个重复弹出的窗口
public static void AddRepeateWindow(EditorWindowBase window)
{
    repeateWindowPriroty++;
    window.Priority = repeateWindowPriroty;
    AddEditorWindow(window);
}

// 管理器强制刷新Window焦点
public static void FoucusWindow()
{
    if (windowList.Count > 0)
    {
        windowList[windowList.Count - 1].Focus();
    }
}
```

## 注意事项

- 所有自定义窗口都应继承自EditorWindowBase
- 窗口优先级决定其在层级中的位置
- 重复弹出的窗口会自动获得递增的优先级
- 关闭窗口时需要正确调用移除方法
- 建议使用管理器提供的方法而不是直接操作窗口

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 