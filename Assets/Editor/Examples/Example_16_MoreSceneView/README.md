# Unity多场景视图工具

这个示例展示了如何在Unity编辑器中创建额外的Scene视图窗口，用于多角度查看和编辑场景。

## 功能特点

- 创建新的Scene视图窗口
- 支持多个Scene视图同时存在
- 每个视图可以独立控制视角和显示设置
- 与主Scene视图功能完全相同
- 支持自定义初始化配置

## 使用方法

1. 在Unity编辑器菜单中选择 `Tools -> CreateMoreSceneView`
2. 新的Scene视图窗口将会创建
3. 可以自由移动和停靠新创建的Scene视图
4. 每个视图都可以独立操作和配置

## 技术细节

- 使用 `ScriptableObject.CreateInstance<SceneView>()` 创建新视图
- 支持Scene视图的完整功能集
- 可以通过扩展方法添加自定义初始化逻辑
- 与Unity编辑器原生Scene视图保持一致的操作方式

## 文件说明

- `CreateMoreSceneView.cs`: 主要实现文件，包含创建Scene视图的核心逻辑

## 代码示例

```csharp
[MenuItem("Tools/CreateMoreSceneView", priority = 16)]
private static void PopUp()
{
    var _window = ScriptableObject.CreateInstance<SceneView>();
    _window.Init();
    _window.Show();
}
```

## 注意事项

- 新创建的Scene视图会占用额外的系统资源
- 建议根据实际需求合理使用多个Scene视图
- 可以通过Unity的窗口管理系统自由组织视图布局
- 所有Scene视图都会同步显示场景的变化

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x
- 建议使用性能较好的显示设备 