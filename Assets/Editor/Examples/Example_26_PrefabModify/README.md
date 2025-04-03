# Unity预制体批量修改工具

这个示例展示了如何在Unity编辑器中批量修改预制体，包括添加和删除组件。

## 功能特点

- 批量修改预制体
- 支持添加组件到预制体
- 支持从预制体移除组件
- 自动保存修改后的预制体
- 保持预制体连接关系
- 自动刷新资源数据库

## 使用方法

1. 在Unity编辑器菜单中选择：
   - `Tools -> PrefabModify -> AddComponentAndSave` 添加组件
   - `Tools -> PrefabModify -> DelComponentAndSave` 删除组件
2. 工具会自动处理指定路径的预制体
3. 修改完成后会自动保存并刷新资源库

## 技术细节

- 使用 `AssetDatabase` 加载预制体资源
- 通过 `PrefabUtility` 实例化和保存预制体
- 使用 `GameObject` API操作组件
- 支持预制体的连接模式保存
- 自动清理临时对象

## 代码示例

```csharp
[MenuItem("Tools/PrefabModify/AddComponentAndSave", priority = 26)]
private static void AddComponentAndSave()
{
    var prefab = AssetDatabase.LoadAssetAtPath<GameObject>(PrefabPath);
    var gameobject = PrefabUtility.InstantiatePrefab(prefab) as GameObject;
    if (null == gameobject.GetComponent<ComponentA>())
    {
        gameobject.AddComponent<ComponentA>();
    }
    
    PrefabUtility.SaveAsPrefabAssetAndConnect(gameobject, PrefabPath,
        InteractionMode.AutomatedAction);
    GameObject.DestroyImmediate(gameobject);
    AssetDatabase.SaveAssets();
    AssetDatabase.Refresh();
}
```

## 工作流程

1. 加载目标预制体资源
2. 实例化预制体对象
3. 执行组件添加或删除操作
4. 保存修改到预制体资源
5. 清理临时对象
6. 刷新资源数据库

## 注意事项

- 确保预制体路径配置正确
- 注意处理组件依赖关系
- 及时清理临时对象避免内存泄漏
- 建议在批处理前备份预制体
- 大量预制体修改时注意性能影响

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 