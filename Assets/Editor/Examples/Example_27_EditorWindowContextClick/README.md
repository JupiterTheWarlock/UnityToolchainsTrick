# Unity编辑器窗口右键菜单工具

这个示例展示了如何在Unity编辑器窗口中实现右键菜单功能，包括多级菜单和分隔符。

## 功能特点

- 自定义编辑器窗口
- 支持右键弹出菜单
- 支持多级菜单结构
- 可添加菜单分隔符
- 自定义菜单项回调
- 设置最小窗口尺寸

## 使用方法

1. 在Unity编辑器菜单中选择 `Tools -> EditorWindowContextClick`
2. 在打开的窗口中右键点击
3. 在弹出的菜单中选择：
   - "功能1"
   - "功能合集/功能2"
   - "功能合集/功能3"
   - "功能合集/功能4"
4. 在控制台查看菜单响应信息

## 技术细节

- 继承 `EditorWindow` 实现自定义窗口
- 使用 `Event.current` 检测鼠标事件
- 通过 `GenericMenu` 创建右键菜单
- 支持菜单项分组和分隔符
- 实现菜单项的回调函数

## 代码示例

```csharp
private void OnGUI()
{
    var e = Event.current;
    if (null != e)
    {
        if (e.type == EventType.MouseDown && e.button == 1)
        {
            var genericMenu = new GenericMenu();
            genericMenu.AddItem(new GUIContent("功能1"), false, 
                () => { Debug.Log("功能1"); });
            genericMenu.AddItem(new GUIContent("功能合集/功能2"), false, 
                () => { Debug.Log("功能2"); });
            genericMenu.AddSeparator("功能合集/");
            genericMenu.ShowAsContext();
        }
    }
}
```

## 菜单结构

- 功能1
- 功能合集
  - 功能2
  - 功能3
  - --------（分隔符）
  - 功能4

## 注意事项

- 注意处理菜单项的命名冲突
- 合理组织多级菜单结构
- 避免在菜单回调中执行耗时操作
- 确保菜单项名称清晰易懂
- 适当使用分隔符提高可读性

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 