# 参考来源与适用边界

本页供核对框架能力或继续阅读时使用，无需每次加载。公开资料核对日期：2026-10-01。API 应以使用项目锁定的版本为准，下面的文档与主分支可能继续变化。

Skill 中的构建路线、抽象选择和调试建议是综合归纳，不是这些项目共同规定的开发流程。

## 框架与组件

| 一手来源 | 支持的参考内容 | 使用边界 |
| --- | --- | --- |
| [Akita Simulator Engine](https://akitasim.dev/docs/akita/) | 引擎与模型分离；事件驱动、Smart Ticking；预建 cache、内存、互连及观测设施 | 框架可复用不代表组件符合任意目标微架构 |
| [MGPUSim Emulation Platform](https://akitasim.dev/docs/mgpusim/configuration/emulation_platform/) | 通过 builder 组装系统与 GPU，分离功能执行平台和系统连接 | 功能平台的例子不能作为周期参数或精确时序的依据 |
| [MGPUSim ComputeUnit](https://github.com/sarchlab/mgpusim/blob/main/amd/timing/cu/computeunit.go) | 计算单元内组织调度、子单元、寄存器及在途请求，通过端口连接其他组件 | 借鉴组件组织，不照搬特定 ISA、资源规模或流水阶段 |

## 推进与观测

[Akita Smart Ticking](https://akitasim.dev/docs/akita/getting_deeper/smart_ticking/) 解释进展判定、消息/端口事件唤醒，以及同时间戳事件排序。适合排查事件队列提前耗尽或组件无法继续运行的问题。不能把它简化成“本拍没有退休就休眠”；内部定时事件和调度器状态变化也可能需要推进。

[Akita Hooking and Tracing](https://akitasim.dev/docs/akita/getting_deeper/hooking/) 介绍任务起止、阶段标记和可挂接 tracer，可作为请求跨组件定位、统计及按需观测的参考。具体 API 和存储后端不属于本 Skill 的要求。

## 存储接口

[gem5 Memory System](https://www.gem5.org/documentation/general_docs/memory_system/) 说明端口、请求与 packet 的区别，以及 timing 访问中的数据、排队和资源竞争。这里借鉴的是交互与数据时序的区分，不建议将 gem5 的 C++ 对象体系搬到其他框架。

[Ramulator 官方仓库](https://github.com/CMU-SAFARI/ramulator2) 及 [README](https://github.com/CMU-SAFARI/ramulator2/blob/main/README.md) 提供可独立使用或作为库接入的 DRAM/控制器模拟。外部模型的存在不能替代适配层对接受、回调、时间单位、背压及排空语义的核对。

## 工程经验

另参考用户提供的《Detailed 到 Fast 的模拟器设计经验》及配套实现，提炼资源抽象、事务组织、对象生命周期、按需观测、配对测量和负实验经验。这里不附项目私有代码、配置、原始报告或性能数据，也不把个案推广为普遍收益。

可迁移的是“删除哪类软件工作、保留哪些因果关系、在什么条件下需要重新验证”，而不是具体队列深度、线程数、聚合延迟或速度倍数。

内部寄存级合并、父子事务、局部直接推进和后端独立替换均是候选方法，不是 Akita 强制架构。全局跳时也不是该经验中跨语言调用批处理的同义词。

## Skill 文件格式

目录与 `name` 对应，入口包含 `name`、`description` 和 Markdown 正文，来源放在可选的 `references/` 中。格式参考 [Agent Skills Specification](https://agentskills.io/specification)。具体发现和加载方式由 Agent 客户端或 Harness 决定，本仓库不安装依赖、不修改权限，也不绑定运行后端。
