# Unity应用图标设置工具

这个示例展示了如何在Unity编辑器中设置应用图标，包括默认图标和不同平台的应用图标。

## 功能特点

- 设置默认图标
- 平台图标配置
- 批量图标设置
- 自动尺寸适配
- 编辑器集成
- 资源管理
- 一键设置

## 使用方法

1. 设置默认图标：
```csharp
public static void SetDefaultIcon()
{
    string iconPath = "Assets/Icons/default_icon.png";
    Texture2D texture = AssetDatabase.LoadAssetAtPath<Texture2D>(iconPath);
    UnityInternalAPIEngineBridger.SetDefaultIcon(texture);
}
```

2. 设置平台图标：
```csharp
public static void SetPlatformIcon()
{
    string iconPath = "Assets/Icons/app_icon.png";
    Texture2D texture = AssetDatabase.LoadAssetAtPath<Texture2D>(iconPath);
    
    // 获取目标平台的图标尺寸
    int[] sizes = PlayerSettings.GetIconSizesForTargetGroup(BuildTargetGroup.iOS);
    Texture2D[] icons = new Texture2D[sizes.Length];
    
    // 设置所有尺寸的图标
    for (int i = 0; i < icons.Length; i++)
    {
        icons[i] = texture;
    }
    
    // 应用图标设置
    PlayerSettings.SetIconsForTargetGroup(BuildTargetGroup.iOS, icons);
    AssetDatabase.SaveAssets();
}
```

## 技术细节

- 使用PlayerSettings API
- 图标资源加载
- 多尺寸处理
- 设置保存

## 实现原理

1. 图标系统
   - 资源加载
   - 尺寸配置
   - 平台适配
   - 设置应用

2. 资源管理
   - 图标导入
   - 格式处理
   - 质量控制
   - 内存管理

3. 平台支持
   - iOS配置
   - Android配置
   - 尺寸要求
   - 格式要求

## 应用场景

1. 应用开发
   - 品牌标识
   - 版本区分
   - 平台适配
   
2. 开发工具
   - 快速配置
   - 批量处理
   - 自动化工具
   
3. 项目管理
   - 版本控制
   - 资源管理
   - 配置管理

## 注意事项

- 图标尺寸要求
- 格式兼容性
- 平台特殊性
- 资源管理
- 性能影响

## 扩展建议

1. 功能扩展
   - 批量导入
   - 预览功能
   - 自动调整
   - 质量检查

2. 工具优化
   - 可视化界面
   - 拖放支持
   - 预设管理
   - 错误检查

## 代码示例

```csharp
public class AppIconManager
{
    private const string ICON_FOLDER = "Assets/Icons/";
    
    public static void SetupAppIcons(string iconName, BuildTargetGroup platform)
    {
        string iconPath = ICON_FOLDER + iconName;
        Texture2D mainIcon = AssetDatabase.LoadAssetAtPath<Texture2D>(iconPath);
        
        if (mainIcon == null)
        {
            Debug.LogError($"找不到图标文件: {iconPath}");
            return;
        }

        try
        {
            // 获取平台图标尺寸
            int[] sizes = PlayerSettings.GetIconSizesForTargetGroup(platform);
            Texture2D[] icons = new Texture2D[sizes.Length];
            
            // 生成不同尺寸的图标
            for (int i = 0; i < sizes.Length; i++)
            {
                // 这里可以添加图像处理逻辑，根据需要调整图标尺寸
                icons[i] = mainIcon;
            }
            
            // 应用图标设置
            PlayerSettings.SetIconsForTargetGroup(platform, icons);
            
            // 保存更改
            AssetDatabase.SaveAssets();
            Debug.Log($"成功设置 {platform} 平台的应用图标");
        }
        catch (System.Exception e)
        {
            Debug.LogError($"设置应用图标时出错: {e.Message}");
        }
    }

    [MenuItem("Tools/App Icons/Set iOS Icons")]
    private static void SetIOSIcons()
    {
        SetupAppIcons("ios_icon.png", BuildTargetGroup.iOS);
    }

    [MenuItem("Tools/App Icons/Set Android Icons")]
    private static void SetAndroidIcons()
    {
        SetupAppIcons("android_icon.png", BuildTargetGroup.Android);
    }
}
```

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 