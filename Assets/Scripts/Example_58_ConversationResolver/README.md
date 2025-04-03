# Unity对话系统解析器

这个示例展示了如何实现一个灵活的对话系统解析器，支持命令系统和文本解析功能。

## 功能特点

- 文本对话解析
- 命令系统支持
- 正则表达式解析
- 自定义命令注册
- 命令参数处理
- 实时对话执行
- 可扩展的命令系统

## 使用方法

1. 对话文本格式：
```
command1(param1,param2) command2(param3):这是对话内容
command3:这是另一段对话
```

2. 添加到场景：
   - 将`ConversationManager`组件添加到场景对象
   - 将`ConversationTest`组件添加到同一对象

3. 编写对话：
   - 在ConversationTest组件的文本区域编写对话内容
   - 使用正确的命令格式和参数

## 技术细节

- 使用正则表达式解析对话文本和命令
- 支持命令参数的解析和处理
- 提供命令注册和执行机制
- 实现对话内容的实时处理

## 代码示例

```csharp
// 定义命令
[CommandName("wait")]
public class WaitCommand : IConversationCommand
{
    float waitTime;

    public void SetUp(string[] _params)
    {
        waitTime = float.Parse(_params[0]);
    }

    public void Process()
    {
        // 执行等待逻辑
    }
}

// 使用示例
string dialogText = "wait(2):这是一段等待2秒的对话";
conversationManager.BeginConversation(dialogText);
```

## 实现原理

1. 文本解析
   - 使用正则表达式分离命令和对话
   - 解析命令参数
   - 处理特殊字符

2. 命令系统
   - 命令注册机制
   - 参数解析处理
   - 命令执行流程
   - 错误处理

3. 对话管理
   - 对话队列处理
   - 命令调度执行
   - 状态管理
   - 事件通知

## 应用场景

1. 游戏对话系统
   - 剧情对话
   - NPC交互
   - 任务系统
   
2. 教程系统
   - 引导流程
   - 操作说明
   - 帮助提示
   
3. 剧情控制
   - 场景切换
   - 事件触发
   - 动画控制

## 注意事项

- 正确处理命令格式
- 注意参数类型转换
- 处理特殊字符
- 管理命令执行顺序
- 处理异常情况

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 