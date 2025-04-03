# Unity子窗口停靠系统

这个示例展示了如何在Unity编辑器中创建和管理可停靠的子窗口系统，支持通过代码或布局文件控制窗口排列。

## 功能特点

- 创建多个可停靠的子窗口
- 支持两种布局控制方式：
  - 代码控制布局
  - 布局文件控制
- 布局状态的保存和加载
- 自定义窗口排列和组织
- 支持布局持久化

## 使用方法

1. 在Unity编辑器菜单中选择 `Tools -> SubWindowDock`
2. 主窗口和两个子窗口（A和B）将会打开
3. 可以通过以下方式控制布局：
   - 切换"是否通过代码实现布局"选项
   - 点击"加载布局"按钮加载预设布局
   - 点击"保存布局"按钮保存当前布局

## 技术细节

- 使用 `EditorWindow` 系统创建窗口
- 通过 `LayoutUtility` 实现窗口停靠
- 使用 `EditorPrefs` 保存布局偏好
- 支持异步窗口布局操作
- 布局文件使用 `.wlt` 格式

## 文件说明

- `Example_15_MainWidow.cs`: 主窗口实现
- `Example_15_SubWindowA.cs`: 子窗口A实现
- `Example_15_SubWindowB.cs`: 子窗口B实现
- `LayoutUtility.cs`: 布局工具类
- `layout.wlt`: 预设布局文件

## 代码示例

```csharp
// 通过代码设置窗口布局
private async void LoadLayoutByCode()
{
    await Task.Delay(100);
    LayoutUtility.DockEditorWindow(_window, _windowB);
    await Task.Delay(100);
    LayoutUtility.DockEditorWindow(_window, _windowA);
}

// 加载预设布局
if (GUILayout.Button("加载布局"))
{
    LayoutUtility.LoadLayoutFromAsset(PATH);
}
```

## 注意事项

- 窗口布局操作需要适当的延时以确保正确执行
- 布局文件的保存路径需要在Unity项目内
- 布局更改后需要刷新资源数据库
- 建议在布局操作完成后再进行其他操作

## 开发环境要求

- Unity 2019.1或更高版本
- .NET Framework 4.x
- 需要适当的编辑器权限来保存布局文件 