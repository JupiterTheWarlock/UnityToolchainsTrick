# Unity编辑器图标浏览器 (Editor Icons Browser)

这个工具提供了一个方便的Unity编辑器扩展，用于浏览和查看Unity编辑器中所有可用的内置图标。

## 功能特点

- 支持浏览所有Unity内置编辑器图标
- 提供大图标和小图标两种显示模式
- 包含搜索功能，方便快速查找特定图标
- 支持深色和浅色预览背景切换
- 实时显示选中图标的预览和详细信息

## 使用方法

1. 在Unity编辑器中，通过菜单 `Tools > Editor Icons` 打开图标浏览器窗口
2. 也可以使用快捷键 `Ctrl/Cmd + E` 快速打开窗口
3. 在搜索框中输入关键字可以过滤图标
4. 点击工具栏的 "Small" 或 "Big" 按钮切换图标显示大小
5. 点击任意图标可以在底部查看该图标的预览和详细信息
6. 使用底部的切换按钮可以在深色和浅色背景之间切换预览效果

## 技术说明

- 工具会自动加载Unity编辑器中所有可用的内置图标
- 支持动态调整窗口大小，自适应不同的显示需求
- 针对不同屏幕分辨率进行了优化

## 文件说明

- `EditorIcons.cs`: 主要实现文件，包含所有功能代码
- `EditorIcons.cs.meta`: Unity生成的元数据文件

## 注意事项

- 此工具仅在Unity编辑器中可用，不可在运行时使用
- 部分图标可能因Unity版本不同而存在差异
- 建议将窗口宽度调整到550像素以上以获得最佳使用体验

## 开发环境

- Unity 2019.4 或更高版本
- 需要在Editor文件夹下使用 