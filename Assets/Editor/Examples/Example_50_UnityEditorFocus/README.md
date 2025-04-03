# Unity编辑器焦点监控工具

这个示例展示了如何监控Unity编辑器窗口的焦点状态变化，实现对编辑器焦点获得和失去事件的响应。

## 功能特点

- 焦点状态监控
- 事件系统集成
- 自动初始化
- 实时状态更新
- 日志输出支持
- 全局事件通知
- 低开销实现

## 使用方法

1. 添加事件监听：
   ```csharp
   UnityFocusUtility.OnUnityEditorFocus += OnEditorFocusChanged;
   ```

2. 实现回调方法：
   ```csharp
   private void OnEditorFocusChanged(bool hasFocus)
   {
       if (hasFocus)
           Debug.Log("编辑器获得焦点");
       else
           Debug.Log("编辑器失去焦点");
   }
   ```

## 技术细节

- 使用 `InitializeOnLoad` 特性自动初始化
- 通过 `EditorApplication.update` 实现持续监控
- 利用 `InternalEditorUtility.isApplicationActive` 检测焦点
- 提供全局事件系统支持
- 实现低开销的状态检测

## 代码示例

```csharp
[InitializeOnLoad]
public class UnityFocusUtility
{
    public static event Action<bool> OnUnityEditorFocus = (focus) => { };
    private static bool _appFocused;

    static UnityFocusUtility()
    {
        EditorApplication.update += Update;
    }
    
    private static void Update()
    {
        if (!_appFocused && UnityEditorInternal.InternalEditorUtility.isApplicationActive)
        {
            _appFocused = UnityEditorInternal.InternalEditorUtility.isApplicationActive;
            OnUnityEditorFocus(true);
            Debug.Log("On focus window!");
        }
        else if (_appFocused && !UnityEditorInternal.InternalEditorUtility.isApplicationActive)
        {
            _appFocused = UnityEditorInternal.InternalEditorUtility.isApplicationActive;
            OnUnityEditorFocus(false);
            Debug.Log("On lost focus");
        }
    }
}
```

## 实现原理

1. 初始化机制
   - 编辑器启动自动初始化
   - 注册更新事件
   - 初始化状态变量
   - 配置事件系统

2. 状态监控
   - 持续检测焦点状态
   - 状态变化判断
   - 事件触发控制
   - 日志记录

3. 事件分发
   - 全局事件通知
   - 状态信息传递
   - 回调函数管理
   - 异常处理

## 应用场景

1. 自动化工具
   - 焦点切换处理
   - 自动保存触发
   - 状态同步控制
   
2. 性能优化
   - 资源加载控制
   - 后台任务管理
   - 处理优先级调整
   
3. 用户体验
   - 界面状态更新
   - 提示信息显示
   - 操作响应控制

## 注意事项

- 避免频繁事件触发
- 处理事件注册释放
- 控制日志输出量
- 注意性能开销
- 处理异常情况

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 