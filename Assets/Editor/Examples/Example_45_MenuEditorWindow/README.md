# Unity可调整区域菜单编辑器窗口

这个示例展示了如何创建一个具有可调整区域和树形菜单的Unity编辑器窗口，支持灵活的布局调整和菜单管理。

## 功能特点

- 可调整区域控制
- 树形菜单系统
- 多方向拖拽调整
- 自定义光标提示
- 最小/最大尺寸限制
- 实时布局更新
- 完整的事件处理

## 使用方法

1. 打开编辑器窗口：
   - 在Unity菜单中选择 `Tools -> MenuEditorWindow`
   - 窗口将显示可调整的区域和树形菜单

2. 区域调整：
   - 拖拽边缘调整大小
   - 拖拽角落进行对角线调整
   - 拖拽中心区域移动整个窗口
   - 鼠标悬停时显示调整提示

## 技术细节

- 使用 `ResizableArea` 类处理区域调整
- 实现 `UnityObjectMenuEditorWindow` 基类
- 集成 `TreeViewState` 管理树形菜单
- 支持自定义菜单项数据
- 提供完整的事件系统

## 代码示例

```csharp
// 创建菜单窗口
public class MenuEditorWindow : UnityObjectMenuEditorWindow
{
    [MenuItem("Tools/MenuEditorWindow")]
    public static void Open()
    {
        GetWindow<MenuEditorWindow>();
    }

    protected override CZMenuTreeView BuildMenuTree(TreeViewState _treeViewState)
    {
        CZMenuTreeView menuTree = new CZMenuTreeView(_treeViewState);
        menuTree.AddMenuItem("PlayerSetting", new CZMenuTreeViewItem() 
        { 
            userData = Resources.FindObjectsOfTypeAll<PlayerSettings>().FirstOrDefault() 
        });
        return menuTree;
    }
}

// 可调整区域实现
public class ResizableArea
{
    public void EnableSide(UIDirection _direction)
    {
        enabledSides |= _direction;
    }

    public virtual Rect OnGUI(Rect _rect)
    {
        Reload(_rect);
        // 处理鼠标事件和区域调整
        // ...
    }
}
```

## 实现原理

1. 区域管理
   - 定义可调整方向
   - 处理边界计算
   - 管理拖拽状态
   - 更新区域位置

2. 菜单系统
   - 构建树形结构
   - 管理菜单项
   - 处理选择事件
   - 更新菜单状态

3. 事件处理
   - 鼠标事件响应
   - 光标样式更新
   - 拖拽逻辑处理
   - 边界检查

## 应用场景

1. 自定义编辑器工具
   - 复杂布局管理
   - 多面板设计
   - 灵活区域划分
   
2. 开发工具窗口
   - 项目设置管理
   - 资源预览工具
   - 调试信息面板
   
3. 插件开发
   - 扩展编辑器功能
   - 自定义工作流
   - 工具集成

## 注意事项

- 合理设置最小尺寸
- 处理边界情况
- 优化拖拽性能
- 管理事件冒泡
- 注意内存使用

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 