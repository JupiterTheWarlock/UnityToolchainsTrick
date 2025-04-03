# Unity编辑器按钮窗口示例

这个示例展示了如何在Unity编辑器中创建一个带有可点击按钮的自定义窗口。

## 功能特点

- 创建自定义编辑器窗口
- 在窗口中显示可点击的按钮
- 使用Unity内置图标作为按钮图标
- 点击按钮后打开外部URL链接

## 使用方法

1. 在Unity编辑器菜单中选择 `Tools -> ShowButtonWindow`
2. 窗口会显示一个带有Unity编辑器图标的按钮
3. 点击按钮将打开百度主页

## 技术细节

- 使用 `EditorWindow` 类创建自定义窗口
- 通过 `EditorGUIUtility.IconContent` 获取Unity内置图标
- 使用 `MenuItem` 特性在Unity菜单中添加入口
- 设置窗口最小尺寸为 300x200

## 文件说明

- `Example_11_ShowButtonEditorWindow.cs`: 主要实现文件，包含窗口类和按钮逻辑
- `QQ截图20210419154434.png`: 示例截图

## 代码示例

```csharp
[MenuItem("Tools/ShowButtonWindow", priority = 11)]
private static void PopUp()
{
    _window = GetWindow<Example_11_ShowButtonEditorWindow>();
    _window.minSize = MIN_SIZE;
    _window.Show();
}
```

## 注意事项

- 窗口大小已设置最小限制，以确保按钮正常显示
- 按钮使用了Unity内置的BuildSettings.Editor图标

## 开发环境要求

- Unity 2019.1或更高版本
- .NET Framework 4.x 