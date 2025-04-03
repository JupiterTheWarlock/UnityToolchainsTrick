# Unity友元访问内部API工具

这个示例展示了如何使用C#的友元特性来访问Unity的内部API，实现对Unity引擎内部功能的扩展。

## 功能特点

- 友元特性访问
- 内部API调用
- 跨程序集访问
- 版本兼容性
- 安全性保证
- 性能优化
- 扩展性支持

## 使用方法

1. 添加友元引用：
   - 在项目中引用 `Unity.InternalAPIEngineBridge.006`
   - 确保Unity版本在2018.1或更高

2. 访问内部API：
   - 使用友元程序集访问Unity内部API
   - 调用PlayerSettings相关功能
   - 扩展Unity编辑器功能

## 技术细节

- 使用C#友元特性
- 访问Unity内部类型
- 处理版本兼容性
- 提供安全访问机制
- 支持编辑器扩展

## 代码示例

```csharp
// 使用友元访问示例
using UnityEngine;

namespace UnityToolchinsTrick
{
    public class UseBind
    {
        void Use()
        {
            // 访问PlayerSettings内部API
            Debug.Log(PlayerSettingBind.PlayerSettingDefineSplits);
        }
    }
}
```

## 实现原理

1. 友元机制
   - 程序集标记
   - 访问权限控制
   - 版本检查
   - 安全性验证

2. API访问
   - 内部类型映射
   - 方法调用转发
   - 异常处理
   - 性能优化

3. 版本管理
   - 兼容性检查
   - API版本控制
   - 降级处理
   - 更新机制

## 应用场景

1. 编辑器扩展
   - 自定义工具开发
   - 工作流程优化
   - 功能定制开发
   
2. 调试工具
   - 内部状态查看
   - 性能分析
   - 问题诊断
   
3. 功能增强
   - 编辑器功能扩展
   - 新特性开发
   - 工具链集成

## 注意事项

- 版本兼容性检查
- 异常处理机制
- 性能影响评估
- 安全性考虑
- API稳定性验证

## 相关资源

- [Unity友元文档](https://docs.microsoft.com/zh-cn/dotnet/standard/assembly/friend)
- [Unity内部API列表](https://github.com/Unity-Technologies/UnityCsReference/blob/2018.1/Editor/Mono/AssemblyInfo/AssemblyInfo.cs)
- Unity版本：2018.1及以上
- 支持的友元程序集：InternalAPIEditorBridge系列

## 开发环境要求

- Unity 2018.1或更高版本
- .NET Framework 4.x