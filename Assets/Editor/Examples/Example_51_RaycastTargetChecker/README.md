# Unity射线检测目标检查工具

这个示例展示了如何创建一个Unity编辑器工具来检查和管理UI元素的射线检测目标（Raycast Target）属性。

## 功能特点

- 射线检测目标显示
- 批量属性修改
- 可视化边界显示
- 场景视图集成
- 实时预览更新
- 撤销/重做支持
- 自定义边框颜色

## 使用方法

1. 打开工具窗口：
   - 在Unity菜单中选择 `Tools -> RaycastTarget Checker`
   - 窗口显示场景中所有UI元素的射线检测状态

2. 功能操作：
   - 勾选 `Show Gizmos` 在场景视图中显示边界
   - 使用颜色选择器修改边界颜色
   - 勾选 `Hide Unchecked` 隐藏未启用射线检测的元素
   - 点击列表中的复选框修改元素的射线检测状态

## 技术细节

- 继承 `EditorWindow` 实现自定义窗口
- 使用 `DrawGizmo` 实现场景视图绘制
- 集成 `Undo` 系统支持操作撤销
- 实现实时预览和自动刷新
- 提供完整的UI元素管理

## 代码示例

```csharp
public class RaycastTargetChecker : EditorWindow
{
    [MenuItem("Tools/RaycastTarget Checker")]
    private static void Open()
    {
        instance = instance ?? EditorWindow.GetWindow<RaycastTargetChecker>("RaycastTargets");
        instance.Show();
    }

    private void DrawElement(MaskableGraphic graphic)
    {
        using (EditorGUILayout.HorizontalScope horizontalScope = new EditorGUILayout.HorizontalScope())
        {
            Undo.RecordObject(graphic, "Modify RaycastTarget");
            graphic.raycastTarget = EditorGUILayout.Toggle(graphic.raycastTarget, GUILayout.Width(20));
            EditorGUILayout.ObjectField(graphic, typeof(MaskableGraphic), true);
        }
    }

    [DrawGizmo(GizmoType.Selected | GizmoType.NonSelected)]
    private static void DrawGizmos(MaskableGraphic source, GizmoType gizmoType)
    {
        if (instance.showBorders && source.raycastTarget)
        {
            Vector3[] corners = new Vector3[4];
            source.rectTransform.GetWorldCorners(corners);
            Gizmos.color = instance.borderColor;
            for (int i = 0; i < 4; i++)
            {
                Gizmos.DrawLine(corners[i], corners[(i + 1) % 4]);
            }
        }
    }
}
```

## 实现原理

1. UI元素管理
   - 获取场景UI元素
   - 管理射线检测状态
   - 更新元素属性
   - 处理选择状态

2. 可视化显示
   - 绘制边界框
   - 更新场景视图
   - 处理选中状态
   - 自定义显示样式

3. 编辑器集成
   - 窗口布局管理
   - 事件系统处理
   - 撤销系统集成
   - 实时更新刷新

## 应用场景

1. UI开发优化
   - 性能优化检查
   - 射线检测管理
   - 布局问题诊断
   
2. 开发调试
   - UI元素检查
   - 交互区域可视化
   - 问题快速定位
   
3. 团队协作
   - UI规范检查
   - 性能问题排查
   - 快速问题修复

## 注意事项

- 大量UI元素时的性能
- 正确处理撤销操作
- 及时更新视图显示
- 处理选择状态变化
- 注意内存使用情况

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 