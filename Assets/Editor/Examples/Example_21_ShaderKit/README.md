# Unity Shader变体统计工具

这个示例展示了如何统计Unity项目中所有Shader的变体数量，并生成详细的统计报告。

## 功能特点

- 统计指定目录下所有Shader的变体数量
- 生成CSV格式的统计报告
- 显示进度条提示处理进度
- 支持批量处理多个Shader
- 自动计算总变体数量
- 报告包含时间戳

## 使用方法

1. 在Unity编辑器菜单中选择 `Tools -> 变体统计`
2. 工具会自动处理 `Assets/GameAssets/Shaders` 目录下的所有Shader
3. 生成的报告将保存在项目根目录的 `Shader` 文件夹中
4. 报告文件名格式为 `ShaderVariantCount-yyyy-MM-dd-hh-mm-ss.csv`

## 技术细节

- 使用反射访问Unity的ShaderUtil内部方法
- 通过AssetDatabase API查找和加载Shader资源
- 使用StreamWriter生成CSV格式报告
- 支持EditorUtility进度条显示
- 自动统计总变体数量

## 文件说明

- `ShaderKit.cs`: 主要实现文件，包含Shader变体统计功能

## 代码示例

```csharp
[MenuItem("Tools/变体统计", priority = 21)]
public static void CalcAllShaderVariantCount()
{
    var type = typeof(SceneView).Assembly.GetType("UnityEditor.ShaderUtil");
    var method = type.GetMethod("GetVariantCount",
        BindingFlags.Static | BindingFlags.Public | BindingFlags.NonPublic);
    
    // 处理每个Shader
    foreach (var shader in shaderList)
    {
        var variantCount = method.Invoke(null, new System.Object[] {shader, true});
        sw.WriteLine(path + "," + variantCount.ToString());
        totalCount += int.Parse(variantCount.ToString());
    }
}
```

## 报告格式

```csv
Shader 数量：[总数]
ShaderFile, VariantCount
[Shader路径1], [变体数量1]
[Shader路径2], [变体数量2]
...
Shader Variant Total Amount: [总变体数量]
```

## 注意事项

- 确保指定的Shader目录路径正确
- 大型项目中可能需要较长处理时间
- 建议在非关键时期执行统计
- CSV文件可以用Excel打开查看
- 注意保存统计结果供后续分析

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 