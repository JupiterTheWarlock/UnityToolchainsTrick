# Unity对象图标设置工具

这个示例展示了如何在Unity编辑器中为游戏对象设置自定义图标。

## 功能特点

- 支持设置内置图标
- 支持多种图标类型
- 实时预览效果
- 批量设置功能
- 支持图标重置
- 自动刷新显示
- 支持层级视图显示

## 使用方法

1. 在Unity编辑器菜单中选择 `Tools -> SetObjectIconDemo`
2. 选择要设置图标的游戏对象
3. 通过API设置不同类型的图标：
   - 标签图标 (sv_label_0 - sv_label_7)
   - 名称图标 (sv_icon_name0 - sv_icon_name7)
   - 点状图标 (sv_icon_dot0_sml - sv_icon_dot15_sml)
   - 像素图标 (sv_icon_dot0_pix16_gizmo - sv_icon_dot15_pix16_gizmo)

## 技术细节

- 使用反射访问Unity内部API
- 扩展 `EditorGUIUtility` 功能
- 支持自定义图标设置
- 提供完整的图标管理API
- 自动处理图标资源加载

## 代码示例

```csharp
// 设置错误图标
EditorGUIExtension.SetIcon(gameObject, "console.erroricon");

// 设置标签图标
EditorGUIExtension.SetIcon(gameObject, "sv_label_3");

// 设置名称图标
EditorGUIExtension.SetIcon(gameObject, "sv_icon_name5");

// 设置点状图标
EditorGUIExtension.SetIcon(gameObject, "sv_icon_dot8_sml");
```

## 实现原理

1. 获取Unity内置图标资源
2. 使用反射调用内部方法
3. 设置对象图标
4. 刷新编辑器视图
5. 处理图标显示

## 图标类型

1. 标签图标
   - 8种不同样式
   - 适合分类标记
   - 清晰可识别
   
2. 名称图标
   - 8种不同样式
   - 适合对象命名
   - 支持自定义颜色
   
3. 点状图标
   - 16种不同样式
   - 适合状态标记
   - 支持不同尺寸

4. 像素图标
   - 16种不同样式
   - 适合精确显示
   - 支持Gizmo显示

## 注意事项

- 图标名称必须正确
- 注意内存资源管理
- 处理图标加载失败
- 考虑编辑器性能
- 正确使用反射API

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 