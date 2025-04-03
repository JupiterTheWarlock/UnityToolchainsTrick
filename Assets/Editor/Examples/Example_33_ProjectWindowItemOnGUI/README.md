# Unity项目窗口扩展工具

这个示例展示了如何扩展Unity的项目窗口，添加文件扩展名显示和文件容量信息等功能。

## 功能特点

- 显示文件扩展名
- 显示文件容量信息
- 支持大图标和列表视图
- 可通过快捷键触发显示
- 支持开关功能控制
- 自动刷新项目窗口
- 支持多种视图模式

## 使用方法

1. 在Unity编辑器菜单中选择：
   - `Tools -> ShowFileExtensions -> OpenShowFileExtensions` 开启扩展名显示
   - `Tools -> ShowFileExtensions -> CloseShowFileExtensions` 关闭扩展名显示
2. 在项目窗口中：
   - 按住Alt键查看文件扩展名
   - 自动显示文件容量信息
   - 支持不同视图模式下的显示

## 技术细节

- 使用 `InitializeOnLoad` 特性实现自动初始化
- 通过 `EditorApplication.projectWindowItemOnGUI` 扩展项目窗口
- 使用反射获取项目窗口信息
- 支持自定义GUI绘制
- 提供完整的窗口操作API

## 代码示例

```csharp
[InitializeOnLoad]
public static class ShowFileExtensions
{
    static ShowFileExtensions()
    {
        EditorApplication.projectWindowItemOnGUI += ProjectWindowItemOnGUI;
    }

    private static void ProjectWindowItemOnGUI(string guid, Rect rect)
    {
        if (ShowFileExtensionsEnable && Event.current.alt)
        {
            string assetPath = AssetDatabase.GUIDToAssetPath(guid);
            string extension = Path.GetExtension(assetPath);
            GUI.Label(rect, extension, EditorStyles.boldLabel);
            EditorApplication.RepaintProjectWindow();
        }
    }
}
```

## 实现原理

1. 注册项目窗口GUI事件回调
2. 检测文件类型和视图模式
3. 计算显示位置和样式
4. 绘制扩展信息
5. 自动刷新窗口显示

## 注意事项

- 注意处理不同视图模式下的显示
- 合理使用反射获取窗口信息
- 避免频繁刷新影响性能
- 处理特殊文件类型的显示
- 注意GUI绘制的性能优化

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 