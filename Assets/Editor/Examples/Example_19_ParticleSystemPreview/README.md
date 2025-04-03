 # Unity粒子系统预览工具

这个示例展示了如何在Unity编辑器中为GameObject添加粒子系统预览功能，实现更直观的粒子效果预览。

## 功能特点

- 为GameObject Inspector添加粒子系统预览
- 支持多对象选择和编辑
- 可切换预览模式（普通/粒子系统）
- 保留原有GameObject预览功能
- 支持交互式预览控制
- 提供详细的粒子系统信息显示

## 使用方法

1. 选择包含粒子系统的GameObject
2. 在Inspector窗口中查看预览区域
3. 使用PS按钮切换预览模式：
   - 普通预览：显示GameObject默认预览
   - 粒子预览：显示粒子系统效果

## 技术细节

- 继承并扩展Unity的GameObject Inspector
- 使用自定义Editor实现预览功能
- 通过反射调用Unity内部方法
- 支持多种Unity版本的兼容性
- 实现完整的预览生命周期管理

## 文件说明

- `ParticleSystemGameObjectEditor.cs`: 主要编辑器实现
- `ParticleSystemPreview.cs`: 粒子系统预览核心功能
- `ParticleSystemEditorUtilsReflect.cs`: Unity内部方法反射工具
- `OverrideEditor.cs`: 编辑器基类

## 代码示例

```csharp
[CustomEditor(typeof(GameObject)), CanEditMultipleObjects]
public class ParticleSystemGameObjectEditor : OverrideEditor
{
    private ParticleSystemPreview preview
    {
        get
        {
            if (m_Preview == null)
            {
                m_Preview = new ParticleSystemPreview();
                m_Preview.SetEditor(this);
                m_Preview.Initialize(targets);
            }
            return m_Preview;
        }
    }

    public override void OnPreviewGUI(Rect r, GUIStyle background)
    {
        if (IsShowParticleSystemPreview())
        {
            preview.OnPreviewGUI(r, background);
        }
        else
        {
            baseEditor.OnPreviewGUI(r, background);
        }
    }
}
```

## 注意事项

- 需要正确处理预览资源的加载和释放
- 注意多对象编辑时的性能影响
- 预览功能可能受Unity版本影响
- 建议在性能较好的设备上使用
- 大型粒子系统可能影响预览性能

## 开发环境要求

- Unity 2019.1或更高版本
- .NET Framework 4.x
- 建议使用支持GPU的设备