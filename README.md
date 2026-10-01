# Sim_skill

面向 Agent 的周期级与周期近似模拟器构建参考。包含基本构建路线，重点是基础设施复用、模型抽象，以及调试和性能优化经验；不绑定目标 ISA、硬件配置、编程语言或 Agent 编排方式。

## 内容

```text
simulator-construction/
├── SKILL.md
└── references/
    └── sources.md
```

[SKILL.md](simulator-construction/SKILL.md) 是唯一 Skill 入口，涵盖 ISA 功能建模、计算单元、流水线、调度、cache/memory 和系统执行的衔接，并给出 Akita 等框架的使用建议。

[参考来源](simulator-construction/references/sources.md) 仅在需要核对框架能力或追溯经验时读取，不是额外开发流程。

## 使用

将整个 `simulator-construction/` 目录放入所用 Agent 客户端支持的 Skill 搜索位置，或由 Harness 按任务读取 `SKILL.md`，并保留相对引用可访问。不同客户端的注册方式以其文档为准。

正文提供候选方法及适用边界。Agent 可根据目标、现有代码与证据调整路线、组件划分和抽象层次，不需要为遵循本 Skill 重做已有功能、迁移框架或维护多套模型。

初版是参考知识整理，尚未通过独立 Agent 构建实验评估效果。
