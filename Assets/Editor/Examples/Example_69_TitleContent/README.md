# Unity编辑器窗口标题内容工具

这个示例展示了如何在Unity编辑器中自定义窗口标题内容，包括设置标题文本和图标。

## 功能特点

- 自定义窗口标题
- 支持标题图标
- 动态标题更新
- 编辑器窗口扩展
- 简单易用
- 无缝集成
- 实时预览

## 使用方法

1. 基本设置：
```csharp
public class CustomEditorWindow : EditorWindow
{
    [MenuItem("Tools/CustomWindow")]
    private static void ShowWindow()
    {
        var window = GetWindow<CustomEditorWindow>("窗口标题");
        
        // 设置标题内容
        var titleContent = new GUIContent();
        titleContent.text = "自定义标题";
        titleContent.image = AssetDatabase.LoadAssetAtPath<Texture2D>("图标路径");
        window.titleContent = titleContent;
    }
}
```

2. 动态更新：
```csharp
void UpdateWindowTitle(string newTitle, Texture2D newIcon)
{
    titleContent = new GUIContent(newTitle, newIcon);
}
```

## 技术细节

- 使用EditorWindow
- GUIContent集成
- 图标资源加载
- 窗口管理

## 实现原理

1. 窗口系统
   - EditorWindow继承
   - 标题内容管理
   - 图标处理
   - 窗口显示

2. 资源管理
   - 图标加载
   - 资源路径
   - 内存管理
   - 资源释放

3. 界面更新
   - 标题更新
   - 实时刷新
   - 状态保持
   - 事件处理

## 应用场景

1. 编辑器工具
   - 自定义工具窗口
   - 设置面板
   - 调试窗口
   
2. 开发辅助
   - 状态显示
   - 工具标识
   - 功能分类
   
3. 用户界面
   - 品牌展示
   - 功能标识
   - 视觉反馈

## 注意事项

- 图标尺寸适配
- 资源路径管理
- 内存资源释放
- 窗口状态维护
- 性能考虑

## 扩展建议

1. 功能扩展
   - 动画标题
   - 状态指示
   - 交互反馈
   - 多语言支持

2. 界面优化
   - 样式定制
   - 主题适配
   - 布局优化
   - 视觉效果

## 代码示例

```csharp
public class AdvancedTitleContent : EditorWindow
{
    private static AdvancedTitleContent window;
    private Texture2D[] titleIcons;
    private int currentIconIndex;

    [MenuItem("Tools/Advanced Title")]
    private static void ShowWindow()
    {
        window = GetWindow<AdvancedTitleContent>();
        window.LoadTitleIcons();
        window.UpdateTitleContent();
    }

    private void LoadTitleIcons()
    {
        titleIcons = new Texture2D[]
        {
            AssetDatabase.LoadAssetAtPath<Texture2D>("Assets/Icons/Icon1.png"),
            AssetDatabase.LoadAssetAtPath<Texture2D>("Assets/Icons/Icon2.png")
        };
    }

    private void UpdateTitleContent()
    {
        titleContent = new GUIContent("动态标题", titleIcons[currentIconIndex]);
    }

    private void OnGUI()
    {
        if (GUILayout.Button("切换图标"))
        {
            currentIconIndex = (currentIconIndex + 1) % titleIcons.Length;
            UpdateTitleContent();
        }
    }
}
```

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 