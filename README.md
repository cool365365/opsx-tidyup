# opsx-tidyup — 项目知识同步（通用版）

用户说「这阶段做完了」「沉淀一下」「同步下项目文档」时触发：把现场层 / 对话历史里的**稳定事实**同步到项目长期载体——主沉淀到**项目级指引**（`CLAUDE.md` / `AGENTS.md`，模型每次会话读），次沉淀到 **README / docs**（人上手读），并清理 WORKLOG 中已同步的条目。

它不是 handover，也不是普通总结：tidyup 写的是**长期项目知识**，不只是会话快照。

## 关于本技能家族

本 skill 属于「会话收束与知识沉淀」能力族（OPSX），共三件，面向 Claude Code / Codex 等通用 coding agent，围绕项目内 `.agent/` 目录协作：

| 成员 | 时机 | 分工 |
|---|---|---|
| [opsx-worklog](https://github.com/cool365365/opsx-worklog) | 任务进行中 | 维护 `.agent/WORKLOG.md` 滚动任务现场 |
| opsx-tidyup（本包） | 阶段性收尾 | 把稳定事实沉淀到项目长期文档（`CLAUDE.md`/`AGENTS.md`、README/docs） |
| [opsx-handover](https://github.com/cool365365/opsx-handover) | 会话结束前 | 判断是否先沉淀，再生成 `.agent/SESSION_HANDOVER.md` 会话快照 |

**本包负责「沉淀」这一层。** 典型完整工作流：进行中由 worklog 记现场 → 收束时 handover 判断是否需要 tidyup → 本包把稳定事实按类型路由写进对应文档 → 清理已同步的 WORKLOG 条目。单独使用任一件也成立。

> **WorkBuddy 用户**：请改用 WorkBuddy 版两件套 [session-handover](https://github.com/cool365365/session-handover) + [memory-distill](https://github.com/cool365365/memory-distill)，它们的沉淀目标是 WorkBuddy 的 MEMORY.md 记忆体系而非项目文档。

## 三层载体

| 层级 | 文件 | 目的 | 动作 |
|---|---|---|---|
| 项目级指引 | 项目根 `CLAUDE.md` / `AGENTS.md` | 影响「模型怎么做」的事实 | 自动写（主目标） |
| 项目级文档 | README / docs/ | 影响「人怎么用」的事实 | 自动写（次目标） |
| 全局指引 | 平台全局规则文件 | 跨项目协作偏好 | 只提醒，不自动写 |

## 写入原则

- **合并优于追加**：更新旧条目，不平行制造重复版本；
- **删除优于保留**：过期计划、推翻方向、临时上下文应删或压缩；
- **写对地方**：「模型该知道的规则」进 CLAUDE.md/AGENTS.md，「人怎么用」进 README/docs——混着写等于没沉淀；
- 不主动发明新文档：项目已有才更新，没有不硬造。

## 使用

把本目录放入你的 agent skills 目录（如 `~/.claude/skills/opsx-tidyup`），对话中说「沉淀一下」「同步下项目文档」「更新 AGENTS.md」等即可触发。

可与同族另两件配合使用；单独安装也完全可用。

## 目录结构

```text
opsx-tidyup/
├── SKILL.md
└── references/
    ├── routing.md          # 事实类型 → 目标文档的路由规则
    ├── worklog-cleanup.md  # WORKLOG 反向清理规则
    └── checklist.md        # 自检清单
```

## License

MIT
