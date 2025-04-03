# Unity WebView编辑器窗口工具

这个示例展示了如何在Unity编辑器中创建内嵌的Web浏览器窗口。

## 功能特点

- 支持内嵌网页显示
- 自定义窗口尺寸
- 支持URL导航
- 可调整窗口位置
- 支持版本兼容性检查
- 自动窗口管理
- 支持多窗口实例

## 使用方法

1. 在Unity编辑器菜单中选择 `Tools -> WebViewWindow`
2. 将会打开一个内嵌的Web浏览器窗口，显示指定的URL内容
3. 窗口支持：
   - 调整大小
   - 拖动位置
   - 网页交互
   - 多实例打开

## 技术细节

- 使用反射访问Unity内部API
- 支持Unity 2020之前的版本
- 使用 `WebViewEditorWindowTabs` 类
- 提供完整的窗口管理API
- 自动处理窗口生命周期

## 代码示例

```csharp
[MenuItem("Tools/WebViewWindow")]
static void Open()
{
    string typeName = "UnityEditor.Web.WebViewEditorWindowTabs";
    Type type = Assembly.Load("UnityEditor.dll").GetType(typeName);
    BindingFlags Flags = BindingFlags.Public | BindingFlags.Static | BindingFlags.FlattenHierarchy;
    var methodInfo = type.GetMethod("Create", Flags);
    methodInfo = methodInfo.MakeGenericMethod(type);
    methodInfo.Invoke(null, new object[] { "WebView", Url, 200, 530, 800, 600 });
}
```

## 实现原理

1. 获取Unity内部WebView类型
2. 使用反射创建窗口实例
3. 配置窗口参数
4. 加载目标URL
5. 管理窗口生命周期

## 窗口参数

1. 基本设置
   - 窗口标题
   - 目标URL
   - 初始位置(x,y)
   - 窗口尺寸(width,height)
   
2. 显示选项
   - 支持窗口最大化
   - 支持窗口最小化
   - 支持窗口关闭
   - 支持窗口焦点

## 注意事项

- 版本兼容性检查
- 正确处理URL格式
- 注意内存资源管理
- 处理网络连接异常
- 正确使用反射API

## 开发环境要求

- Unity 2018.4或更高版本（不支持Unity 2020及以上版本）
- .NET Framework 4.x 