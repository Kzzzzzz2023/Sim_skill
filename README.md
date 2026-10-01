# 模拟器构建 Skill

面向离线、沙盒环境的模拟器构建参考。只包含方法说明，不包含外部链接、外部实现名称、目标架构参数或实验结果。

## 内容

```text
simulator-construction/
├── SKILL.md
└── references/
    ├── construction-and-framework.md
    ├── modeling-abstraction.md
    └── debugging-and-performance.md
```

入口为 [SKILL.md](simulator-construction/SKILL.md)。三份参考正文分别覆盖构建与基础设施复用、模型抽象、调试与性能优化；不是需要另行查询的来源索引。

## 离线接入

由实验准备方将整个 `simulator-construction/` 目录放入沙盒可读的位置，保持目录关系，并在任务参考输入中明确入口文件。仅有宿主路径或单独注入入口文本，不代表相邻参考文件在沙盒内可读。

运行前检查入口及三份参考文件均可读取；具备只读参考挂载能力时可按该方式提供。不要依赖自动联网下载、客户端隐式发现或其他工程目录。Skill 不自行安装依赖，也不修改实验环境、权限或验收要求。

Agent 根据任务选择阅读范围、组件组织和实现方案，无需执行固定阶段或维护多套模型。具体配置、可复用设施与接口以该次实验提供的本地材料为准。

本包尚未通过独立的 Agent 构建实验评估效果；文件检查不等于模型构建或沙盒接入验证。
