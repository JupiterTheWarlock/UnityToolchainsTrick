# Unity扩展Transform编辑器工具

这个示例展示了如何扩展Unity的Transform组件编辑器，添加更多实用功能和更好的用户体验。

## 功能特点

- 扩展Transform Inspector界面
- 支持位置、旋转、缩放的快速重置
- 提供坐标复制功能
- 支持多对象编辑
- 自定义编辑器样式
- 支持拖拽缩放操作
- 提供右键菜单扩展
- 支持浅色/深色主题

## 使用方法

1. 选择场景中的任意GameObject
2. 在Inspector中查看扩展的Transform组件：
   - 使用重置按钮快速归零
   - 点击复制按钮复制坐标值
   - 拖拽缩放区域进行比例缩放
   - 使用右键菜单访问额外功能

## 技术细节

- 使用 `CustomEditor` 特性扩展Transform编辑器
- 通过 `SerializedProperty` 访问Transform属性
- 实现自定义GUI控件和样式
- 支持编辑器主题切换
- 提供完整的坐标系操作API

## 代码示例

```csharp
[CustomEditor(typeof(Transform)), CanEditMultipleObjects]
public class ExtendedTransformEditor : Editor
{
    private void OnInspectorGUI()
    {
        using (new EditorGUILayout.HorizontalScope())
        {
            EditorGUILayout.PropertyField(properties.Position, Content.Position);
            using (new EditorGUI.DisabledGroupScope(
                properties.Position.vector3Value == Vector3.zero))
            {
                if (GUILayout.Button(Content.ResetPosition, Styles.ResetButton))
                    properties.Position.vector3Value = Vector3.zero;
            }
        }
    }
}
```

## 功能列表

1. 基础变换操作
   - 位置编辑
   - 旋转编辑
   - 缩放编辑
   
2. 快捷功能
   - 一键重置
   - 坐标复制
   - 比例拖拽
   
3. 右键菜单
   - 随机旋转
   - 对齐地面
   - 自定义操作

## 注意事项

- 注意多对象编辑时的数值同步
- 处理坐标系转换的精度问题
- 合理使用SerializedProperty
- 注意编辑器性能优化
- 保持UI布局的一致性

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 