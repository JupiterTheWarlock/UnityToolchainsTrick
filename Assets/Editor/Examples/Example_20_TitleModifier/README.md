# Unity编辑器标题修改工具

这个示例展示了如何通过反射机制修改Unity编辑器窗口的标题，实现自定义标题信息的显示。

## 功能特点

- 自动修改Unity编辑器主窗口标题
- 支持异步延迟加载
- 使用反射机制访问Unity内部API
- 可自定义标题内容
- 编辑器启动时自动执行

## 使用方法

1. 将脚本添加到项目中
2. 编辑器启动时会自动执行
3. 默认会在原有标题后添加"【分支】：release"
4. 可以通过修改 `UpdateWindowTitle` 方法自定义标题内容

## 技术细节

- 使用 `InitializeOnLoadMethod` 特性实现编辑器启动时初始化
- 通过反射获取和修改Unity内部的标题描述器
- 使用异步延迟确保标题修改的稳定性
- 支持动态更新标题内容

## 文件说明

- `TitleModifier.cs`: 主要实现文件，包含标题修改的核心逻辑

## 代码示例

```csharp
[InitializeOnLoadMethod]
private static void Init()
{
    ModifyTitleAsync();
}

private static void UpdateWindowTitle(object desc)
{
    var fieldInfo = typeof(EditorApplication).Assembly.GetTypes()
        .First(x => x.FullName == "UnityEditor.ApplicationTitleDescriptor")
        .GetField("title", BindingFlags.Instance | BindingFlags.Public);
    var str = fieldInfo.GetValue(desc) as string;
    fieldInfo.SetValue(desc, str + "【分支】：release");
}
```

## 注意事项

- 使用反射可能受Unity版本更新影响
- 建议设置适当的延迟时间确保稳定性
- 避免频繁修改标题以防止性能问题
- 自定义标题内容时注意长度适中
- 确保标题信息对开发有实际帮助

## 开发环境要求

- Unity 2019.1或更高版本
- .NET Framework 4.x 