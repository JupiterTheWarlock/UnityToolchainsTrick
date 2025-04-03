# Unity编辑器输入事件监听工具

这个示例展示了如何在Unity编辑器窗口中监听和处理键盘输入事件，特别是组合键的处理。

## 功能特点

- 监听键盘按键事件
- 支持组合键检测
- 实时响应按键状态
- 支持以下组合键：
  - 空格 + A
  - 空格 + S
  - 空格 + 上箭头
  - 空格 + 下箭头
- 在控制台输出按键信息

## 使用方法

1. 在Unity编辑器菜单中选择 `Tools -> GetInputEventWindow`
2. 在打开的窗口中尝试以下操作：
   - 按住空格，然后按A键
   - 按住空格，然后按S键
   - 按住空格，然后按上箭头
   - 按住空格，然后按下箭头
3. 在控制台查看触发的组合键信息

## 技术细节

- 使用 `EditorWindow` 创建自定义窗口
- 通过 `Event.current` 获取当前事件
- 使用 `EventType` 区分按键按下和释放
- 通过状态变量追踪组合键

## 代码示例

```csharp
private void OnGUI()
{
    Event e = Event.current;
    if (e.isKey)
    {
        if (e.keyCode == KeyCode.Space)
        {
            isSpaceDown = e.type != EventType.KeyUp;
        }

        if (e.type == EventType.KeyUp)
        {
            if (e.keyCode == KeyCode.A && isSpaceDown)
            {
                Debug.LogError("组合键：空格 + A");
            }
        }
    }
}
```

## 实现原理

1. 监听空格键的状态变化
2. 使用 `isSpaceDown` 变量记录空格键是否按下
3. 在空格键按下的状态下检测其他按键
4. 根据不同的按键组合触发相应的操作

## 注意事项

- 确保窗口处于焦点状态才能接收按键事件
- 组合键的检测依赖于按键顺序
- 注意处理按键的按下和释放状态
- 避免在事件处理中执行耗时操作
- 建议添加适当的错误处理机制

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 