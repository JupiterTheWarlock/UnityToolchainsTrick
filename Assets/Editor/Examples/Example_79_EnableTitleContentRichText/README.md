# Unity标题内容富文本工具

这个示例展示了如何在Unity编辑器窗口标题中启用富文本支持，实现动态和丰富的标题显示效果。

## 功能特点

- 标题富文本支持
- 动态状态显示
- 图标集成
- 实时更新
- 工具提示
- 自定义样式
- 反射机制应用

## 使用方法

1. 创建窗口：
```csharp
[MenuItem("Tools/Example_79_EnableTitleContentRichText")]
private static void Init()
{
    var window = GetWindow<TinyWebServerWindow>();
    window.minSize = new Vector2(300, 180);
    var icon = EditorGUIUtility.IconContent("d_BuildSettings.Web.Small");
    window.titleContent = new GUIContent("Tiny WebServer", icon.image);
    window.Show();
}
```

2. 更新标题：
```csharp
private void TryRepaintTitleContent()
{
    window.titleContent.text = "Tiny WebServer <color=" + 
        (IsListening ? "green" : "red") + ">●</color>";
    window.titleContent.tooltip = IsListening ? 
        "Server is running" : "Server is stopped";
}
```

## 技术细节

- 反射API使用
- GUI样式管理
- 窗口标题控制
- 状态监控系统
- 实时更新机制

## 实现原理

1. 标题系统
   - 富文本解析
   - 样式计算
   - 图标管理
   - 状态显示

2. 更新机制
   - 定时检查
   - 状态变更
   - 重绘触发
   - 样式刷新

3. 反射应用
   - 类型获取
   - 字段访问
   - 样式修改
   - 缓存清理

## 应用场景

1. 工具窗口
   - 状态显示
   - 进度指示
   - 警告提醒
   
2. 编辑器扩展
   - 自定义窗口
   - 动态标题
   - 视觉反馈
   
3. 调试工具
   - 运行状态
   - 连接指示
   - 错误提示

## 注意事项

- 反射性能
- 更新频率
- 内存管理
- 样式兼容
- 版本适配

## 扩展建议

1. 功能扩展
   - 动画效果
   - 多状态支持
   - 自定义颜色
   - 样式预设

2. 工具优化
   - 性能优化
   - 缓存机制
   - 配置保存
   - 事件系统

## 代码示例

```csharp
public class AdvancedTitleWindow : EditorWindow
{
    private bool isActive;
    private string currentStatus;
    private Color statusColor;
    
    private void UpdateWindowTitle()
    {
        var title = $"高级窗口 <color={ColorUtility.ToHtmlStringRGB(statusColor)}>" +
                   $"{currentStatus}</color>";
        titleContent = new GUIContent(title);
        
        // 更新工具提示
        titleContent.tooltip = $"当前状态: {currentStatus}";
        
        // 触发重绘
        Repaint();
    }
    
    private void SetStatus(string status, Color color)
    {
        currentStatus = status;
        statusColor = color;
        UpdateWindowTitle();
    }
    
    private void OnGUI()
    {
        if (GUILayout.Button("切换状态"))
        {
            isActive = !isActive;
            SetStatus(
                isActive ? "运行中" : "已停止",
                isActive ? Color.green : Color.red
            );
        }
    }
}
```

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 