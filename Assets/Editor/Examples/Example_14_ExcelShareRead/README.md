# Unity Excel文件读取工具

这个示例展示了如何在Unity编辑器中实现Excel文件的读取功能，包括普通读取和共享读取两种模式。

## 功能特点

- 支持Excel文件的基本读取功能
- 提供共享读取模式，允许多个程序同时访问
- 使用EPPlus库进行Excel文件操作
- 支持按行列遍历Excel内容
- 自动输出读取结果到Unity控制台

## 使用方法

1. 在Unity编辑器菜单中选择：
   - `Tools -> Excel -> NormalRead` 进行普通读取
   - `Tools -> Excel -> ShareRead` 进行共享读取
2. Excel文件应放置在项目的 `Excels` 文件夹中
3. 默认读取文件名为 `Example.xlsx`
4. 读取结果将在Console窗口中显示

## 技术细节

- 使用 `OfficeOpenXml` 库处理Excel文件
- 支持两种文件访问模式：
  - 普通读取：`FileShare.Read`
  - 共享读取：`FileShare.ReadWrite`
- 自动遍历工作表的所有行和列
- 支持不同数据类型的读取和转换

## 文件说明

- `Example_14_ExcelShareRead.cs`: 主要实现文件
- `Libs/`: 包含EPPlus等第三方库

## 代码示例

```csharp
using (ExcelPackage excelPackage = new ExcelPackage(new FileStream(PATH, FileMode.Open, FileAccess.Read, FileShare.ReadWrite)))
{
    var workbook = excelPackage.Workbook.Worksheets[1];
    for (int i = 1; i <= workbook.Dimension.End.Row; i++)
    {
        var key = workbook.GetValue(i, 1);
        for (int j = 2; j <= workbook.Dimension.End.Column; j++)
        {
            var value = workbook.GetValue(i, j) as string;
            Debug.Log($"value{j} : {value}");
        }
    }
}
```

## 注意事项

- 需要提前配置好Excel文件的路径
- 确保Excel文件格式正确且可访问
- 共享读取模式适用于需要同时访问文件的场景
- 建议处理可能的文件访问异常

## 开发环境要求

- Unity 2018.4或更高版本
- EPPlus库
- .NET Framework 4.x 