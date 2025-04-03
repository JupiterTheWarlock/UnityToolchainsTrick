# Unity全局输入事件监听工具

这个示例展示了如何在Unity编辑器中实现全局输入事件监听，不受窗口焦点限制。

## 功能特点

- 全局监听键盘输入事件
- 支持组合键检测
- 不受窗口焦点限制
- 可通过EditorPrefs开启/关闭
- 支持以下组合键：
  - 空格 + A
  - 空格 + S
  - 空格 + 上箭头
  - 空格 + 下箭头

## 使用方法

1. 将脚本添加到项目中
2. 通过 `EditorPrefs` 设置 `GLOBAL_INPUT_ENEVT_ENABLE` 为 true 启用功能
3. 在编辑器中任意位置尝试组合键：
   - 按住空格，然后按A键
   - 按住空格，然后按S键
   - 按住空格，然后按上箭头
   - 按住空格，然后按下箭头
4. 在控制台查看触发的组合键信息

## 技术细节

- 使用 `InitializeOnLoadMethod` 特性实现编辑器启动时初始化
- 通过反射获取和设置 `EditorApplication.globalEventHandler`
- 使用 `Event.current` 获取当前事件
- 通过 `EditorPrefs` 控制功能开关
- 支持事件的动态注册和注销

## 代码示例

```csharp
[InitializeOnLoadMethod]
public static void EditorInitialize()
{
    FieldInfo info = typeof(EditorApplication).GetField("globalEventHandler",
        BindingFlags.Static | BindingFlags.Instance | BindingFlags.NonPublic);
    EditorApplication.CallbackFunction functions = 
        (EditorApplication.CallbackFunction)info.GetValue(null);
    
    if (EditorPrefs.GetBool(Constants.GLOBAL_INPUT_ENEVT_ENABLE, false))
    {
        functions += OnGlobalEventHandler;
        info.SetValue(null, (object)functions);
    }
}
```

## 实现原理

1. 通过反射获取Unity编辑器的全局事件处理器
2. 根据配置决定是否注册全局事件监听
3. 在事件处理器中检测组合键状态
4. 触发相应的操作并输出日志

## 注意事项

- 全局事件监听可能影响编辑器性能
- 注意正确处理事件的注册和注销
- 避免在事件处理中执行耗时操作
- 建议提供配置选项控制功能开关
- 注意处理可能的异常情况

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 