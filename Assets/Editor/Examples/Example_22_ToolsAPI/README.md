# Unity Tools API示例工具

这个示例展示了如何使用Unity的Tools API来监控和响应场景视图中的工具状态变化。

## 功能特点

- 监控Scene视图工具状态
- 实时显示当前工具类型
- 支持工具切换事件监听
- 提供Tools.current状态查看
- 集成Scene视图GUI事件

## 使用方法

1. 在Unity编辑器菜单中选择 `Tools -> ToolsAPI`
2. 点击窗口中的 "Tools.current" 按钮查看当前工具
3. 在Scene视图中切换不同工具（如移动、旋转、缩放等）
4. 控制台会输出工具状态的变化信息

## 技术细节

- 使用 `EditorWindow` 创建自定义窗口
- 通过 `SceneView.duringSceneGui` 监听场景视图事件
- 使用 `Tools` 类获取工具状态
- 支持实时工具状态更新
- 提供GUI界面交互

## 文件说明

- `ToolsAPI.cs`: 主要实现文件，包含工具状态监控功能

## 代码示例

```csharp
[MenuItem("Tools/ToolsAPI", priority = 22)]
private static void PopUp()
{
    var _window = GetWindow<ToolsAPI>("ToolsAPI");
    SceneView.duringSceneGui -= OnSceneViewGUI;
    SceneView.duringSceneGui += OnSceneViewGUI;
    _window.Show();
}

private static void OnSceneViewGUI(SceneView view)
{
    if (Tools.viewTool != _viewTool)
    {
        Debug.Log("Tools.viewTool:" + Tools.viewTool);
        _viewTool = Tools.viewTool;
    }
}
```

## 可监控的工具状态

- Move Tool (移动工具)
- Rotate Tool (旋转工具)
- Scale Tool (缩放工具)
- Rect Tool (矩形工具)
- Transform Tool (变换工具)
- View Tool (视图工具)
- Custom Tool (自定义工具)

## 注意事项

- 工具状态变化会实时反映在控制台
- 避免在场景视图更新事件中执行耗时操作
- 注意处理工具状态监听的注册和注销
- 确保正确关闭窗口以防止事件泄漏
- 可以扩展功能以响应特定工具的状态变化

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 