# Unity场景可见性管理工具

这个示例展示了如何在Unity编辑器中管理场景对象的可见性和拾取状态。

## 功能特点

- 控制对象显示/隐藏
- 管理对象拾取状态
- 支持批量操作
- 状态切换功能
- 状态查询功能
- 支持层级结构
- 实时状态更新

## 使用方法

1. 在Unity编辑器菜单中选择 `Tools -> SceneVisibility`，包含以下功能：
   - `Show`: 显示指定对象
   - `Hide`: 隐藏指定对象
   - `ShowAll`: 显示所有对象
   - `HideAll`: 隐藏所有对象
   - `DisablePicking`: 禁用对象拾取
   - `EnablePicking`: 启用对象拾取
   - `TogglePicking`: 切换拾取状态
   - `ToggleVisibility`: 切换可见性
   - `IsHidden`: 检查隐藏状态
   - `IsPickingDisabled`: 检查拾取状态

## 技术细节

- 使用 `SceneVisibilityManager` 管理可见性
- 支持对象层级操作
- 提供完整的状态管理API
- 实时更新场景视图
- 自动处理子对象状态

## 代码示例

```csharp
// 显示/隐藏对象
SceneVisibilityManager.instance.Show(gameObject, true);
SceneVisibilityManager.instance.Hide(gameObject, true);

// 管理拾取状态
SceneVisibilityManager.instance.DisablePicking(gameObject, true);
SceneVisibilityManager.instance.EnablePicking(gameObject, true);

// 状态切换
SceneVisibilityManager.instance.ToggleVisibility(gameObject, true);
SceneVisibilityManager.instance.TogglePicking(gameObject, true);

// 状态查询
bool isHidden = SceneVisibilityManager.instance.IsHidden(gameObject, true);
bool isPickingDisabled = SceneVisibilityManager.instance.IsPickingDisabled(gameObject, true);
```

## 实现原理

1. 可见性控制
   - 管理对象显示状态
   - 处理层级关系
   - 更新场景视图
   - 保持状态一致性

2. 拾取管理
   - 控制对象选择状态
   - 处理鼠标事件
   - 管理交互行为
   - 维护拾取状态

3. 状态同步
   - 实时更新显示
   - 同步层级状态
   - 处理状态变化
   - 保持数据一致

## 应用场景

1. 场景编辑
   - 临时隐藏对象
   - 简化场景编辑
   - 提高工作效率
   
2. 调试工具
   - 快速隔离对象
   - 检查场景结构
   - 优化编辑体验
   
3. 开发辅助
   - 简化对象选择
   - 提高编辑效率
   - 改善工作流程

## 注意事项

- 正确处理层级关系
- 注意性能影响
- 处理状态冲突
- 维护状态一致性
- 考虑撤销/重做支持

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 