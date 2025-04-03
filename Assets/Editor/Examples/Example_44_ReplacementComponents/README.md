# Unity组件替换工具

这个示例展示了如何在Unity编辑器中实现组件的无缝替换功能，支持保持组件属性值和预制体实例的处理。

## 功能特点

- 组件类型替换
- 保持属性值
- 支持预制体实例
- 支持撤销/重做
- 自定义右键菜单
- 运行时脚本更新
- 序列化数据保持

## 使用方法

1. 在Inspector中右键点击组件标题栏：
   - 对于Image组件，选择 `Replace To Test Image`
   - 对于TestImage组件，选择 `Replace To Image`
   - 组件将被替换，同时保持原有属性值

2. 支持的操作：
   - 普通游戏对象的组件替换
   - 预制体实例的组件替换
   - 批量组件替换
   - 自定义替换规则

## 技术细节

- 使用 `SerializedObject` 处理序列化
- 支持 `MonoScript` 动态替换
- 处理预制体实例修改
- 提供完整的撤销支持
- 自动处理脚本引用

## 代码示例

```csharp
// 基本组件替换
public static T ReplaceComponent<T>(this Component self) where T : Component
{
    return self.ReplaceComponent(typeof(T)) as T;    
}

// 添加右键菜单项
[MenuItem("CONTEXT/Image/Replace To Test Image")]
static void _imageReplaceToTestImage(MenuCommand command)
{
    ((Component) command.context).ReplaceComponent<TestImage>();
}

// 处理预制体实例
if (PrefabUtility.IsPartOfPrefabInstance(go))
{
    PrefabUtility.ApplyPrefabInstance(PrefabUtility.GetNearestPrefabInstanceRoot(go));
    Undo.DestroyObjectImmediate(self);
    var c = Undo.AddComponent(go, type);
    EditorUtility.CopySerializedManagedFieldsOnly(removeC.Last().assetComponent, c);
    return c;
}
```

## 实现原理

1. 组件替换
   - 获取目标类型
   - 创建新组件
   - 复制属性值
   - 更新序列化数据

2. 预制体处理
   - 检查预制体状态
   - 应用预制体修改
   - 保持属性一致
   - 处理预制体变体

3. 撤销支持
   - 记录操作组
   - 设置操作名称
   - 合并撤销操作
   - 维护状态一致

## 应用场景

1. 开发调试
   - 快速切换组件
   - 测试不同实现
   - 优化工作流程
   
2. 组件升级
   - 批量更新组件
   - 保持数据一致
   - 减少手动操作
   
3. 预制体管理
   - 处理预制体变体
   - 统一组件更新
   - 维护预制体状态

## 注意事项

- 检查类型兼容性
- 处理序列化异常
- 注意预制体状态
- 维护数据一致性
- 考虑性能影响

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 