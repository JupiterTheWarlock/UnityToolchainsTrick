# Unity编辑器事件监听工具

这个示例展示了如何监听和处理Unity编辑器中的各种事件，包括层级视图变化、项目视图变化、资源修改等事件。

## 功能特点

- 监听编辑器更新事件
- 监听层级视图变化事件
- 监听项目视图变化事件
- 监听播放模式状态变化
- 监听资源创建、保存、移动和删除事件
- 支持自定义事件处理逻辑

## 使用方法

1. 将脚本添加到项目中
2. 启用 `InitializeOnLoad` 特性（取消注释）
3. 根据需要实现各个事件的处理逻辑
4. 在控制台查看事件触发日志

## 技术细节

### EditorListener类
- 使用 `EditorApplication` 类提供的事件回调
- 支持以下事件监听：
  - `update`: 编辑器更新
  - `hierarchyChanged`: 层级视图变化
  - `projectChanged`: 项目视图变化
  - `playModeStateChanged`: 播放模式状态变化

### MyAssetModificationProcessor类
- 继承自 `UnityEditor.AssetModificationProcessor`
- 提供以下资源修改事件监听：
  - `IsOpenForEdit`: 双击打开资源
  - `OnWillCreateAsset`: 资源创建
  - `OnWillSaveAsset`: 资源保存
  - `OnWillMoveAsset`: 资源移动
  - `OnWillDeleteAsset`: 资源删除

## 代码示例

```csharp
// 监听播放模式状态变化
private static void OnPlayerModeStateChanged(PlayModeStateChange playModeState)
{
    Debug.LogFormat("state:{0} will:{1} isPlaying:{2}", playModeState,
        EditorApplication.isPlayingOrWillChangePlaymode, EditorApplication.isPlaying);
}

// 监听资源移动事件
public static AssetMoveResult OnWillMoveAsset(string oldPath, string newPath)
{
    Debug.LogFormat("Move from:{0} to:{1}", oldPath, newPath);
    return AssetMoveResult.DidMove;
}
```

## 注意事项

- 事件监听可能影响编辑器性能，建议只监听必要的事件
- 在事件处理函数中避免执行耗时操作
- 注意正确处理事件的注册和注销
- 资源修改事件可以通过返回值控制是否允许操作
- 确保在处理事件时不会引发死循环

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 