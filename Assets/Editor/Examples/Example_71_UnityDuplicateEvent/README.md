# Unity复制事件监听工具

这个示例展示了如何在Unity编辑器中监听对象复制事件，实现自定义的复制操作处理。

## 功能特点

- 复制事件监听
- 层级视图集成
- 自动初始化
- 可配置开关
- 事件处理
- 编辑器扩展
- 实时响应

## 使用方法

1. 基本设置：
```csharp
[InitializeOnLoadMethod]
public static void EditorInitialize()
{
    // 注册事件监听
    EditorApplication.hierarchyWindowItemOnGUI += OnHierarchyItemGUI;
}

private static void OnHierarchyItemGUI(int instanceId, Rect selectionRect)
{
    if (Event.current.commandName == "Duplicate")
    {
        // 处理复制事件
        Debug.Log("检测到复制操作");
    }
}
```

2. 配置监听：
```csharp
// 启用监听
EditorPrefs.SetBool("DuplicateEventListen", true);

// 禁用监听
EditorPrefs.SetBool("DuplicateEventListen", false);
```

## 技术细节

- 使用EditorApplication事件
- 层级视图事件处理
- EditorPrefs配置存储
- 事件委托管理

## 实现原理

1. 事件系统
   - 初始化注册
   - 事件监听
   - 事件处理
   - 状态管理

2. 编辑器集成
   - 层级视图集成
   - 命令识别
   - 配置保存
   - 自动加载

3. 状态控制
   - 开关管理
   - 事件过滤
   - 响应处理
   - 数据同步

## 应用场景

1. 开发工具
   - 复制监控
   - 操作记录
   - 行为分析
   
2. 自动化工具
   - 批量处理
   - 自动配置
   - 数据同步
   
3. 调试辅助
   - 操作跟踪
   - 状态监控
   - 错误检测

## 注意事项

- 性能影响控制
- 事件重复处理
- 内存管理
- 配置持久化
- 错误处理

## 扩展建议

1. 功能扩展
   - 复制规则
   - 批量处理
   - 撤销支持
   - 自定义操作

2. 工具优化
   - 可视化配置
   - 状态显示
   - 日志记录
   - 性能优化

## 代码示例

```csharp
public class DuplicateEventHandler
{
    private const string CONFIG_KEY = "EnableDuplicateEvent";
    private static bool isEnabled;

    [InitializeOnLoadMethod]
    private static void Initialize()
    {
        isEnabled = EditorPrefs.GetBool(CONFIG_KEY, false);
        if (isEnabled)
        {
            RegisterEvents();
        }
    }

    private static void RegisterEvents()
    {
        EditorApplication.hierarchyWindowItemOnGUI += OnHierarchyGUI;
    }

    private static void OnHierarchyGUI(int instanceId, Rect selectionRect)
    {
        var current = Event.current;
        if (current.commandName == "Duplicate")
        {
            var obj = EditorUtility.InstanceIDToObject(instanceId);
            if (obj != null)
            {
                Debug.Log($"正在复制对象: {obj.name}");
                // 执行自定义处理
                ProcessDuplicate(obj);
            }
        }
    }

    private static void ProcessDuplicate(Object originalObject)
    {
        // 实现自定义的复制后处理逻辑
    }
}
```

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 