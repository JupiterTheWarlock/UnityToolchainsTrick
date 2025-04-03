# Unity Gizmos圆形绘制工具

这个示例展示了如何使用Unity的Gizmos系统来绘制自定义的圆形辅助线，用于场景可视化和调试。

## 功能特点

- 自定义圆形绘制
- 可调节半径
- 平滑度控制
- 颜色自定义
- 矩阵变换支持
- 实时预览
- 场景集成

## 使用方法

1. 添加组件：
```csharp
// 将GizmosCircle组件添加到场景物体上
var circle = gameObject.AddComponent<GizmosCircle>();
circle.m_Transform = transform;
circle.m_Radius = 1.0f;
circle.m_Theta = 0.1f;
circle.m_Color = Color.green;
```

2. 参数调整：
```csharp
// 在Inspector中调整参数
public class GizmosCircle : MonoBehaviour
{
    public Transform m_Transform;    // 圆形所在的变换
    public float m_Radius = 1;      // 圆环的半径
    public float m_Theta = 0.1f;    // 平滑度（值越低越平滑）
    public Color m_Color = Color.green; // 线框颜色
}
```

## 技术细节

- Gizmos绘制API
- 矩阵变换处理
- 参数化圆形生成
- 场景视图集成
- 实时渲染支持

## 实现原理

1. 绘制系统
   - 参数计算
   - 点位生成
   - 线段连接
   - 矩阵变换

2. 可视化控制
   - 颜色管理
   - 平滑度调节
   - 半径控制
   - 变换同步

3. 场景集成
   - 组件管理
   - 实时更新
   - 错误处理
   - 性能优化

## 应用场景

1. 调试可视化
   - 范围显示
   - 路径标记
   - 碰撞预览
   
2. 游戏开发
   - 技能范围
   - 触发区域
   - 警戒范围
   
3. 关卡设计
   - 区域标记
   - 距离参考
   - 布局辅助

## 注意事项

- 性能考虑
- 平滑度设置
- 半径限制
- 变换同步
- 场景视图性能

## 扩展建议

1. 功能扩展
   - 多形状支持
   - 动画效果
   - 填充模式
   - 样式预设

2. 工具优化
   - 批量绘制
   - 缓存优化
   - 参数预设
   - 交互控制

## 代码示例

```csharp
public class AdvancedGizmosCircle : MonoBehaviour
{
    [Header("基础设置")]
    public Transform target;
    public float radius = 1f;
    
    [Header("样式设置")]
    public Color fillColor = new Color(0, 1, 0, 0.2f);
    public Color outlineColor = Color.green;
    public float thickness = 2f;
    
    [Header("动画设置")]
    public bool enablePulse = false;
    public float pulseSpeed = 1f;
    public float pulseRange = 0.2f;
    
    private void OnDrawGizmos()
    {
        if (!target) return;
        
        // 计算动画半径
        float currentRadius = radius;
        if (enablePulse)
        {
            float pulse = Mathf.Sin(Time.time * pulseSpeed) * pulseRange;
            currentRadius += pulse;
        }
        
        // 绘制填充
        Gizmos.color = fillColor;
        DrawFilledCircle(currentRadius);
        
        // 绘制轮廓
        Gizmos.color = outlineColor;
        DrawCircleOutline(currentRadius);
    }
    
    private void DrawFilledCircle(float radius)
    {
        const float segment = 0.1f;
        Vector3 lastPoint = Vector3.zero;
        
        for (float theta = 0; theta < 2 * Mathf.PI; theta += segment)
        {
            Vector3 current = new Vector3(
                Mathf.Cos(theta) * radius,
                0,
                Mathf.Sin(theta) * radius
            );
            
            if (theta > 0)
            {
                Gizmos.DrawLine(Vector3.zero, current);
                Gizmos.DrawLine(lastPoint, current);
            }
            
            lastPoint = current;
        }
    }
}
```

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 