# Unity动画曲线预览工具

这个示例展示了如何在Unity编辑器中创建动画曲线预览工具，通过反射调用Unity内部API实现曲线的可视化预览。

## 功能特点

- 自定义动画曲线编辑
- 实时曲线预览功能
- 支持曲线可视化显示
- 自定义预览窗口尺寸
- 使用Unity内部API
- 支持颜色自定义

## 使用方法

1. 在Unity编辑器菜单中选择 `Tools -> AnimationCurvePreview`
2. 在打开的窗口中：
   - 使用曲线编辑器调整动画曲线
   - 点击"预览"按钮查看曲线效果
   - 观察曲线的可视化显示

## 技术细节

- 继承 `EditorWindow` 实现自定义窗口
- 使用反射获取Unity内部API
- 通过 `AnimationCurve` 创建动画曲线
- 使用 `Texture2D` 显示曲线预览
- 支持自定义预览区域和尺寸

## 代码示例

```csharp
private void Init()
{
    var type = Type.GetType("UnityEditorInternal.AnimationCurvePreviewCache,UnityEditor");
    _methodInfo = type.GetMethod("GetPreview",
        new[]
        {
            typeof(int), typeof(int), typeof(AnimationCurve), typeof(Color),
            typeof(Color), typeof(Color)
        });
}

private void OnGUI()
{
    _curve = EditorGUILayout.CurveField("调整动画曲线", _curve);
    if (GUILayout.Button("预览"))
    {
        _texture = _methodInfo.Invoke(null,
            new Object[] {200, 200, _curve, Color.green, Color.clear, Color.clear}) 
            as Texture2D;
    }
}
```

## 实现原理

1. 通过反射获取Unity内部的曲线预览功能
2. 创建可编辑的动画曲线界面
3. 调用内部API生成预览纹理
4. 在指定区域绘制预览纹理

## 注意事项

- 使用反射调用内部API可能存在版本兼容性问题
- 注意预览纹理的内存管理
- 合理设置预览窗口的尺寸
- 确保曲线编辑区域足够大
- 建议添加错误处理机制

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 