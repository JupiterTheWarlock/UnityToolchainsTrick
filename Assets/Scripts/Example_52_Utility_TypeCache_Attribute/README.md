# Unity类型缓存和特性工具

这个示例展示了如何实现高效的类型缓存和特性（Attribute）管理系统，提供了一套完整的反射和特性处理工具。

## 功能特点

- 类型特性缓存
- 字段特性管理
- 方法特性处理
- 高效反射支持
- 泛型类型处理
- 缓存优化机制
- 完整错误处理

## 使用方法

1. 类型特性获取：
   ```csharp
   if (Utility_Attribute.TryGetTypeAttribute<CustomAttribute>(typeof(MyClass), out var attribute))
   {
       // 使用attribute
   }
   ```

2. 字段特性获取：
   ```csharp
   if (Utility_Attribute.TryGetFieldAttribute<SerializeField>(typeof(MyClass), "fieldName", out var attribute))
   {
       // 使用attribute
   }
   ```

3. 方法特性获取：
   ```csharp
   if (Utility_Attribute.TryGetMethodAttribute<ContextMenu>(typeof(MyClass), "methodName", out var attribute))
   {
       // 使用attribute
   }
   ```

## 技术细节

- 使用字典实现特性缓存
- 支持类型、字段、方法特性
- 实现泛型方法处理
- 提供完整的错误检查
- 优化反射性能

## 代码示例

```csharp
public static partial class Utility_Attribute
{
    // 类型特性缓存
    private static readonly Dictionary<Type, Attribute[]> TypeAttributes = 
        new Dictionary<Type, Attribute[]>();

    // 字段特性缓存
    private static readonly Dictionary<Type, Dictionary<string, Attribute[]>> TypeFieldAttributes =
        new Dictionary<Type, Dictionary<string, Attribute[]>>();

    // 获取类型特性示例
    public static bool TryGetTypeAttribute<AttributeType>(Type _type, out AttributeType _attribute)
        where AttributeType : Attribute
    {
        if (TryGetTypeAttributes(_type, out Attribute[] attributes))
        {
            foreach (var tempAttribute in attributes)
            {
                _attribute = tempAttribute as AttributeType;
                if (_attribute != null)
                    return true;
            }
        }
        _attribute = null;
        return false;
    }

    // 获取字段特性示例
    public static bool TryGetFieldAttribute<AttributeType>(Type _type, string _fieldName,
        out AttributeType _attribute) where AttributeType : Attribute
    {
        return TryGetFieldInfoAttribute(
            Utility_Reflection.GetFieldInfo(_type, _fieldName), 
            out _attribute);
    }
}
```

## 实现原理

1. 缓存机制
   - 类型特性缓存
   - 字段特性缓存
   - 方法特性缓存
   - 缓存更新策略

2. 反射优化
   - 减少反射调用
   - 缓存反射结果
   - 优化查找性能
   - 内存使用优化

3. 特性处理
   - 特性类型检查
   - 继承关系处理
   - 多重特性支持
   - 特性参数处理

## 应用场景

1. 编辑器工具
   - 自定义Inspector
   - 属性绘制器
   - 编辑器扩展
   
2. 运行时功能
   - 配置系统
   - 序列化处理
   - 动态功能加载
   
3. 框架开发
   - 依赖注入
   - 事件系统
   - 组件管理

## 注意事项

- 合理使用缓存
- 处理类型加载
- 注意内存占用
- 优化反射调用
- 处理特性继承

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 