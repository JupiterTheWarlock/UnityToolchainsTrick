# Unity边界框操作工具

这个示例展示了如何在Unity编辑器中创建和管理不同类型的边界框（Bounds），包括盒型、胶囊体和球形边界框的可视化和操作。

## 功能特点

- 多种边界框支持
- 可视化编辑
- 实时预览
- 参数调节
- 场景集成
- 直观操作
- 类型转换

## 使用方法

1. 盒型边界框：
```csharp
public class BoxBoundsExample : MonoBehaviour
{
    // 定义一个中心在原点，大小为1的盒型边界框
    public Bounds BoxBounds = new Bounds(Vector3.zero, Vector3.one);
}
```

2. 胶囊体边界框：
```csharp
public class CapsuleBoundsExample : MonoBehaviour
{
    public Vector3 Center;    // 胶囊体中心点
    public float Radius;      // 胶囊体半径
    public float Height;      // 胶囊体高度
}
```

3. 球形边界框：
```csharp
public class SphereBoundsHandleExample : MonoBehaviour
{
    public Vector3 Center;    // 球体中心点
    public float Radius;      // 球体半径
}
```

## 技术细节

- 边界框计算
- 参数控制
- 可视化渲染
- 碰撞检测
- 变换处理

## 实现原理

1. 边界系统
   - 参数定义
   - 形状计算
   - 碰撞检测
   - 变换同步

2. 可视化控制
   - 边界显示
   - 操作手柄
   - 实时更新
   - 参数同步

3. 编辑器集成
   - 自定义检查器
   - 场景视图
   - 操作响应
   - 数据持久化

## 应用场景

1. 游戏开发
   - 碰撞检测
   - 触发区域
   - 物理边界
   
2. 关卡设计
   - 区域划分
   - 空间规划
   - 碰撞设置
   
3. 调试工具
   - 边界可视化
   - 碰撞测试
   - 空间分析

## 注意事项

- 性能考虑
- 精度控制
- 碰撞检测
- 更新频率
- 内存管理

## 扩展建议

1. 功能扩展
   - 复合边界框
   - 动态更新
   - 路径预测
   - 碰撞回调

2. 工具优化
   - 批量编辑
   - 预设支持
   - 导入导出
   - 可视化增强

## 代码示例

```csharp
public class AdvancedBoundsHandler : MonoBehaviour
{
    [System.Serializable]
    public class BoundsData
    {
        public Vector3 center;
        public Vector3 size;
        public BoundsType type;
        public Color color = Color.green;
    }
    
    public enum BoundsType
    {
        Box,
        Sphere,
        Capsule
    }
    
    public BoundsData boundsData;
    public bool showBounds = true;
    public bool enableCollision = true;
    
    private void OnDrawGizmos()
    {
        if (!showBounds) return;
        
        Gizmos.color = boundsData.color;
        
        switch (boundsData.type)
        {
            case BoundsType.Box:
                Gizmos.DrawWireCube(boundsData.center, boundsData.size);
                break;
                
            case BoundsType.Sphere:
                Gizmos.DrawWireSphere(boundsData.center, 
                    boundsData.size.x * 0.5f);
                break;
                
            case BoundsType.Capsule:
                DrawWireCapsule(boundsData.center, 
                    boundsData.size.x * 0.5f, 
                    boundsData.size.y);
                break;
        }
    }
    
    private void DrawWireCapsule(Vector3 center, float radius, float height)
    {
        // 绘制胶囊体的实现...
    }
    
    public bool IsPointInside(Vector3 point)
    {
        switch (boundsData.type)
        {
            case BoundsType.Box:
                var bounds = new Bounds(boundsData.center, boundsData.size);
                return bounds.Contains(point);
                
            case BoundsType.Sphere:
                return Vector3.Distance(point, boundsData.center) <= 
                    boundsData.size.x * 0.5f;
                
            case BoundsType.Capsule:
                // 胶囊体点位检测实现...
                return false;
                
            default:
                return false;
        }
    }
}
```

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 