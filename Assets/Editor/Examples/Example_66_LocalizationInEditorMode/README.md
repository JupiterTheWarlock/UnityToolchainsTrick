# Unity编辑器模式本地化工具

这个示例展示了如何在Unity编辑器模式下实现界面本地化功能，支持多语言切换和动态文本更新。

## 功能特点

- 编辑器界面本地化
- 多语言支持
- 动态语言切换
- 资源自动加载
- GUIContent扩展
- 本地化资源管理
- 实时预览

## 使用方法

1. 基本设置：
```csharp
// 设置当前语言
EditorPrefs.SetString("CurrentLanguage", "zh-CN");

// 使用本地化文本
var content = GUIContent_Extend.GetText("key_hello_world");
EditorGUILayout.LabelField(content);
```

2. 资源配置：
   - 在Resources文件夹中创建语言配置文件
   - 按语言代码命名配置文件
   - 设置键值对应的文本

3. 使用本地化：
```csharp
// 创建本地化的GUIContent
var guiContent = new GUIContent_Extend("key_button_text");
if (GUILayout.Button(guiContent))
{
    // 按钮点击处理
}
```

## 技术细节

- 使用Resources管理语言资源
- 实现GUIContent扩展
- 支持动态语言切换
- 提供缓存机制

## 实现原理

1. 资源管理
   - 语言文件加载
   - 资源缓存
   - 动态更新
   - 内存管理

2. 本地化系统
   - 语言切换
   - 文本查找
   - 默认值处理
   - 错误处理

3. 编辑器集成
   - GUI扩展
   - 事件处理
   - 状态保持
   - 实时更新

## 应用场景

1. 编辑器工具
   - 工具界面
   - 设置面板
   - 提示信息
   
2. 开发流程
   - 多语言开发
   - 团队协作
   - 本地化测试
   
3. 用户界面
   - 菜单项
   - 按钮文本
   - 提示框

## 注意事项

- 资源文件命名规范
- 键值唯一性
- 默认语言设置
- 资源加载性能
- 内存管理

## 扩展建议

1. 功能扩展
   - 字体切换
   - 图片本地化
   - 样式本地化
   - 导入导出

2. 工具优化
   - 预览窗口
   - 检查工具
   - 批量处理
   - 自动化工具

## 代码示例

```csharp
public class LocalizationExample : EditorWindow
{
    void OnGUI()
    {
        // 语言切换
        if (GUILayout.Button(GUIContent_Extend.GetText("switch_language")))
        {
            string currentLang = EditorPrefs.GetString("CurrentLanguage");
            string newLang = currentLang == "zh-CN" ? "en-US" : "zh-CN";
            EditorPrefs.SetString("CurrentLanguage", newLang);
            Repaint();
        }

        // 本地化文本显示
        EditorGUILayout.LabelField(GUIContent_Extend.GetText("welcome_message"));
    }
}
```

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 