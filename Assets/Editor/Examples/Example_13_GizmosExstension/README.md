# Unity Gizmos绘制扩展工具

这个示例提供了一套强大的Gizmos绘制扩展工具，用于在Unity场景视图中绘制各种几何形状和辅助线。

## 功能特点

- 提供丰富的几何形状绘制方法：
  - 线框立方体 (WireCube)
  - 线框球体 (WireSphere)
  - 箭头 (Arrow)
  - 圆形 (Circle)
  - 圆弧 (Arc)
  - 圆柱体 (Cylinder)
  - 胶囊体 (Capsule)
- 支持自定义旋转和变换
- 自动集成碰撞器组件的可视化
- 提供精确的数学计算和矩阵变换

## 使用方法

1. 在脚本中引用 `ToolKits` 命名空间
2. 使用 `GizmosExtensions` 类中的静态方法进行绘制
3. 可以在 `OnDrawGizmos` 或 `OnDrawGizmosSelected` 方法中调用

## 技术细节

- 使用Unity的Gizmos API进行底层绘制
- 支持矩阵变换实现复杂的旋转和缩放
- 提供对BoxCollider和SphereCollider的自动可视化
- 使用数学计算实现精确的几何形状绘制

## 文件说明

- `GizmosExtensions.cs`: 主要实现文件，包含所有绘制方法
- `GizmosCircle.cs`: 圆形绘制的具体实现

## 代码示例

```csharp
// 绘制箭头
GizmosExtensions.DrawArrow(Vector3.zero, Vector3.forward * 2f);

// 绘制带旋转的线框立方体
GizmosExtensions.DrawWireCube(transform.position, Vector3.one, Quaternion.Euler(45f, 45f, 45f));

// 绘制圆形
GizmosExtensions.DrawWireCircle(transform.position, 1f, 32);
```

## 主要方法说明

- `DrawWireCube`: 绘制线框立方体，支持位置、大小和旋转
- `DrawWireSphere`: 绘制线框球体，支持位置、半径和旋转
- `DrawArrow`: 绘制箭头，可自定义箭头大小和角度
- `DrawWireCircle`: 绘制圆形，可指定分段数
- `DrawWireArc`: 绘制圆弧，支持不同的绘制方式
- `DrawWireCylinder`: 绘制圆柱体，支持高度和旋转
- `DrawWireCapsule`: 绘制胶囊体，包含圆柱体和半球端部

## 注意事项

- 所有绘制方法仅在Scene视图中可见
- 绘制操作应在适当的Unity生命周期方法中调用
- 复杂形状的绘制可能会影响编辑器性能
- 建议根据需要调整分段数量以平衡性能和视觉效果

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 