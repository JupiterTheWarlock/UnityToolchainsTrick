# Unity编辑器窗口中绘制Inspector工具

这个示例展示了如何在自定义编辑器窗口中绘制Inspector界面，实现对ScriptableObject资源的编辑功能。

## 功能特点

- 自定义编辑器窗口
- Inspector界面集成
- ScriptableObject资源编辑
- 自定义Inspector布局
- 自定义按钮功能
- 窗口大小控制
- 资源自动加载

## 使用方法

1. 打开编辑器窗口：
   - 在Unity菜单栏选择 `Tools/DrawInspectorOnEditorWindow`
   - 将显示一个固定大小的编辑器窗口

2. 编辑资源属性：
   - 在窗口中可以直接编辑ScriptableObject的属性
   - 包括Name（字符串）、Age（整数）和Skill（字符串列表）
   - 点击"自定义按钮"可触发自定义功能

## 技术细节

- 使用 `EditorWindow` 创建自定义窗口
- 通过 `Editor.CreateEditor` 创建Inspector
- 实现自定义Inspector布局
- 集成ScriptableObject资源管理
- 提供按钮事件处理

## 代码示例

```csharp
// 编辑器窗口类
public class Example_55_Window : EditorWindow
{
    private Editor _editor;
    
    [MenuItem("Tools/DrawInspectorOnEditorWindow", priority = 55)]
    private static void PopUp()
    {
        var window = GetWindow<Example_55_Window>("");
        window.minSize = new Vector2(400, 400);
        window.Init();
        window.Show();
    }
    
    private void Init()
    {
        var asset = AssetDatabase.LoadAssetAtPath<Example_55_Scriptobj>(path);
        _editor = Editor.CreateEditor(asset);
    }
}

// 自定义Inspector类
[CustomEditor(typeof(Example_55_Scriptobj))]
public class Example_55_Inspector : Editor
{
    public override void OnInspectorGUI()
    {
        base.OnInspectorGUI();
        if (GUILayout.Button("自定义按钮"))
        {
            Debug.Log("点击了自定义按钮");
        }
    }
}
```

## 实现原理

1. 窗口创建
   - 继承EditorWindow
   - 设置窗口属性
   - 初始化资源
   - 创建Editor实例

2. Inspector绘制
   - 自定义Inspector类
   - 重写OnInspectorGUI
   - 添加自定义控件
   - 处理用户输入

3. 资源管理
   - 创建ScriptableObject
   - 加载资源文件
   - 保存资源更改
   - 刷新资源显示

## 应用场景

1. 工具开发
   - 资源编辑器
   - 配置管理器
   - 数据预览工具
   
2. 工作流优化
   - 批量数据编辑
   - 自定义预览窗口
   - 资源检查工具
   
3. 界面定制
   - 专用编辑器
   - 数据可视化
   - 交互式工具

## 注意事项

- 正确处理资源加载和卸载
- 注意窗口的生命周期管理
- 处理Inspector的刷新时机
- 考虑undo/redo支持
- 注意内存管理

## 扩展建议

1. 功能扩展：
   - 添加资源预览
   - 支持多资源编辑
   - 集成搜索功能
   - 添加导入导出功能

2. 界面优化：
   - 自定义样式
   - 响应式布局
   - 分组显示
   - 折叠面板

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 