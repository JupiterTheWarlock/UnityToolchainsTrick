# Unity场景视图层级锁定工具

这个示例展示了如何在Unity编辑器中实现场景视图的层级锁定功能，可以防止特定层级的对象被意外选中或修改。

## 功能特点

- 锁定指定层级对象
- 解锁指定层级对象
- 切换层级锁定状态
- 查询层级锁定状态
- 支持位运算操作
- 默认层级快速锁定/解锁

## 使用方法

1. 在Unity编辑器菜单中选择：
   - `Tools -> SceneViewLock -> LockDefault` 锁定默认层级
   - `Tools -> SceneViewLock -> UnLockDefault` 解锁默认层级
2. 或者通过代码调用相应方法：
   - `LockLayer(layer)` 锁定指定层级
   - `UnLockLayer(layer)` 解锁指定层级
   - `SwichLockLayer(layer)` 切换锁定状态
   - `IsLayerLocked(layer)` 检查锁定状态

## 技术细节

- 使用 `Tools.lockedLayers` 控制层级锁定
- 通过位运算实现层级状态管理
- 支持 `LayerMask` 层级转换
- 提供完整的层级操作API
- 支持运行时动态控制

## 代码示例

```csharp
// 锁定指定层级
public static void LockLayer(int layer)
{
    Tools.lockedLayers |= 1 << layer;
}

// 解锁指定层级
public static void UnLockLayer(int layer)
{
    Tools.lockedLayers &= ~(1 << layer);
}

// 切换锁定状态
public static void SwichLockLayer(int layer)
{
    Tools.lockedLayers ^= 1 << layer;
}
```

## 实现原理

1. 使用位运算管理32个层级的状态
2. 通过位移操作定位目标层级
3. 使用位与、位或、异或等操作控制状态
4. 利用Unity内置的Tools.lockedLayers属性

## 注意事项

- 注意层级编号范围（0-31）
- 确保层级名称正确配置
- 锁定后的对象无法在Scene视图选中
- 可能影响编辑器操作流程
- 建议在必要时才启用锁定

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 