# Unity中文字符查找工具

这个示例展示了如何在Unity项目中查找和统计代码文件中的中文字符，支持批量扫描和导出结果。

## 功能特点

- 中文字符检测
- 批量文件扫描
- CSV格式导出
- 进度显示
- 注释过滤
- 路径自定义
- 实时处理反馈

## 使用方法

1. 打开工具窗口：
   - 在Unity菜单中选择 `Tools -> 查找代码中文`
   - 设置要扫描的代码路径（默认为"/Scripts"）

2. 执行扫描：
   - 点击"开始遍历项目"按钮
   - 等待扫描完成
   - 结果将保存在 `Temp/ChineseTexts.csv` 文件中

## 技术细节

- 使用正则表达式检测中文
- 支持多种文件编码
- 分帧处理大量文件
- 自动过滤特定文件
- 提供完整的扫描API

## 代码示例

```csharp
// 检测中文字符
private bool HasChinese(string str)
{
    return Regex.IsMatch(str, @"[\u4e00-\u9fa5]");
}

// 遍历文件系统
private void GetAllFIle(DirectoryInfo dir)
{
    FileInfo[] allFile = dir.GetFiles();
    foreach (FileInfo fi in allFile)
    {
        if (fi.FullName.IndexOf(".meta") == -1 && fi.FullName.IndexOf(".cs") != -1)
        {
            csList.Add(fi.DirectoryName + "/" + fi.Name);
        }
    }
    DirectoryInfo[] allDir = dir.GetDirectories();
    foreach (DirectoryInfo d in allDir)
    {
        GetAllFIle(d);
    }
}

// 导出中文字符信息
private void printChinese(string path)
{
    string[] fileContents = File.ReadAllLines(path, Encoding.Default);
    // 处理文件内容并导出到CSV
    // ...
}
```

## 实现原理

1. 文件扫描
   - 递归遍历目录
   - 过滤文件类型
   - 收集文件路径
   - 分批处理文件

2. 中文检测
   - 正则表达式匹配
   - 字符串解析
   - 注释识别
   - 上下文分析

3. 结果导出
   - CSV格式组织
   - 文件路径记录
   - 行号定位
   - 上下文保存

## 应用场景

1. 国际化准备
   - 查找硬编码文本
   - 收集待翻译内容
   - 统计中文使用
   
2. 代码审查
   - 检查命名规范
   - 查找注释文本
   - 统计代码质量
   
3. 资源管理
   - 文本资源提取
   - 字符串管理
   - 本地化支持

## 注意事项

- 设置正确的扫描路径
- 注意大文件处理性能
- 避免重复扫描
- 正确处理文件编码
- 定期清理临时文件

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 