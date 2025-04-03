# Unity预制体丢失检查工具 (Missing Prefab Checker)

这个工具用于检查Unity项目中预制体的引用是否完整，帮助开发者快速定位和发现丢失的预制体引用。它可以递归检查预制体及其子物体，确保所有预制体引用都是有效的。

## 功能特点

- 自动检查指定目录下所有预制体
- 递归检查预制体的子物体
- 支持检查预制体断开连接的情况
- 使用进度条显示检查进度
- 使用彩色日志输出检查结果
- 支持多种预制体丢失情况的检测

## 使用方法

1. 在Unity编辑器中，通过菜单 `Tools > CheckMissingPrefab` 启动检查
2. 工具会自动检查 `Assets/Editor/Examples/Example_07_MissingPrefabChecker/Prefabs` 目录下的所有预制体
3. 检查过程中会显示进度条
4. 检查结果会在Console窗口中以彩色日志形式显示：
   - 绿色：当前检查的预制体名称
   - 红色：丢失的预制体名称

## 技术说明

- 使用 `AssetDatabase` API 查找和加载预制体
- 使用 `PrefabUtility` API 检查预制体状态
- 实现了递归检查预制体层级结构
- 支持以下检查项：
  - Missing Prefab标记
  - 预制体资源丢失
  - 预制体断开连接

## 文件说明

- `MissingPrefabChecker.cs`: 实现预制体检查功能的主要代码文件

## 代码示例

```csharp
// 检查预制体是否丢失
if (PrefabUtility.IsPrefabAssetMissing(gameObject))
{
    Debug.LogError($"<color={PrefabNameColor}>{prefabName}</color> has missing prefab <color={SubPrefabNameColor}>{gameObject.name}</color>");
    return;
}

// 检查预制体是否断开连接
if (PrefabUtility.IsDisconnectedFromPrefabAsset(gameObject))
{
    Debug.LogError($"<color={PrefabNameColor}>{prefabName}</color> has missing prefab <color={SubPrefabNameColor}>{gameObject.name}</color>");
    return;
}
```

## 注意事项

- 此工具仅在Unity编辑器中可用
- 检查路径已硬编码为特定目录，使用前需要确认路径是否正确
- 建议在项目整理或版本提交前运行检查
- 大型项目中检查可能需要一定时间，请耐心等待

## 开发环境

- Unity 2019.4 或更高版本
- 需要在Editor文件夹下使用 