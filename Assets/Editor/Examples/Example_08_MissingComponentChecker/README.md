# Unity组件丢失检查工具 (Missing Component Checker)

这个工具用于检查Unity项目中预制体上是否存在丢失的组件（Missing Components）。它可以递归检查预制体及其子物体上的所有组件，帮助开发者快速定位和发现丢失的组件引用。

## 功能特点

- 自动检查指定目录下所有预制体的组件
- 递归检查预制体的子物体
- 显示组件丢失的完整路径
- 使用进度条显示检查进度
- 使用彩色日志输出检查结果
- 检查完成后显示提示对话框

## 使用方法

1. 在Unity编辑器中，通过菜单 `Tools > CheckMissingComponent` 启动检查
2. 工具会自动检查 `Assets/Editor/Examples/Example_08_MissingComponentChecker/Prefabs` 目录下的所有预制体
3. 检查过程中会显示进度条
4. 检查结果会在Console窗口中以彩色日志形式显示：
   - 绿色：丢失组件的游戏对象路径
   - 蓝色：预制体资源路径
5. 检查完成后会显示提示对话框

## 技术说明

- 使用 `AssetDatabase` API 查找和加载预制体
- 使用 `GetComponents<Component>()` 获取所有组件
- 实现了递归检查预制体层级结构
- 通过路径构建显示对象的完整层级关系
- 使用彩色日志增强输出的可读性

## 文件说明

- `MissingComponentChecker.cs`: 实现组件检查功能的主要代码文件

## 代码示例

```csharp
// 检查对象上的所有组件
var cmps = gameObject.GetComponents<Component>();
for (int i = 0; i < cmps.Length; i++)
{
    if (null == cmps[i])
    {
        Debug.LogError(
            $"<color={PrefabNameColor}>{GetRelativePath(gameObject, prefab)}</color> has missing components! path is: <color={PathColor}>{path}</color>"
        );
    }
}
```

## 注意事项

- 此工具仅在Unity编辑器中可用
- 检查路径已硬编码为特定目录，使用前需要确认路径是否正确
- 建议在项目整理或版本提交前运行检查
- 大型项目中检查可能需要一定时间，请耐心等待
- 组件丢失通常是由于以下原因造成：
  - 脚本文件被删除或移动
  - 脚本类名称被修改
  - 程序集引用错误

## 开发环境

- Unity 2019.4 或更高版本
- 需要在Editor文件夹下使用 