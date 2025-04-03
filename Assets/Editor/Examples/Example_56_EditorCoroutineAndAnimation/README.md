# Unity编辑器协程与动画工具

这个示例展示了如何在Unity编辑器中实现协程和动画效果，包括丰富的缓动函数库和动画预览功能。

## 功能特点

- 编辑器协程支持
- 丰富的缓动函数库
- 实时动画预览
- 可视化参数调整
- 多种动画曲线
- 动态缩放效果
- 自定义锚点控制

## 使用方法

1. 打开编辑器窗口：
   - 在Unity菜单栏选择 `Tools/编辑器协程和动画`
   - 将显示动画预览窗口

2. 调整动画参数：
   - 选择缓动类型（EasingType）
   - 调整锚点位置（Pivot）
   - 观察实时缩放效果
   - 查看动画曲线变化

## 技术细节

- 使用 `EditorCoroutine` 实现编辑器协程
- 实现33种缓动函数
- 支持自定义动画曲线
- 提供实时预览功能
- 集成编辑器GUI控制

## 代码示例

```csharp
public class EditorCoroutineWindow : BasicEditorWindow
{
    Vector2 pivot = new Vector2(0.5f, 0.5f);
    float scale;
    Rect r = new Rect(200, 300, 300, 300);
    EasingType easingType;

    private void OnEnable()
    {
        StartCoroutine(Test());
    }

    IEnumerator Test()
    {
        while (true)
        {
            scale = Easing.Tween(0, 1, (float)(EditorApplication.timeSinceStartup % 2 / 2), easingType);
            Repaint();
            yield return null;
        }
    }
}

// 缓动函数示例
public static float EaseInQuad(float start, float end, float t)
{
    end -= start;
    return end * t * t + start;
}
```

## 实现原理

1. 协程系统
   - 编辑器协程实现
   - 时间控制
   - 状态管理
   - 生命周期控制

2. 缓动系统
   - 函数注册
   - 参数计算
   - 曲线插值
   - 实时更新

3. 动画控制
   - 缩放计算
   - 锚点处理
   - GUI绘制
   - 实时刷新

## 缓动类型

1. 基础缓动
   - Linear（线性）
   - Clerp（圆形插值）
   - Spring（弹簧）

2. 数学函数
   - Quad（二次方）
   - Cubic（三次方）
   - Quart（四次方）
   - Quint（五次方）

3. 特殊效果
   - Bounce（弹跳）
   - Elastic（弹性）
   - Back（回退）
   - Expo（指数）

## 应用场景

1. 编辑器工具
   - 动画预览
   - 参数调整
   - 效果测试
   
2. 界面动画
   - UI过渡
   - 元素动画
   - 视觉反馈
   
3. 开发辅助
   - 动画调试
   - 参数微调
   - 效果验证

## 注意事项

- 合理控制协程更新频率
- 注意动画性能开销
- 处理窗口关闭时的协程清理
- 考虑编辑器刷新时机
- 避免过度使用复杂曲线

## 扩展建议

1. 功能扩展：
   - 添加动画录制
   - 支持关键帧编辑
   - 导出动画曲线
   - 批量动画预览

2. 界面优化：
   - 曲线预览
   - 参数预设
   - 动画轨道
   - 时间轴控制

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 