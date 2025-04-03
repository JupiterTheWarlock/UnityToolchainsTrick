# Unity自定义资源图标工具

这个示例展示了如何为Unity中的自定义资源（ScriptableObject）设置自定义图标，提供了两种不同的实现方式。

## 功能特点

- 自定义资源图标
- 多种实现方式
- 菜单集成
- 运行时设置
- 批量处理支持
- 图标预览
- 便捷操作接口

## 使用方法

1. 创建自定义资源：
   - 在Project视图中右键选择 `Assets/Create/CreateExample_53_CustomSO_1`
   - 或选择 `Assets/Create/CreateExample_53_CustomSO_2`
   - 资源将使用自定义图标显示

2. 设置自定义图标：
   - 选择目标资源
   - 右键选择 `Assets/Example_53/SetAssetsCustomIcon`
   - 图标将被设置为错误图标样式

## 技术细节

- 使用 `EditorGUIUtility.SetIconForObject` 设置图标
- 支持Gizmos文件夹图标映射
- 提供编辑器扩展方法
- 实现资源创建菜单
- 支持图标动态修改

## 代码示例

```csharp
public class CreateExample_53_Assets
{
    // 创建自定义ScriptableObject
    [MenuItem("Assets/Create/CreateExample_53_CustomSO_1", false, 10)]
    public static void CreateExample_53_CustomSO_1()
    {
        var so1 = ScriptableObject.CreateInstance<CustomSO_1>();
        ProjectWindowUtil.CreateAsset(so1, "CreateExample_53_CustomSO_1.asset");
    }
    
    // 设置自定义图标
    [MenuItem("Assets/Example_53/SetAssetsCustomIcon", false, 10)]
    public static void SetCustomIcon()
    {
        EditorGUIExtension.SetIcon(Selection.activeObject, "console.erroricon");
    }
}

// 自定义ScriptableObject
public class CustomSO_1 : ScriptableObject
{
}
```

## 实现原理

1. 图标设置
   - 运行时设置
   - Gizmos映射
   - 图标缓存
   - 刷新机制

2. 资源管理
   - 创建资源
   - 保存资源
   - 资源命名
   - 路径处理

3. 编辑器集成
   - 菜单注册
   - 选择处理
   - 预览更新
   - 撤销支持

## 应用场景

1. 资源管理
   - 自定义资源标识
   - 资源分类管理
   - 快速资源识别
   
2. 编辑器扩展
   - 自定义工具图标
   - 状态可视化
   - 类型标识
   
3. 工作流优化
   - 资源组织
   - 视觉反馈
   - 操作效率

## 注意事项

- 图标文件命名规范
- 处理图标缓存
- 注意图标大小
- 考虑性能影响
- 处理图标丢失

## 实现方式对比

1. Gizmos文件夹方式：
   - 优点：持久化存储，不影响脚本图标
   - 缺点：需要特定的文件夹结构和命名规则
   
2. SetIconForObject方式：
   - 优点：动态设置，灵活控制
   - 缺点：会影响脚本文件图标，需要手动管理

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 