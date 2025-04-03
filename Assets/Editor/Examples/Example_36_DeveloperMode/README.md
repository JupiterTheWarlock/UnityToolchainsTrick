# Unity开发者模式工具

这个示例展示了如何在Unity编辑器中实现开发者模式的切换功能。

## 功能特点

- 支持开发者模式切换
- 状态持久化保存
- 快速访问菜单
- 运行时状态检查
- 支持条件编译
- 自动状态恢复
- 支持多项目配置

## 使用方法

1. 在Unity编辑器菜单中：
   - 选择 `Tools -> DeveloperMode -> EnableDeveloperMode` 启用开发者模式
   - 选择 `Tools -> DeveloperMode -> DisableDeveloperMode` 禁用开发者模式
2. 开发者模式状态会被保存在EditorPrefs中
3. 重启Unity后状态会自动恢复

## 技术细节

- 使用 `EditorPrefs` 存储状态
- 提供菜单项快速切换
- 支持编辑器状态管理
- 提供完整的状态检查API
- 自动处理状态持久化

## 代码示例

```csharp
// 启用开发者模式
[MenuItem("Tools/DeveloperMode/EnableDeveloperMode")]
private static void Enable()
{
    UnityEditor.EditorPrefs.SetBool("DeveloperMode", true);
}

// 禁用开发者模式
[MenuItem("Tools/DeveloperMode/DisableDeveloperMode")]
private static void Disable()
{
    UnityEditor.EditorPrefs.SetBool("DeveloperMode", false);
}

// 检查开发者模式状态
public static bool IsDeveloperMode()
{
    return UnityEditor.EditorPrefs.GetBool("DeveloperMode", false);
}
```

## 实现原理

1. 创建菜单项
2. 设置状态标志
3. 保存到EditorPrefs
4. 状态持久化
5. 自动恢复机制

## 应用场景

1. 调试功能
   - 显示调试信息
   - 启用调试工具
   - 记录详细日志
   
2. 开发工具
   - 显示开发菜单
   - 启用高级功能
   - 显示性能数据
   
3. 测试功能
   - 启用测试工具
   - 显示测试数据
   - 支持自动化测试

## 注意事项

- 正确处理状态切换
- 避免状态冲突
- 考虑性能影响
- 处理异常情况
- 注意数据安全

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 