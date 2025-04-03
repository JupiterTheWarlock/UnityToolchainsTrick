# Unity隐藏脚本对象名称工具

这个示例展示了如何在Unity Inspector中隐藏ScriptableObject的脚本名称，提供更清晰的资源显示方式。

## 功能特点

- 隐藏脚本名称显示
- 自定义Inspector界面
- 简洁的资源显示
- 编辑器扩展支持
- 可选的显示控制
- 无缝集成
- 易于使用

## 使用方法

1. 创建ScriptableObject：
   - 继承自`HideScriptObjectName`基类
   - 或添加自定义Inspector属性

2. 自定义Inspector：
   ```csharp
   [CustomEditor(typeof(YourScriptableObject))]
   public class YourCustomInspector : HideScriptObjectNameInspector
   {
       // 自定义Inspector内容
   }
   ```

3. 应用效果：
   - 创建资源实例
   - 在Inspector中查看效果
   - 脚本名称将被隐藏

## 技术细节

- 使用CustomEditor特性
- 重写Inspector绘制逻辑
- 提供基类继承支持
- 保持原有功能完整

## 实现原理

1. Inspector定制
   - 重写OnInspectorGUI
   - 控制脚本标题显示
   - 保持其他属性显示
   - 自定义绘制逻辑

2. 编辑器集成
   - 无缝Unity集成
   - 保持原有功能
   - 支持撤销操作
   - 实时更新显示

3. 资源管理
   - 支持预制体
   - 支持场景对象
   - 资源序列化
   - 引用完整性

## 应用场景

1. 资源管理
   - 配置文件
   - 数据容器
   - 资源描述
   
2. 编辑器工具
   - 自定义窗口
   - 工具面板
   - 设置界面
   
3. 开发优化
   - 界面简化
   - 视觉优化
   - 工作流改进

## 注意事项

- 保持Inspector功能完整
- 处理多重继承情况
- 注意序列化支持
- 考虑编辑器兼容性
- 处理特殊属性显示

## 扩展建议

1. 功能扩展
   - 条件显示控制
   - 自定义显示样式
   - 多层级支持
   - 批量处理工具

2. 界面优化
   - 自定义图标
   - 分组显示
   - 折叠支持
   - 搜索功能

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 