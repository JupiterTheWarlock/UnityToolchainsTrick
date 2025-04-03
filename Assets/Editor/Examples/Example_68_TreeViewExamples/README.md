# Unity树形视图示例

这个示例展示了如何在Unity编辑器中实现和使用树形视图控件，支持层级数据的显示和管理。

## 功能特点

- 树形结构显示
- 层级数据管理
- 拖放重排序
- 展开/折叠控制
- 多选支持
- 上下文菜单
- 自定义绘制

## 使用方法

1. 创建树形视图：
```csharp
public class CustomTreeView : TreeView
{
    public CustomTreeView(TreeViewState state)
        : base(state)
    {
        Reload();
    }

    protected override TreeViewItem BuildRoot()
    {
        var root = new TreeViewItem { id = 0, depth = -1, displayName = "Root" };
        var allItems = new List<TreeViewItem>();
        // 添加子项
        allItems.Add(new TreeViewItem { id = 1, depth = 0, displayName = "Item 1" });
        SetupParentsAndChildrenFromDepths(root, allItems);
        return root;
    }
}
```

2. 使用树形视图：
```csharp
public class TreeViewWindow : EditorWindow
{
    [SerializeField] TreeViewState treeViewState;
    CustomTreeView treeView;

    void OnEnable()
    {
        if (treeViewState == null)
            treeViewState = new TreeViewState();

        treeView = new CustomTreeView(treeViewState);
    }

    void OnGUI()
    {
        treeView.OnGUI(new Rect(0, 0, position.width, position.height));
    }
}
```

## 技术细节

- 使用TreeView基类
- 实现数据模型
- 支持自定义绘制
- 处理用户交互

## 实现原理

1. 数据结构
   - 树形模型
   - 节点管理
   - 状态保持
   - 序列化支持

2. 视图控制
   - 项目绘制
   - 展开控制
   - 选择管理
   - 滚动处理

3. 交互处理
   - 拖放操作
   - 菜单控制
   - 键盘导航
   - 多选支持

## 应用场景

1. 数据管理
   - 层级数据
   - 文件系统
   - 组织结构
   
2. 编辑器工具
   - 资源管理器
   - 场景大纲
   - 配置编辑器
   
3. 可视化工具
   - 依赖关系
   - 节点编辑器
   - 状态机编辑器

## 注意事项

- 性能优化
- 数据一致性
- 状态管理
- 内存使用
- 用户体验

## 扩展建议

1. 功能扩展
   - 搜索过滤
   - 排序功能
   - 列表视图
   - 数据导出

2. 交互优化
   - 自定义图标
   - 行高设置
   - 工具提示
   - 快捷操作

## 代码示例

```csharp
public class TreeViewItem : TreeViewItem<MyData>
{
    public TreeViewItem(int id, int depth, string displayName, MyData data) 
        : base(id, depth, displayName, data)
    {
    }

    public override void OnGUI(Rect rect, bool selected, bool focused)
    {
        // 自定义绘制逻辑
        GUI.Label(rect, displayName);
        
        if (data != null)
        {
            // 显示额外数据
            var dataRect = rect;
            dataRect.x += rect.width - 100;
            dataRect.width = 100;
            EditorGUI.LabelField(dataRect, data.value.ToString());
        }
    }
}
```

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 