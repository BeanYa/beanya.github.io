---
title: ClaudeCode+Glm4.7/OpenCode+OhMyOpenCode/Antigravity在同项目下的对比
mathjax: true
date: 2026-01-24 02:03:29
tags: 
    - AI
    - Coding
    - VibeCoding
---

# 背景

## Before

原先跟着[Autofac.Annotation](https://github.com/yuzd/Autofac.Annotation)手写了一个用于C#类似功能的项目（简化版），利用了Autofac的Module功能进行额外加载。受限于当时语言版本和对Roysln的不熟悉，利用了当时非PostSharp以外的Aop实现方案：Castle.DynamicProxy，有很多地方不理想，想要实现比较复杂的功能比较麻烦，需要借助各种事件和额外的容器，包括异步和各个AOP方法调用链中的各种异常和结果处理，性能也不如意。

## Whats new?

### VibeCoding 初体验

大模型大行其道的今天，VibeCoding一直是很热门的话题，手头上没有多少有点价值或者说复杂度的项目（当然这个也并不很复杂），想到之前购买过一系列的API或者CodingPlan等，但都是只买了一个月或者浅尝即止。

体验了一下`Gemini 3`横空出世时的前端抽卡，买了一个月的`MiniMax-2.1`和智谱AI的CodingPlan Lite(`GLM-4.7`)，都在`Claude Code`和`OpenCode`上体验了一下，但也只是简单的利用一些现成的，或者自己写的简单的prompt去做一些前端App。

> 例如: 简单的公司介绍页，用药提醒App等

发现其实各家IDE和模型在这种简单场景下体验都差不多，细节是`MiniMax-2.1`和`Glm-4.7`在做简单任务时完成的不错，但是在做同一个用药提醒APP的时候，这俩收尾时都容易出现项目运行`npm run`后界面空白，控制台报错等错误，把错误粘贴回去一般几次prompt后可以修复。

同样的场景，OpenAi的`codex`花了很长很长时间（具体忘了，几个小时是有的）才完成，但是代码并没有报错且界面审美我个人可以接受。

> 为什么不用Claude Code + Claude的呢？贵（同样的prompt，一句话吃了$8）当然效果不错，速度很快且无报错，界面审美我个人可以接受

### Now

有了上面的初步体验，确实感受到了Ai大模型的强大。

看到有老哥有两个屏幕铺满了Agent，一天甚至`Claude Max`的用量都不够，一个月能刷到几百甚至几千刀乐，想起自己确实没有这么大的项目和量来使用AI，但是可以复写一些以前的项目，便想起于此。

试着用`Claude Code`+`Glm-4.7`来实际编写这个项目，当然还引入了一些SDD（Specification-Driven Development），利用轻量的`OpenSpec`来辅助项目规划，本质是一次`Vibe Coding`的尝试与学习。

> 当然不限于这个组合，还用上了`Open Code + Oh-My-OpenCode`+`DeepSeek Reasoner/Glm-4.7`，最后碰上难题切换了`Antigravity`+`Claude Opus 4.5`（用上`Claude Opus`比较经济的方法，当然还有各种白嫖`Cursor`的）

# 收获

项目上传于`Github`-[Csanno](https://github.com/BeanYa/csanno)

## 刚开始

利用`OpenSpec`，完成了项目的初始化和初步的编写。

项目的核心功能是完成注解的扫描并注册组件，利用`Claude Code`+`Glm-4.7`完成的很好。

不足的是不知是否是模型差异，无论在`OpenCode`还是`Claude Code`里`GLM-4.7`并不能一步到位，在已经拆分需求，单需求并不复杂的情况下，需要介入几次让他继续完成任务（Token还没有触顶），编写时长也挺长的，并且真的像很多评论说的，有几次在项目里随地大小便。有几次在项目已经有`REAMD.md`的情况下生成了另一个`README_XXX.md`甚至有git做版本管理的情况下生成了`README.md.backup`

> 我全程并不介入文件的编写，仅发起prompt

## 遇到问题

以上都可以通过耐心等待他的编写回应来继续完成任务，虽然时间长了点但是任务是可以完成的。

但是在我往里面添加一个新功能，去实现AOP的时候，问题就出现了。

尝试了以下组合：

- `Claude Code`+`Glm-4.7`直接coding
- `Open Code + Oh-My-OpenCode`+`DeepSeek Reasoner`plan模式做规划，`Open Code + Oh-My-OpenCode`+`Glm-4.7`做执行
- `Open Code + Oh-My-OpenCode`+`Glm-4.7`开启plan模式后直接执行
- `Claude Code`+`Glm-4.7`从plan模式开始分析并执行
- `Claude Code`+`Glm-4.7`+`openspec`做规划并执行

都难以真正完成任务。

出现了：

- 可以看见在会话token未见顶的情况下，剩下三分之一左右的tasks需要进行手动的prompt让他继续执行。
- 测试代码在Agent的控制台里报的是通过，但是我用`Rider`去编译调试这段[Test]代码，显示的是用例不通过。
- 在根目录下生成了奇怪的`README.md.backup`（已经用git在管理版本）
- 在test目录下生成了一个初始项目，即包含了只有一句`Console.WirteLine("Hello World")`的`Program.cs`和一个`xxx.csproj`
- 把已经生成管理好的sln文件，修改其目录，额外把src下的项目单独包括起来，test和generator又被独立于src之外，类似于:
    - src
        - csanno
    - csanno.test
    - csanno.generator

等各种问题，且始终不能完成我最终的目的。

并且在尝试手写一大段样例prompt之后依然无法完成的很好，测试无法通过：

```markdown
背景：项目目前已经实现了注解式注册组件，且支持利用SourceGenerator进行编译期生成。
目标：

实现AOP功能，支持方法前后拦截。

实现方式：
使用SourceGenerator在编译期生成代理类，代理类在方法调用前后插入拦截逻辑。
不依赖额外的类似于Autofac.DynamicProxy/Castle.DynamicProxy的库

用户使用方式：
1. 定义一个拦截器接口，例如IInterceptor，包含方法OnBefore和OnAfter。
    拦截器由用户自定义实现，以下例子在test中实现，用于测试：

    ```csharp
    public interface IInterceptor
    {
        void OnBefore(MethodInfo method, object[] args);
        void OnAfter(MethodInfo method, object result);
    }

    public abstract class BaseInterceptor : IInterceptor
    {
        public virtual void OnBefore(MethodInfo method, object[] args) { }
        public virtual void OnAfter(MethodInfo method, object result) { }
    }

    public class LoggingAttribute : Attribute
    {
        public string AddtionalInfo { get;set; }

        public LoggingAttribute(string addtionalInfo)
        {
            AddtionalInfo = addtionalInfo;
        }
    }

    [BindWith<LoggingAttribute>]
    public class LoggingInterceptor : BaseInterceptor
    {
        public void OnBefore(MethodInfo method, object[] args)
        {
            Console.WriteLine($"Entering {method.Name} with arguments: {string.Join(", ", args)}");
        }

        public void OnAfter(MethodInfo method, object result)
        {
            Console.WriteLine($"Exiting {method.Name} with result: {result}");
        }
    }

    
    [BindWith<LoggingAttribute>]
    public class LoggingInterceptor2 : BaseInterceptor
    {
        public void OnBefore(MethodInfo method, object[] args)
        {
            Console.WriteLine($"Entering {method.Name} with arguments: {string.Join(", ", args)} [2]");
        }

        public void OnAfter(MethodInfo method, object result)
        {
            Console.WriteLine($"Exiting {method.Name} with result: {result} [2]");
        }
    }
    ```
    注：拦截器同时应该作为组件注入到Autofac容器中。

2. 在需要拦截的方法上使用自定义的拦截器特性，例如[Logging]。
    ```csharp
    public class SampleService
    {
        ...constructor
        ...props
        ...methods

        [Logging("Sample method execution")]
        public int Add(int a, int b)
        {
            return a + b;
        }
    }
    ```

3. 编译期生成代理类，代理类在方法调用前后插入拦截逻辑。
    因为用户代码定义了多个拦截器，所以生成的代理类需要支持多个拦截器的调用。
    生成的代理类示例：
    ```csharp
    public class SampleService_Proxy : SampleService
    {
         ...constructor
        ...props
        ...methods

        private readonly List<BaseInterceptor> _interceptors;

        // 构造函数注入拦截器列表
        public SampleService_Proxy(List<BaseInterceptor> interceptors)
        {
            _interceptors = interceptors;
        }

        public override int Add(int a, int b)
        {
            foreach (var interceptor in _interceptors)
            {
                interceptor.OnBefore(MethodBase.GetCurrentMethod(), new object[] { a, b });
            }
            var result = base.Add(a, b);
            foreach (var interceptor in _interceptors)
            {
                interceptor.OnAfter(MethodBase.GetCurrentMethod(), result);
            }
            return result;
        }
    }
    ```

约束：
- 作为类库应用，src目录下的代码仅作为类库实现，测试代码（例如Logging/Cache等自定义的拦截器和注解属性的实现应仅作为测试和样例）放在test目录下。
- 若有对README的更新，请更新在根目录下的README.md，补充或新增对应章节即可。
- 其他约束参考@/openspec/project.md中描述。
- 所有过程均不使用OpenSpec或OpenSpec-cn的规范操作。
``

## 解决问题

最后用回了以上最为令人称赞的`Claude-Opus-4.5`，打开了`Antigravity`选好模型后，将上述的prompt直接贴入。

他一步到位生成了我想要的内容，简洁且可运行。

> 当然还是需要他自己运行test发现错误并自己修复的。

## 总结

简单任务下，使用`Claude Code`+`Glm-4.7`或者`Open Code + Oh-My-OpenCode`+`Glm-4.7`是不错的，任务响应很快，在良好的约束下(例如使用`openspec`)是不错的。

> 后来嫌`openspec`麻烦，直接用plan模式了

但是遇到复杂的难题，用回`Claude-Opus-4.5`还是更能实际的解决问题，不然会在无尽的procee申请中耗费一天。

当然我相信如果足够耐心，最后问题是可以被解决的，解决方案也趋同，但是这之中耗费的实际估计会成倍数增长。