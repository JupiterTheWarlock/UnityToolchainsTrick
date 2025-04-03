# Unity普通对象绘制工具

这个示例展示了如何在Unity编辑器中创建自定义属性绘制器，实现普通对象的可视化编辑功能。

## 功能特点

- 自定义属性绘制
- 范围值控制
- Inspector面板集成
- 动态属性更新
- 列表类型支持
- 自定义属性特性
- 实时预览功能

## 使用方法

1. 打开工具窗口：
   - 在Unity菜单中选择 `Tools -> DrawNormalObject`
   - 窗口中显示测试数据的编辑界面

2. 属性编辑：
   - 直接在窗口中编辑属性值
   - 使用滑动条调整范围值
   - 点击"绘制一个普通对象到Inspector"在Inspector中查看

## 技术细节

- 继承 `EditorWindow` 实现自定义窗口
- 使用 `ObjectDrawerAttribute` 创建属性特性
- 实现 `FieldDrawer` 自定义绘制逻辑
- 支持列表类型的属性绘制
- 提供完整的属性绘制API

## 代码示例

```csharp
// 自定义范围属性
public class FloatRangeAttribute : ObjectDrawerAttribute
{
    public float minLimit, maxLimit;
    public FloatRangeAttribute(float _minLimit, float _maxLimit)
    {
        minLimit = _minLimit;
        maxLimit = _maxLimit;
    }
}

// 自定义绘制器
[CustomFieldDrawer(typeof(FloatRangeAttribute))]
public class FloatRangeDrawer : FieldDrawer
{
    public override void OnGUI(GUIContent label)
    {
        FloatRangeAttribute rangeAttribute = Attribute as FloatRangeAttribute;
        Value = EditorGUILayout.Slider(label, (float)Value, 
            rangeAttribute.minLimit, rangeAttribute.maxLimit);
    }
}

// 使用示例
public class TestData
{
    public float f;
    [FloatRange(0, 1)]
    public List<float> sliders;
}
```

## 实现原理

1. 属性系统
   - 定义属性特性
   - 创建绘制器
   - 注册绘制类型
   - 处理属性更新

2. 绘制逻辑
   - 自定义GUI布局
   - 处理用户输入
   - 更新属性值
   - 刷新显示

3. 数据管理
   - 序列化支持
   - 类型转换
   - 值范围验证
   - 列表处理

## 应用场景

1. 数据编辑工具
   - 配置文件编辑
   - 游戏参数调整
   - 资源属性编辑
   
2. 开发辅助工具
   - 快速数据预览
   - 批量属性修改
   - 调试数据查看
   
3. 自定义编辑器
   - 专用属性编辑
   - 可视化数据编辑
   - 工具面板定制

## 注意事项

- 处理数值范围验证
- 注意性能开销
- 保持UI响应性
- 处理异常输入
- 维护数据一致性

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 