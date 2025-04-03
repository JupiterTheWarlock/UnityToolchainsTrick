# Unity文件和文件夹打开扩展工具

这个示例展示了如何在Unity编辑器中扩展文件和文件夹的打开功能，支持快速访问Unity特定路径和打开Excel文件。

## 功能特点

- 快速打开Unity特定路径
- 支持Excel文件打开
- 跨平台支持
- 集成右键菜单
- 批量文件处理
- 自动格式检查
- 错误提示功能

## 使用方法

1. 在Project视图中右键选择 `Assets/Open Folder/` 可以打开以下路径：
   - `Data Path`: 项目Assets文件夹路径
   - `Persistent Data Path`: 持久化数据路径
   - `Streaming Assets Path`: 流媒体资源路径
   - `Temporary Cache Path`: 临时缓存路径

2. 打开Excel文件：
   - 在Project视图中选择Excel文件
   - 右键选择 `Assets/Open Files/OpenExcel`
   - 支持的格式：xlsx、xls、csv

## 技术细节

- 使用 `Process.Start` 调用系统命令
- 支持Windows和macOS平台
- 提供完整的路径处理API
- 自动处理文件类型检查
- 集成Unity编辑器菜单

## 代码示例

```csharp
// 打开指定文件夹
public static void Execute(string folder)
{
    folder = string.Format("\"{0}\"", folder);
    switch (Application.platform)
    {
        case RuntimePlatform.WindowsEditor:
            Process.Start("Explorer.exe", folder.Replace('/', '\\'));
            break;
        case RuntimePlatform.OSXEditor:
            Process.Start("open", folder);
            break;
    }
}

// 打开Excel文件
[MenuItem("Assets/Open Files/OpenExcel")]
public static void OpenExcel()
{
    string[] suffixs = new[] { "xlsx", "xls", "csv" };
    var objects = Selection.objects;
    foreach (var o in objects)
    {
        string path = AssetDatabase.GetAssetPath(o);
        if (o is TextAsset)
        {
            // 处理Excel文件打开逻辑
        }
    }
}
```

## 实现原理

1. 路径处理
   - 获取Unity特定路径
   - 格式化路径字符串
   - 处理跨平台差异
   - 验证路径有效性

2. 文件处理
   - 检查文件类型
   - 验证文件后缀
   - 处理批量文件
   - 调用系统命令

3. 菜单集成
   - 添加右键菜单项
   - 设置菜单优先级
   - 处理菜单事件
   - 提供操作反馈

## 支持平台

1. Windows
   - 使用Explorer.exe
   - 处理路径分隔符
   - 支持中文路径
   
2. macOS
   - 使用open命令
   - 保持路径格式
   - 处理特殊字符

## 注意事项

- 检查文件路径有效性
- 处理特殊字符路径
- 注意文件类型验证
- 考虑权限问题
- 处理打开失败情况

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 