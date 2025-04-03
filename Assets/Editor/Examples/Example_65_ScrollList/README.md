# Unity编辑器滚动列表工具

这个示例展示了如何在Unity编辑器中实现高效的滚动列表功能，扩展EditorGUILayout以支持大量数据的显示和管理。

## 功能特点

- 高效滚动列表
- 虚拟化列表项
- 自定义列表样式
- 动态内容加载
- 性能优化支持
- 自动高度计算
- 滚动位置记忆

## 使用方法

1. 基本使用：
```csharp
scrollPosition = EditorGUILayoutExtension.ScrollList(
    scrollPosition,
    itemCount,
    itemHeight,
    (index, rect) =>
    {
        // 绘制列表项
        EditorGUI.LabelField(rect, $"Item {index}");
    }
);
```

2. 自定义列表项：
```csharp
EditorGUILayoutExtension.ScrollList(
    position,
    items.Count,
    30f, // 项目高度
    (index, rect) =>
    {
        // 自定义绘制逻辑
        GUI.Box(rect, "");
        EditorGUI.ObjectField(rect, items[index], typeof(Object), false);
    }
);
```

## 技术细节

- 虚拟化滚动实现
- 高效内存管理
- 动态项目渲染
- 滚动位置控制

## 实现原理

1. 虚拟化技术
   - 只渲染可见项
   - 动态计算位置
   - 优化内存使用
   - 处理滚动事件

2. 列表管理
   - 项目池管理
   - 高度计算
   - 可见性判断
   - 重用机制

3. 性能优化
   - 渲染优化
   - 事件处理
   - 缓存机制
   - 按需加载

## 应用场景

1. 资源管理
   - 资源列表
   - 对象选择器
   - 配置管理
   
2. 编辑器工具
   - 数据预览
   - 批量操作
   - 日志显示
   
3. 开发辅助
   - 调试信息
   - 状态监控
   - 数据检查

## 注意事项

- 合理设置项目高度
- 处理大量数据
- 优化渲染性能
- 管理滚动状态
- 处理选择事件

## 扩展建议

1. 功能扩展
   - 搜索过滤
   - 排序功能
   - 分组显示
   - 多列支持

2. 交互优化
   - 拖放支持
   - 右键菜单
   - 键盘导航
   - 多选功能

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 