# Unity高级下拉菜单属性工具

这个示例展示了如何在Unity中创建自定义的高级下拉菜单属性，用于资源引用的选择。

## 功能特点

- 自定义属性特性
- 支持资源引用选择
- 自定义Inspector界面
- 支持Texture类型资源
- 可扩展到其他资源类型
- 简化资源引用设置

## 使用方法

1. 在脚本中添加 `[AssetReference]` 特性：
```csharp
[AssetReference] public Texture TestTexture;
```

2. 在Inspector中：
   - 点击属性字段显示下拉菜单
   - 选择需要引用的资源
   - 自动设置资源引用

## 技术细节

- 继承 `PropertyAttribute` 创建自定义特性
- 使用 `MonoBehaviour` 组件展示属性
- 支持资源类型检查和过滤
- 提供简洁的API接口
- 可自定义下拉菜单样式

## 实现原理

1. 定义自定义属性特性
2. 创建属性绘制器
3. 实现资源选择逻辑
4. 处理资源引用设置
5. 更新Inspector界面

## 扩展方向

- 支持更多资源类型
- 添加资源预览功能
- 实现资源过滤器
- 添加搜索功能
- 支持多选模式

## 注意事项

- 确保资源类型匹配
- 处理空引用情况
- 注意资源加载性能
- 保持界面响应性
- 添加错误处理机制

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 