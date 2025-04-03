# Unity GUI样式预览工具 (GUIStyles Preview)

这个工具是一个Unity编辑器扩展，用于预览和浏览Unity编辑器中所有内置的GUI样式（GUIStyle）。它可以帮助开发者快速查看和使用Unity提供的各种GUI样式。

## 功能特点

- 预览所有Unity内置的GUI样式
- 实时展示样式的激活（active）和非激活（inactive）状态
- 支持样式名称搜索功能
- 支持样式名称一键复制
- 自适应窗口大小的布局系统
- 垂直滚动条支持

## 使用方法

1. 在Unity编辑器中，通过菜单 `Tools > GUIStyles Preview` 打开预览窗口
2. 在顶部搜索框中输入关键字可以过滤样式
3. 点击样式名称可以复制该样式的代码引用（格式：`(GUIStyle)"样式名称"`）
4. 每个样式都显示了其激活和非激活状态的效果
5. 使用右侧滚动条可以浏览更多样式

## 技术说明

- 工具自动获取 `GUI.skin` 中的所有可用样式
- 动态计算并优化样式预览的布局
- 支持窗口大小调整时的实时重排
- 实现了高效的样式渲染和内存管理

## 文件说明

- `GUIStylesPreview.cs`: 主要实现文件，包含所有功能代码
- `GUIStylesPreview.cs.meta`: Unity生成的元数据文件

## 使用示例

```csharp
// 在代码中使用预览工具中看到的样式
GUIStyle style = GUI.skin.GetStyle("样式名称");
// 或者
GUIStyle style = (GUIStyle)"样式名称";
```

## 注意事项

- 此工具仅在Unity编辑器中可用，不可在运行时使用
- 部分样式的显示效果可能因Unity版本不同而存在差异
- 建议将窗口调整到合适的大小以获得最佳预览效果

## 开发环境

- Unity 2019.4 或更高版本
- 需要在Editor文件夹下使用 