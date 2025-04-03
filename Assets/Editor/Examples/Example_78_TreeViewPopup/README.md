# Unity树视图弹出窗口工具

这个示例展示了如何在Unity编辑器中创建和使用树视图弹出窗口，实现对象选择和场景资源管理功能。

## 功能特点

- 树视图弹出窗口
- 对象选择功能
- 场景资源浏览
- 双击操作支持
- 右键菜单集成
- 类型泛型支持
- 自定义数据源

## 使用方法

1. 创建弹出窗口：
```csharp
public class CustomTreeViewWindow : EditorWindow
{
    private ObjectSelectTreeView<GameObject> objectTreeView;
    private TreeViewState treeViewState;
    
    [MenuItem("Tools/Show TreeView")]
    static void ShowWindow()
    {
        var window = GetWindow<CustomTreeViewWindow>();
        window.titleContent = new GUIContent("对象选择器");
        window.Show();
    }
}
```

2. 显示选择弹出窗口：
```csharp
var popup = SelectTreeViewWindow.Show<ObjectSelectTreeView<GameObject>, GameObject>(
    selectedObject =>
    {
        Debug.Log($"选中对象: {selectedObject.name}");
    }, 
    typeof(CustomTreeViewWindow)
);
popup.SetData(GameObject.FindObjectsOfType<GameObject>());
```

## 技术细节

- TreeView控件使用
- 泛型类型支持
- 事件系统集成
- 资源加载管理
- 界面布局控制

## 实现原理

1. 视图系统
   - 树结构管理
   - 节点控制
   - 数据绑定
   - 状态同步

2. 选择机制
   - 对象引用
   - 事件处理
   - 回调系统
   - 状态更新

3. 数据管理
   - 类型处理
   - 资源加载
   - 缓存系统
   - 更新机制

## 应用场景

1. 资源管理
   - 对象选择
   - 资源浏览
   - 场景管理
   
2. 开发工具
   - 资源选择器
   - 对象查找器
   - 层级浏览器
   
3. 编辑器扩展
   - 自定义窗口
   - 工具集成
   - 界面定制

## 注意事项

- 类型安全
- 内存管理
- 性能优化
- 状态同步
- 资源释放

## 扩展建议

1. 功能扩展
   - 搜索过滤
   - 拖放支持
   - 预览功能
   - 批量操作

2. 界面优化
   - 自定义样式
   - 图标支持
   - 列表视图
   - 分组显示

## 代码示例

```csharp
public class AdvancedTreeViewPopup<T> where T : Object
{
    private TreeViewState treeViewState;
    private ObjectSelectTreeView<T> treeView;
    private SearchField searchField;
    private string searchString = string.Empty;
    
    public void Initialize()
    {
        treeViewState = new TreeViewState();
        treeView = new ObjectSelectTreeView<T>(treeViewState);
        searchField = new SearchField();
        
        // 配置树视图
        treeView.DoubleClick = OnItemDoubleClicked;
        treeView.AddMenu("选择", OnItemSelected);
    }
    
    public void OnGUI()
    {
        // 搜索栏
        EditorGUILayout.BeginHorizontal(EditorStyles.toolbar);
        string newSearch = searchField.OnToolbarGUI(searchString);
        if (newSearch != searchString)
        {
            searchString = newSearch;
            treeView.searchString = searchString;
            treeView.Reload();
        }
        EditorGUILayout.EndHorizontal();
        
        // 树视图
        Rect rect = EditorGUILayout.GetControlRect(false, 
            GUILayout.ExpandWidth(true), 
            GUILayout.ExpandHeight(true));
        treeView.OnGUI(rect);
    }
    
    public void SetData(IList<T> items)
    {
        treeView.SetData(items);
    }
    
    private void OnItemSelected(object item)
    {
        if (item is T selectedItem)
        {
            Debug.Log($"选中: {selectedItem.name}");
            // 处理选中逻辑
        }
    }
    
    private void OnItemDoubleClicked(object item)
    {
        if (item is T selectedItem)
        {
            Debug.Log($"双击: {selectedItem.name}");
            // 处理双击逻辑
        }
    }
}

// 使用示例
public class CustomObjectSelector : EditorWindow
{
    private AdvancedTreeViewPopup<GameObject> treeViewPopup;
    
    private void OnEnable()
    {
        treeViewPopup = new AdvancedTreeViewPopup<GameObject>();
        treeViewPopup.Initialize();
        
        // 加载数据
        var objects = GameObject.FindObjectsOfType<GameObject>();
        treeViewPopup.SetData(objects);
    }
    
    private void OnGUI()
    {
        treeViewPopup.OnGUI();
    }
}
```

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 