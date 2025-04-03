# Unity ReactiveX实现工具

这个示例展示了如何在Unity中实现ReactiveX（响应式编程）模式，提供了一套完整的响应式编程工具链。

## 功能特点

- 响应式编程支持
- 链式操作API
- 多线程支持
- 事件流处理
- 可组合操作符
- 自动资源释放
- 主线程调度

## 使用方法

1. 基础订阅：
```csharp
List<int> nums = new List<int> { 10, 20, 30 };
nums.ToObservable()
    .Where(_value => _value > 10)
    .Select(_value => _value * _value)
    .Subscribe(_result => { Debug.Log(_result); });
```

2. 延时操作：
```csharp
this.ToObservable()
    .Delay(1)
    .Execute(() => { Debug.Log(1); })
    .Delay(1)
    .Execute(() => { Debug.Log(2); })
    .Subscribe();
```

3. 输入检测：
```csharp
this.ToObservable()
    .EveryUpdate()
    .Where(_ => Input.GetButtonDown("Fire1"))
    .Subscribe(_ => { Debug.Log("点击"); });
```

## 技术细节

- 实现 `IObserver` 和 `IObservable` 接口
- 支持自定义操作符
- 提供线程调度功能
- 实现事件流控制
- 支持资源自动释放

## 主要组件

1. 核心类
   - Subscribe：订阅者实现
   - Observable：可观察对象
   - Operator：操作符基类
   - MainThreadDispatcher：主线程调度器

2. 操作符
   - Where：条件过滤
   - Select：数据转换
   - First：获取首个元素
   - Foreach：遍历处理
   - Execute：执行操作
   - Delay：延时处理

3. 工具类
   - IOnDestroy：销毁接口
   - ThreadDispatcher：线程调度
   - DisposableBag：资源释放管理

## 实现原理

1. 订阅机制
   - 观察者模式
   - 事件流处理
   - 异常处理
   - 完成通知

2. 操作符链
   - 链式调用
   - 数据转换
   - 条件过滤
   - 组合操作

3. 线程控制
   - 主线程分发
   - 异步操作
   - 线程同步
   - 任务调度

## 应用场景

1. 事件处理
   - UI交互
   - 输入检测
   - 网络请求
   - 异步操作

2. 数据流处理
   - 数据转换
   - 数据过滤
   - 数据组合
   - 数据缓存

3. 游戏系统
   - 状态管理
   - 计时器系统
   - 动画控制
   - 资源加载

## 注意事项

- 正确处理订阅释放
- 避免内存泄漏
- 合理使用线程
- 注意性能开销
- 处理异常情况

## 扩展建议

1. 功能扩展
   - 更多操作符
   - 更多工具方法
   - 调试工具
   - 性能优化

2. 使用优化
   - 链式API改进
   - 错误处理增强
   - 内存管理优化
   - 线程控制增强

## 开发环境要求

- Unity 2018.4或更高版本
- .NET Framework 4.x 