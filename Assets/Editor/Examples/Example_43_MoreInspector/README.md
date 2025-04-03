# Unity多重Inspector面板工具

这个示例展示了如何在Unity编辑器中创建和管理多个Inspector面板，支持面板停靠和锁定功能。

## 功能特点

- 创建额外Inspector面板
- 支持面板停靠功能
- 面板锁定机制
- 自定义面板布局
- 动态面板管理
- 保持选择状态
- 支持多对象检视

## 使用方法

1. 在Unity编辑器菜单中选择 `Tools -> 额外Inspector面板`
2. 在弹出的窗口中点击"显示额外Inspector面板"按钮
3. 新的Inspector面板将会：
   - 自动停靠到右侧
   - 锁定显示指定对象
   - 保持独立状态

## 技术细节

- 使用反射访问Unity内部API
- 实现自定义停靠系统
- 管理Inspector状态
- 提供完整的窗口管理API
- 自动处理选择状态

## 代码示例

```csharp
// 创建额外Inspector面板
public EditorWindow GetInspectTarget(UnityEngine.Object targetGO)
{
    Type inspectorType = typeof(Editor).Assembly.GetType("UnityEditor.InspectorWindow");
    EditorWindow inspectorInstance = ScriptableObject.CreateInstance(inspectorType) as EditorWindow;
    
    // 缓存当前选择
    UnityEngine.Object prevSelection = Selection.activeObject;
    // 设置目标对象
    Selection.activeObject = targetGO;
    // 锁定Inspector
    var isLocked = inspectorType.GetProperty("isLocked", BindingFlags.Instance | BindingFlags.Public);
    isLocked.GetSetMethod().Invoke(inspectorInstance, new object[] {true});
    // 恢复选择
    Selection.activeObject = prevSelection;
    
    return inspectorInstance;
}

// 停靠窗口
public static void DockWindow(EditorWindow anchor, EditorWindow docked, DockPosition position)
{
    var anchorParent = GetParentOf(anchor);
    SetDragSource(anchorParent, GetParentOf(docked));
    PerformDrop(GetWindowOf(anchorParent), docked, GetFakeMousePosition(anchor, position));
}
```

## 实现原理

1. 窗口创建
   - 获取Inspector类型
   - 创建窗口实例
   - 设置窗口属性
   - 处理窗口生命周期

2. 停靠系统
   - 模拟鼠标位置
   - 处理停靠逻辑
   - 管理窗口层级
   - 维护窗口关系

3. 状态管理
   - 锁定检视对象
   - 保持选择状态
   - 处理窗口焦点
   - 同步窗口更新

## 停靠位置

1. 支持方向
   - 左侧停靠
   - 顶部停靠
   - 右侧停靠
   - 底部停靠
   
2. 布局控制
   - 自动调整大小
   - 保持最小尺寸
   - 处理重叠关系
   - 优化显示效果

## 注意事项

- 正确处理窗口引用
- 注意内存资源管理
- 处理窗口关闭事件
- 维护停靠状态
- 考虑版本兼容性

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 