# Unity渲染器探索工具

这个示例展示了如何创建一个Unity编辑器扩展工具，用于探索和管理场景中的渲染器组件。该工具参考了Unity的LightingExplorer实现，提供了类似的功能和界面。

## 功能特点

- 渲染器组件探索
- 多标签页管理
- SRP支持
- 实时更新
- 选择同步
- 批量编辑
- 自定义扩展

## 使用方法

1. 打开窗口：
```csharp
[MenuItem("Window/Rendering/Renderer Explorer")]
static void CreateRendererExplorerWindow()
{
    RendererExplorerWindow window = EditorWindow.GetWindow<RendererExplorerWindow>();
    window.minSize = new Vector2(500, 250);
    window.Show();
}
```

2. 创建扩展：
```csharp
public class CustomRendererExtension : IRendererExplorerExtension
{
    private RendererExplorerTab[] tabs;
    
    public RendererExplorerTab[] GetContentTabs()
    {
        return tabs;
    }
    
    public void OnEnable()
    {
        // 初始化标签页
    }
    
    public void OnDisable()
    {
        // 清理资源
    }
}
```

## 技术细节

- 编辑器窗口管理
- 渲染管线集成
- 标签页系统
- 组件探索
- 事件处理

## 实现原理

1. 窗口系统
   - 标签页管理
   - 界面布局
   - 事件处理
   - 状态同步

2. 渲染器管理
   - 组件探索
   - 属性编辑
   - 批量操作
   - 实时更新

3. 扩展系统
   - 接口定义
   - 自定义实现
   - 管线适配
   - 功能扩展

## 应用场景

1. 开发工具
   - 渲染调试
   - 性能优化
   - 场景管理
   
2. 资源管理
   - 材质检查
   - 渲染设置
   - 批量修改
   
3. 调试工具
   - 性能分析
   - 问题定位
   - 优化建议

## 注意事项

- 性能影响
- 内存管理
- 渲染管线兼容
- 大场景处理
- 实时更新开销

## 扩展建议

1. 功能扩展
   - 自定义视图
   - 数据导出
   - 批处理工具
   - 性能分析

2. 工具优化
   - 搜索过滤
   - 预设管理
   - 快捷操作
   - 可视化增强

## 代码示例

```csharp
public class CustomRendererTab : RendererExplorerTab
{
    private TreeViewState treeViewState;
    private RendererTreeView treeView;
    
    public CustomRendererTab()
    {
        title = new GUIContent("自定义渲染器");
    }
    
    public override void OnEnable()
    {
        // 初始化树视图
        if (treeViewState == null)
            treeViewState = new TreeViewState();
            
        treeView = new RendererTreeView(treeViewState);
        treeView.Reload();
    }
    
    public override void OnGUI()
    {
        EditorGUILayout.BeginVertical();
        
        // 工具栏
        DrawToolbar();
        
        // 渲染器列表
        var rect = EditorGUILayout.GetControlRect(false, 
            GUILayout.ExpandWidth(true), 
            GUILayout.ExpandHeight(true));
        treeView.OnGUI(rect);
        
        EditorGUILayout.EndVertical();
    }
    
    private void DrawToolbar()
    {
        EditorGUILayout.BeginHorizontal(EditorStyles.toolbar);
        
        if (GUILayout.Button("刷新", EditorStyles.toolbarButton))
        {
            treeView.Reload();
        }
        
        GUILayout.FlexibleSpace();
        
        // 搜索框
        var searchString = EditorGUILayout.TextField(
            treeView.searchString, 
            EditorStyles.toolbarSearchField
        );
        if (searchString != treeView.searchString)
        {
            treeView.searchString = searchString;
            treeView.Reload();
        }
        
        EditorGUILayout.EndHorizontal();
    }
    
    public override void OnSelectionChange()
    {
        if (treeView != null)
        {
            treeView.SetSelection(Selection.instanceIDs);
        }
    }
}
```

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x
- 支持SRP的Unity版本（可选） 