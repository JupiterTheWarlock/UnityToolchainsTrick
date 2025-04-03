# Unity复合枚举编辑器工具

这个示例展示了如何在Unity编辑器中使用和编辑复合枚举（Flags Enum），实现多选枚举值的编辑和检查功能。

## 功能特点

- 支持复合枚举编辑
- 使用位运算实现多选
- 可视化枚举选择界面
- 支持枚举值检查
- 自定义窗口布局
- 实时状态更新

## 使用方法

1. 在Unity编辑器菜单中选择 `Tools -> 复合枚举`
2. 在打开的窗口中：
   - 使用下拉框选择多个枚举值
   - 点击"是否包含Red"按钮检查状态
   - 在控制台查看检查结果

## 技术细节

- 使用 `[System.Flags]` 特性标记复合枚举
- 通过位运算实现枚举值组合
- 使用 `EditorGUILayout.EnumFlagsField` 创建多选界面
- 支持枚举值的位运算检查
- 提供完整的枚举操作API

## 代码示例

```csharp
[System.Flags]
public enum CompositeEnum
{
    Red = 1 << 1,
    Blue = 1 << 2,
    Yellow = 1 << 3,
    All = Red | Blue | Yellow,
}

private void OnGUI()
{
    _compositeEnum = (CompositeEnum)EditorGUILayout.EnumFlagsField(
        "复合枚举", _compositeEnum);
    if (GUILayout.Button("是否包含Red"))
    {
        var contain = (_compositeEnum & CompositeEnum.Red) > 0;
        Debug.Log($"是否包含Red？{contain}");
    }
}
```

## 实现原理

1. 定义带有Flags特性的枚举类型
2. 使用位移运算定义枚举值
3. 通过位运算组合多个枚举值
4. 使用Unity编辑器GUI显示多选界面
5. 通过位与运算检查枚举值状态

## 注意事项

- 枚举值必须是2的幂次方
- 注意枚举值的位数限制
- 合理设计枚举值的组合关系
- 注意处理All等组合值
- 建议添加值范围检查

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 