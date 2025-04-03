# Unity编辑器首选项扩展示例

这个示例展示了如何在Unity编辑器的首选项(Preferences)窗口中添加自定义设置选项。

## 功能特点

- 在Unity首选项窗口中添加自定义设置页面
- 支持文本配置的保存和加载
- 提供多个功能开关选项：
  - SceneView扩展开关
  - 全局事件检测开关
  - Hierarchy窗口Ctrl+D事件监听开关
- 使用EditorPrefs持久化存储设置

## 使用方法

1. 在Unity编辑器中打开 `Edit -> Preferences`
2. 在左侧列表中找到 `ToolChainsTrick` 选项
3. 可以在右侧面板中进行以下设置：
   - 输入文本配置
   - 切换SceneView扩展功能
   - 开启/关闭全局事件检测
   - 开启/关闭Hierarchy的Ctrl+D事件监听

## 技术细节

- 使用 `SettingsProvider` 在Unity 2019.1及更高版本中创建设置界面
- 兼容旧版本Unity的 `PreferenceItem` 实现
- 通过 `EditorPrefs` 存储和读取设置数据
- 实现即时生效的设置更改

## 文件说明

- `Example_12_PerferenceExtension.cs`: 主要实现文件，包含首选项扩展逻辑
- `QQ截图20210419154551.png`: 示例截图

## 代码示例

```csharp
[SettingsProvider]
private static SettingsProvider ToolChainsTrickSetting()
{
    var provider = new SettingsProvider("Preferences/ToolChainsTrick", SettingsScope.User)
    {
        guiHandler = (string key) => { PreferenceGUI(); },
        keywords = new string[] {"Tool", "Chains", "Trick"},
    };
    return provider;
}
```

## 注意事项

- 设置更改会立即生效并保存
- 不同版本的Unity使用不同的实现方式
- 所有设置值在编辑器重启后会自动加载

## 开发环境要求

- Unity 2019.1或更高版本（推荐，使用SettingsProvider）
- 低版本Unity使用PreferenceItem实现
- .NET Framework 4.x 