# Unity时间控制器 (Time Control Tool)

这个工具提供了一个类似于Unity动画窗口的时间控制器界面，可用于控制和预览各种基于时间的操作。它实现了播放、暂停、拖拽时间轴等功能，是制作编辑器工具时常用的时间控制组件。

## 功能特点

- 提供播放/暂停控制
- 支持时间轴拖拽控制
- 实现循环播放功能
- 支持键盘箭头键控制
- 可调节播放速度
- 提供时间标记显示
- 支持自定义时间范围
- 包含完整的事件回调系统

## 使用方法

1. 在Unity编辑器中，通过菜单 `Tools > TimeControlWindow` 打开示例窗口
2. 时间控制器提供以下功能：
   - 点击播放/暂停按钮控制播放状态
   - 拖动时间轴改变当前时间
   - 使用左右箭头键微调时间
   - 实时显示播放进度

## 技术说明

- 使用 `EditorWindow` 创建自定义编辑器窗口
- 实现了完整的鼠标和键盘输入控制
- 支持自定义时间范围和播放速度
- 提供规范化时间计算
- 包含播放状态变化和播放结束事件

## 文件说明

- `TimeControlWindow.cs`: 时间控制器窗口实现
- `TimeControl.cs`: 时间控制器核心功能实现

## 代码示例

```csharp
// 创建时间控制器
TimeControl timeControl = new TimeControl();

// 设置时间范围
timeControl.startTime = 0.0f;
timeControl.stopTime = 10.0f;

// 设置播放选项
timeControl.loop = true;
timeControl.playbackSpeed = 1.0f;

// 注册事件回调
timeControl.PlayStatusChanged = (isPlaying) => {
    Debug.Log($"播放状态改变: {isPlaying}");
};

timeControl.OnPlayEnd = () => {
    Debug.Log("播放结束");
};
```

## 自定义选项

```csharp
// 时间控制器的默认配置
private static readonly Vector2 MIN_SIZE = new Vector2(400, 300);
private static readonly Rect TIME_RECR = new Rect(20, 20, 300, 50);

// 时间步进值
private const float kStepTime = 0.01f;

// UI元素尺寸
private const float kScrubberHeight = 21;
private const float kPlayButtonWidth = 33;
```

## 注意事项

- 此工具仅在Unity编辑器中可用
- 时间控制需要在OnGUI中更新
- 建议在Repaint事件中更新时间状态
- 可以通过继承扩展更多功能
- 注意处理窗口关闭时的清理工作

## 开发环境

- Unity 2019.4 或更高版本
- 需要在Editor文件夹下使用

## 扩展功能

- 支持自定义时间显示格式
- 可以添加更多播放控制选项
- 支持时间刻度标记自定义
- 可以集成到其他编辑器工具中
- 提供完整的状态控制接口 