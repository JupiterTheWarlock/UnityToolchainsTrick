# Unity链接字段工具

这个示例展示了如何在Unity编辑器中创建可点击的链接字段，支持文件链接和URL链接。

## 功能特点

- 支持文件链接
- 支持URL链接
- 自定义链接样式
- 支持布局和绝对定位
- 自动处理链接点击
- 支持文件定位
- 支持浏览器打开

## 使用方法

1. 在Unity编辑器菜单中选择 `Tools -> LinkDemoWindow`
2. 在打开的窗口中：
   - 点击文件链接自动定位到文件
   - 点击URL链接在浏览器中打开
   - 支持不同布局方式的链接显示

## 技术细节

- 扩展 `EditorGUILayout` 实现布局链接
- 扩展 `GUI` 实现绝对定位链接
- 使用 `EditorGUIUtility` 处理鼠标事件
- 支持自定义链接样式和颜色
- 提供完整的链接处理API

## 代码示例

```csharp
private void OnGUI()
{
    // 使用布局方式
    EditorGUILayoutExtension.LinkFileLabelField(
        "EditorGUILayoutExtension.cs", 
        "Assets/Editor/.../EditorGUILayoutExtension.cs");
    
    EditorGUILayoutExtension.LinkUrlLabelField(
        "UnityToolchainsTrick仓库",
        "https://github.com/XINCGer/UnityToolchainsTrick");
    
    // 使用绝对定位
    GUIExtension.LinkFileLabelField(
        new Rect(200,40,120,16), 
        "EditorGUIExtension.cs",
        "Assets/Editor/.../EditorGUIExtension.cs");
}
```

## 实现原理

1. 创建自定义链接样式
2. 检测鼠标点击事件
3. 处理链接点击响应
4. 打开文件或URL
5. 自动处理不同类型链接

## 链接类型

1. 文件链接
   - 支持项目内文件定位
   - 自动高亮显示文件
   - 处理文件不存在情况
   
2. URL链接
   - 支持外部网址打开
   - 自动使用默认浏览器
   - 处理无效URL情况

## 注意事项

- 确保文件路径正确
- 验证URL的有效性
- 注意链接样式的一致性
- 处理链接点击的异常
- 考虑不同平台的兼容性

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 