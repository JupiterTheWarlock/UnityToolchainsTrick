# Unity场景视图扩展工具

这个示例展示了如何扩展Unity场景视图的功能，添加自定义的快捷键和视角控制功能。

## 功能特点

- 扩展Scene视图的交互功能
- 添加自定义快捷键控制
- 支持FPS模式下的视角旋转
- 可通过编辑器偏好设置开启/关闭
- 平滑的旋转控制

## 使用方法

1. 在Unity编辑器的Preferences中启用Scene视图扩展
2. 在Scene视图中切换到FPS模式（默认快捷键为F）
3. 使用以下快捷键控制视角：
   - F键：向左旋转视角
   - G键：向右旋转视角

## 技术细节

- 使用 `SceneView.duringSceneGui` 事件监听场景视图更新
- 通过 `EditorPrefs` 保存扩展功能的开启状态
- 使用 `InitializeOnLoadMethod` 特性确保编辑器启动时初始化
- 支持实时视角旋转控制
- 可配置的旋转速度

## 文件说明

- `SceneViewExtension.cs`: 主要实现文件，包含所有场景视图扩展功能

## 代码示例

```csharp
[InitializeOnLoadMethod]
public static void EditorInitialize()
{
    SceneView.duringSceneGui -= Update;
    if (EditorPrefs.GetBool(Constants.SCENE_VIEW_EXTENSITON_SWITH, false))
    {
        SceneView.duringSceneGui += Update;
    }
}

private static void Update(SceneView sceneView)
{
    var e = Event.current;
    if (null != e && Tools.viewTool == ViewTool.FPS)
    {
        if (e.keyCode == KeyCode.F)
        {
            var lastAngle = SceneView.lastActiveSceneView.rotation.eulerAngles;
            var newAngle = new Vector3(lastAngle.x, lastAngle.y, lastAngle.z - RotateSpeed);
            SceneView.lastActiveSceneView.rotation = Quaternion.Euler(newAngle);
        }
    }
}
```

## 注意事项

- 扩展功能需要在Preferences中手动启用
- 仅在FPS模式下生效
- 旋转速度可以通过修改 `RotateSpeed` 变量调整
- 确保不与Unity默认快捷键冲突
- 建议在使用时关闭其他可能干扰的工具

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 