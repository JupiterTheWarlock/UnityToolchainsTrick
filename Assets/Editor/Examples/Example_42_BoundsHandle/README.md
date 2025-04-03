# Unity边界控制手柄工具

这个示例展示了如何在Unity编辑器中使用不同类型的边界控制手柄（BoundsHandle）来可视化和编辑对象的边界。

## 功能特点

- 支持多种边界类型
- 可视化边界编辑
- 实时预览更新
- 支持撤销/重做
- 自定义手柄颜色
- 场景视图交互
- 精确边界控制

## 使用方法

1. 支持的边界类型：
   - 盒型边界 (BoxBoundsHandle)
   - 球型边界 (SphereBoundsHandle)
   - 胶囊型边界 (CapsuleBoundsHandle)

2. 编辑操作：
   - 在场景视图中直接拖拽手柄调整边界
   - 使用控制点调整大小和形状
   - 实时预览边界变化
   - 支持精确数值输入

## 技术细节

- 使用 `UnityEditor.IMGUI.Controls` 命名空间
- 继承自 `Editor` 类
- 实现 `OnSceneGUI` 方法
- 支持边界数据序列化
- 提供完整的编辑器集成

## 代码示例

```csharp
// 盒型边界示例
[CustomEditor(typeof(BoxBoundsExample))]
public class BoundsExampleEditor : Editor
{
    private BoxBoundsHandle m_BoxBoundsHandle;
    
    protected virtual void OnSceneGUI()
    {
        BoxBoundsExample boundsExample = (BoxBoundsExample)target;
        m_BoxBoundsHandle.center = boundsExample.transform.position + boundsExample.BoxBounds.center;
        m_BoxBoundsHandle.size = boundsExample.BoxBounds.size;
        m_BoxBoundsHandle.DrawHandle();
    }
}

// 球型边界示例
[CustomEditor(typeof(SphereBoundsHandleExample))]
public class SphereBoundsHandleExampleEditor : Editor
{
    private SphereBoundsHandle m_SphereBoundsHandle;
    
    protected virtual void OnSceneGUI()
    {
        SphereBoundsHandleExample boundsExample = (SphereBoundsHandleExample)target;
        m_SphereBoundsHandle.center = boundsExample.Center;
        m_SphereBoundsHandle.radius = boundsExample.Radius;
        m_SphereBoundsHandle.DrawHandle();
    }
}
```

## 实现原理

1. 边界控制
   - 创建边界手柄实例
   - 设置边界参数
   - 处理用户输入
   - 更新边界数据

2. 可视化显示
   - 绘制边界轮廓
   - 显示控制手柄
   - 处理颜色设置
   - 更新场景视图

3. 数据同步
   - 记录撤销操作
   - 更新组件数据
   - 保持状态一致
   - 处理序列化

## 应用场景

1. 碰撞检测
   - 设置碰撞边界
   - 调整触发区域
   - 可视化碰撞范围
   
2. 区域定义
   - 标记游戏区域
   - 设置触发范围
   - 定义影响范围
   
3. 调试工具
   - 可视化调试
   - 快速调整范围
   - 优化工作流程

## 注意事项

- 正确处理坐标转换
- 注意性能开销
- 处理多对象编辑
- 考虑缩放影响
- 维护数据一致性

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 