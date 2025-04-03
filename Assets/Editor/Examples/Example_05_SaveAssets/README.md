# Unity资源保存示例 (SaveAssets Example)

这个示例展示了如何在Unity编辑器中创建一个自定义窗口来编辑和保存ScriptableObject资源。通过这个示例，你可以学习到如何在编辑器中实时修改和保存资源数据。

## 功能特点

- 创建自定义编辑器窗口
- 实时编辑ScriptableObject数据
- 演示EditorGUI的基本使用
- 展示资源的保存和刷新机制
- 使用不同颜色区分界面元素

## 使用方法

1. 在Unity编辑器中，通过菜单 `Tools > 资源保存测试窗口` 打开测试窗口
2. 在窗口中可以修改以下属性：
   - 姓名（Name）：字符串类型
   - 年龄（Age）：整数类型
3. 点击"保存"按钮将修改保存到资源文件中

## 技术说明

- 使用 `ScriptableObject` 存储数据
- 通过 `EditorWindow` 创建自定义编辑器窗口
- 使用 `EditorGUI` 创建编辑器界面
- 实现了数据的实时更新和保存机制
- 展示了如何使用 `EditorUtility.SetDirty()` 和 `AssetDatabase.SaveAssets()` 保存资源

## 文件说明

- `Example05Window.cs`: 编辑器窗口实现
- `ExampleScriptableObject.cs`: 数据对象定义
- `ExampleAssets.asset`: 实际存储数据的资源文件

## 代码示例

```csharp
// 标记资源为已修改状态
EditorUtility.SetDirty(setting);
// 保存所有修改的资源
AssetDatabase.SaveAssets();
// 刷新资源数据库
AssetDatabase.Refresh();
```

## 注意事项

- 此示例仅在Unity编辑器中可用
- 修改后需要点击保存按钮才会永久保存更改
- 资源文件保存在 `Assets/Editor/Examples/Example_05_SaveAssets/` 目录下

## 开发环境

- Unity 2019.4 或更高版本
- 需要在Editor文件夹下使用 