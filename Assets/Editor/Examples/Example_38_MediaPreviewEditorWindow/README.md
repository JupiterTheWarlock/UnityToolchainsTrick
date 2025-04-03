# Unity媒体预览编辑器窗口工具

这个示例展示了如何在Unity编辑器中创建媒体预览窗口，支持视频和图片的预览功能。

## 功能特点

- 支持视频预览
- 支持图片预览
- 自动调整窗口大小
- 居中显示窗口
- 实时预览更新
- 自动资源管理
- 支持窗口关闭回调

## 使用方法

1. 通过API调用显示预览窗口：
   ```csharp
   // 显示视频
   MediaPreviewWindow.ShowVideo("Assets/Videos/example.mp4");
   
   // 显示图片
   MediaPreviewWindow.ShowPic("Assets/Images/example.png");
   ```
2. 窗口特性：
   - 自动调整为媒体内容大小
   - 在主窗口中居中显示
   - 失去焦点自动关闭
   - 支持关闭回调事件

## 技术细节

- 使用 `EditorWindow` 创建预览窗口
- 通过反射调用Unity内部视频API
- 支持多种媒体格式预览
- 提供完整的窗口管理API
- 自动处理资源加载和释放

## 代码示例

```csharp
// 显示视频并处理关闭事件
MediaPreviewWindow.ShowVideo(videoPath, () => {
    Debug.Log("视频窗口已关闭");
});

// 显示图片并处理关闭事件
MediaPreviewWindow.ShowPic(imagePath, () => {
    Debug.Log("图片窗口已关闭");
});
```

## 实现原理

1. 媒体加载
   - 使用 `AssetDatabase` 加载媒体资源
   - 通过反射调用Unity内部API
   - 自动处理资源释放

2. 窗口管理
   - 计算窗口尺寸
   - 居中显示位置
   - 处理窗口事件
   - 管理窗口生命周期

3. 预览控制
   - 视频播放控制
   - 图片显示控制
   - 实时更新预览
   - 自动关闭处理

## 支持格式

1. 视频格式
   - MP4
   - MOV
   - AVI
   - 其他Unity支持的视频格式
   
2. 图片格式
   - PNG
   - JPG
   - TGA
   - 其他Unity支持的图片格式

## 注意事项

- 确保媒体文件路径正确
- 注意内存资源管理
- 处理加载失败情况
- 考虑性能影响
- 正确使用反射API

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 