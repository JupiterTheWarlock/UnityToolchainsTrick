# Unity编辑器箭头线绘制示例 (Draw Arrow Line Example)

这个示例展示了如何在Unity编辑器窗口中绘制带箭头的线条。通过这个示例，你可以学习到如何使用Unity的Handles系统在编辑器窗口中进行自定义绘制。

## 功能特点

- 在编辑器窗口中绘制带箭头的直线
- 支持自定义线条颜色
- 支持自定义线条起点和终点
- 展示了坐标轴的绘制方式
- 使用Handles.BeginGUI和Handles.EndGUI进行绘制

## 使用方法

1. 在Unity编辑器中，通过菜单 `Tools > 在窗口上绘制一条带有箭头的线` 打开示例窗口
2. 窗口中会显示两条带箭头的白色线条：
   - X轴方向的箭头线
   - Y轴方向的箭头线
3. 每个箭头线末端都有对应的轴向标签

## 技术说明

- 使用 `EditorWindow` 创建自定义编辑器窗口
- 使用 `Handles.DrawAAPolyLine` 绘制抗锯齿线条
- 通过数学计算实现箭头的绘制
- 使用 `GUI.Label` 添加文本标签
- 展示了如何在编辑器GUI中进行自定义绘制

## 文件说明

- `DrawArrowWindow.cs`: 实现箭头线绘制的主要代码文件

## 代码示例

```csharp
// 绘制带箭头的线条
private void DrawArrow(Vector2 from, Vector2 to, Color color)
{
    Handles.BeginGUI();
    Handles.color = color;
    // 绘制主线
    Handles.DrawAAPolyLine(3, from, to);
    // 计算并绘制箭头
    Vector2 v0 = from - to;
    v0 *= 10 / v0.magnitude;
    Vector2 v1 = new Vector2(v0.x * 0.866f - v0.y * 0.5f, v0.x * 0.5f + v0.y * 0.866f);
    Vector2 v2 = new Vector2(v0.x * 0.866f + v0.y * 0.5f, v0.x * -0.5f + v0.y * 0.866f);
    Handles.DrawAAPolyLine(3, to + v1, to, to + v2);
    Handles.EndGUI();
}
```

## 注意事项

- 此示例仅在Unity编辑器中可用
- 窗口大小固定为300x200像素
- 箭头大小和线条粗细可以通过代码调整
- 绘制操作需要在OnGUI中进行

## 开发环境

- Unity 2019.4 或更高版本
- 需要在Editor文件夹下使用 