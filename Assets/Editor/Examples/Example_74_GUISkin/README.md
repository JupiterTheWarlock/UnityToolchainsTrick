# Unity GUISkin自定义样式工具

这个示例展示了如何在Unity编辑器中使用GUISkin来自定义GUI控件的样式和外观。

## 功能特点

- 自定义GUI样式
- 可视化样式编辑
- 样式实时预览
- 多控件支持
- 样式复用
- 主题切换
- 编辑器集成

## 使用方法

1. 创建GUISkin：
```csharp
public class CustomEditorWindow : EditorWindow
{
    private GUISkin customSkin;
    private GUIStyle buttonStyle;
    private GUIStyle labelStyle;

    private void Init()
    {
        customSkin = AssetDatabase.LoadAssetAtPath<GUISkin>("Assets/Path/To/YourSkin.guiskin");
        buttonStyle = customSkin.button;
        labelStyle = customSkin.label;
    }
}
```

2. 应用样式：
```csharp
private void OnGUI()
{
    GUILayout.Label("自定义标签样式", labelStyle);
    if (GUILayout.Button("自定义按钮样式", buttonStyle))
    {
        // 按钮点击处理
    }
}
```

## 技术细节

- GUISkin资源管理
- GUIStyle配置
- 样式属性设置
- 实时渲染

## 实现原理

1. 样式系统
   - 资源加载
   - 样式配置
   - 属性设置
   - 实时应用

2. 控件管理
   - 按钮样式
   - 标签样式
   - 布局控制
   - 事件处理

3. 资源控制
   - 样式加载
   - 资源缓存
   - 内存管理
   - 资源释放

## 应用场景

1. 编辑器工具
   - 自定义面板
   - 工具窗口
   - 设置界面
   
2. 主题定制
   - 品牌定制
   - 风格统一
   - 视觉体验
   
3. 界面设计
   - 控件美化
   - 交互优化
   - 视觉反馈

## 注意事项

- 样式资源管理
- 性能优化
- 内存控制
- 实时更新
- 兼容性处理

## 扩展建议

1. 功能扩展
   - 样式预设
   - 主题切换
   - 动态更新
   - 样式导出

2. 工具优化
   - 预览功能
   - 实时编辑
   - 样式复制
   - 批量应用

## 代码示例

```csharp
public class AdvancedGUISkinWindow : EditorWindow
{
    private GUISkin customSkin;
    private Dictionary<string, GUIStyle> styles;
    
    [MenuItem("Tools/Advanced GUISkin")]
    private static void ShowWindow()
    {
        var window = GetWindow<AdvancedGUISkinWindow>();
        window.titleContent = new GUIContent("样式预览");
        window.Init();
    }

    private void Init()
    {
        // 加载自定义皮肤
        customSkin = AssetDatabase.LoadAssetAtPath<GUISkin>(
            "Assets/Editor/Styles/CustomSkin.guiskin");
            
        // 初始化样式字典
        styles = new Dictionary<string, GUIStyle>
        {
            {"button", customSkin.button},
            {"label", customSkin.label},
            {"box", customSkin.box},
            {"toggle", customSkin.toggle}
        };
    }

    private void OnGUI()
    {
        EditorGUILayout.BeginVertical(styles["box"]);
        
        GUILayout.Label("样式预览窗口", styles["label"]);
        
        if (GUILayout.Button("自定义按钮", styles["button"]))
        {
            Debug.Log("按钮被点击");
        }
        
        bool toggleValue = GUILayout.Toggle(false, "自定义开关", styles["toggle"]);
        
        EditorGUILayout.EndVertical();
    }
}
```

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 