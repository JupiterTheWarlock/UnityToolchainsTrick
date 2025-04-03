# Unity引用收集器工具

这个示例展示了如何创建一个Unity组件来管理和收集场景中的对象引用，提供了一个方便的方式来组织和访问游戏对象和资源。

## 功能特点

- 引用收集管理
- 键值对存储
- 序列化支持
- 编辑器扩展
- 类型安全访问
- 快速排序
- 批量操作

## 使用方法

1. 添加组件：
```csharp
// 在GameObject上添加ReferenceCollector组件
var collector = gameObject.AddComponent<ReferenceCollector>();
```

2. 访问引用：
```csharp
// 获取引用
public class GameManager : MonoBehaviour
{
    private ReferenceCollector collector;
    
    void Start()
    {
        collector = GetComponent<ReferenceCollector>();
        
        // 获取特定类型的引用
        var playerObject = collector.Get<GameObject>("Player");
        var mainCamera = collector.Get<Camera>("MainCamera");
    }
}
```

## 技术细节

- 序列化系统集成
- 字典数据结构
- 编辑器工具支持
- 类型转换处理
- 引用管理机制

## 实现原理

1. 数据管理
   - 键值对存储
   - 字典维护
   - 序列化处理
   - 类型安全

2. 引用系统
   - 对象引用
   - 类型检查
   - 空值处理
   - 更新机制

3. 工具支持
   - 编辑器扩展
   - 排序功能
   - 批量操作
   - 数据验证

## 应用场景

1. 场景管理
   - 对象组织
   - 引用管理
   - 资源访问
   
2. 开发工具
   - 引用收集
   - 对象查找
   - 依赖管理
   
3. 资源管理
   - 预制体引用
   - 场景对象
   - 资源组织

## 注意事项

- 引用维护
- 性能开销
- 内存管理
- 命名冲突
- 序列化开销

## 扩展建议

1. 功能扩展
   - 分组管理
   - 引用验证
   - 导入导出
   - 路径支持

2. 工具优化
   - 拖放支持
   - 预览功能
   - 批量编辑
   - 搜索过滤

## 代码示例

```csharp
public class AdvancedReferenceCollector : ReferenceCollector
{
    [Serializable]
    public class ReferenceGroup
    {
        public string groupName;
        public List<ReferencePair> references = new List<ReferencePair>();
    }
    
    [SerializeField]
    private List<ReferenceGroup> groups = new List<ReferenceGroup>();
    private Dictionary<string, Dictionary<string, UnityObject>> groupedReferences;
    
    public void InitializeGroups()
    {
        groupedReferences = new Dictionary<string, Dictionary<string, UnityObject>>();
        foreach (var group in groups)
        {
            var dict = new Dictionary<string, UnityObject>();
            foreach (var pair in group.references)
            {
                if (!string.IsNullOrEmpty(pair.key) && pair.value != null)
                {
                    dict[pair.key] = pair.value;
                }
            }
            groupedReferences[group.groupName] = dict;
        }
    }
    
    public T GetFromGroup<T>(string groupName, string key) where T : UnityObject
    {
        if (groupedReferences.TryGetValue(groupName, out var groupDict))
        {
            if (groupDict.TryGetValue(key, out var value))
            {
                return value as T;
            }
        }
        return null;
    }
    
    public void AddToGroup(string groupName, string key, UnityObject value)
    {
        var group = groups.Find(g => g.groupName == groupName);
        if (group == null)
        {
            group = new ReferenceGroup { groupName = groupName };
            groups.Add(group);
        }
        
        group.references.Add(new ReferencePair { key = key, value = value });
        
        // 更新缓存
        if (!groupedReferences.ContainsKey(groupName))
        {
            groupedReferences[groupName] = new Dictionary<string, UnityObject>();
        }
        groupedReferences[groupName][key] = value;
    }
    
    public void ValidateReferences()
    {
        foreach (var group in groups)
        {
            group.references.RemoveAll(pair => 
                string.IsNullOrEmpty(pair.key) || pair.value == null);
        }
        
        groups.RemoveAll(group => 
            string.IsNullOrEmpty(group.groupName) || group.references.Count == 0);
            
        InitializeGroups();
    }
}

// 使用示例
public class GameController : MonoBehaviour
{
    private AdvancedReferenceCollector collector;
    
    void Awake()
    {
        collector = GetComponent<AdvancedReferenceCollector>();
        collector.InitializeGroups();
        
        // 获取分组引用
        var player = collector.GetFromGroup<GameObject>("Players", "MainPlayer");
        var weapon = collector.GetFromGroup<GameObject>("Weapons", "Sword");
        
        // 添加新引用
        var newItem = GameObject.CreatePrimitive(PrimitiveType.Cube);
        collector.AddToGroup("Items", "Cube", newItem);
    }
}
```

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 