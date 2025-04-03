# Unity Avatar预览工具 (Avatar Preview Tool)

这个工具提供了一个强大的Avatar（角色模型）预览窗口，可以在编辑器中实时预览角色模型和动画。它支持人形动画预览、IK控制、2D/3D视图切换等多种功能。

## 功能特点

- 实时预览角色模型和动画
- 支持动画播放控制（播放、暂停、循环）
- 提供2D和3D预览模式
- 支持IK（反向运动学）预览
- 可调整预览视角和缩放
- 显示角色pivot点和重心
- 支持地面网格和阴影显示
- 自定义预览速度控制

## 使用方法

1. 在Unity编辑器中，通过菜单 `Tools > PreviewWindow` 打开预览窗口
2. 点击"加载预览"按钮加载预设的角色模型和动画
3. 预览窗口提供以下功能：
   - 使用鼠标左键拖动旋转视角
   - 使用鼠标右键或Alt+左键平移视图
   - 使用鼠标滚轮或Alt+右键缩放
   - 使用工具栏按钮切换各种预览选项

## 技术说明

- 使用 `PreviewRenderUtility` 实现预览渲染
- 集成 `AnimatorController` 系统控制动画
- 支持动画帧率和时间控制
- 实现了自定义预览相机控制
- 提供完整的预览场景光照系统
- 支持动画状态机的预览控制

## 文件说明

- `PreviewWindow.cs`: 预览窗口的主要实现
- `AvatarPreview.cs`: Avatar预览功能的核心实现

## 配置说明

```csharp
// 预览窗口的默认配置
private static readonly Vector2 MIN_SIZE = new Vector2(600, 400);
private static readonly Rect PREVIEW_RECT = new Rect(0, 50, 500, 300);

// 预设资源路径
private const string PREVIEW_ANIMCONTROLLER_PATH = "Assets/GameAssets/Arts/AnimatorControllers/PreviewController.controller";
private const string AVATAR_PATH = "Assets/GameAssets/Arts/Prefabs/Warrior.prefab";
private const string CLIP_PATH = "Assets/GameAssets/Arts/Models/AnimationClips/Female/1HIdle.anim";
```

## 注意事项

- 此工具仅在Unity编辑器中可用
- 使用前需要确保相关资源路径配置正确
- 预览实例会在窗口关闭时自动清理
- 支持的动画类型取决于角色的动画设置
- 大型模型可能需要较长加载时间

## 开发环境

- Unity 2019.4 或更高版本
- 需要在Editor文件夹下使用

## 扩展功能

- 支持自定义动画控制器
- 可以通过代码修改预览参数
- 支持多种预览模式切换
- 提供完整的事件回调系统 