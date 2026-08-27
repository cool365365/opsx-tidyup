---
name: opsx-tidyup
description: 当用户要求整理或梳理项目知识、阶段性收尾、思考沉淀、同步项目文档、更新 CLAUDE.md/AGENTS.md、让下次会话能接上，或说"这阶段做完了""沉淀一下"时，使用本 Skill。它把当前会话和 `.agent/WORKLOG.md` 中已经稳定的项目事实同步到项目级 CLAUDE.md/AGENTS.md（模型读的指引）和 README/docs（人读的说明），并清理已沉淀的 WORKLOG 内容。区别于 handover：tidyup 写长期项目知识，不只是会话快照。不用于普通总结、单次问答。
---

# opsx-tidyup — 项目知识同步

## 定位

把现场层 / 对话历史里的**稳定事实**同步到项目长期载体。主沉淀到**项目级指引**（`CLAUDE.md` / `AGENTS.md`，模型每次会话读），次沉淀到 **README / docs**（人上手读）。它不是 handover，也不是普通总结。

## 三层载体

| 层级 | 文件 | 目的 | 本 skill 动作 |
|---|---|---|---|
| 项目级指引 | 项目根 `CLAUDE.md` / `AGENTS.md` | 影响「模型怎么做」的事实 | **自动写**（主目标） |
| 项目级文档 | README / docs/ | 影响「人怎么用」的事实 | 自动写（次目标） |
| 全局指引 | `~/.claude/CLAUDE.md` | 跨项目协作偏好 | **只提醒，不自动写** |

## 快速流程

1. 读取 `.agent/tidyup.md`，若存在则作为项目级补充规则，优先于默认路由。
2. 盘点项目级 `CLAUDE.md` / `AGENTS.md`、README、docs/ 和 `.agent/` 文件。
3. 从 `.agent/WORKLOG.md` 和本次会话提取长期事实。
4. 按事实类型路由（见 `references/routing.md`）。
5. 清理 WORKLOG 中已同步条目。
6. 输出变更摘要和未处理项。

详细规则：

- 路由规则：`references/routing.md`
- WORKLOG 清理：`references/worklog-cleanup.md`
- 自检清单：`references/checklist.md`

## 边界

本 skill 管：

- 项目级 `CLAUDE.md` / `AGENTS.md`（主目标：影响「模型怎么做」的事实）
- README / docs/ 下已有项目文档（次目标：影响「人怎么用」的事实）
- `.agent/WORKLOG.md` 的反向清理

本 skill 不管：

- 全局 `~/.claude/CLAUDE.md`——跨项目偏好，只提醒用户手动同步。
- `.clinerules` / `.cursorrules` 等平台特定规则文件。
- 不主动创建 ARCHITECTURE / ROADMAP / PRINCIPLES / CHANGELOG / openspec 等文档——项目已有才更新，没有不硬造。
- secrets、tokens、私钥或本地敏感配置。

## 写入原则

- 合并优于追加：更新旧条目，不平行制造重复版本。
- 删除优于保留：过期计划、推翻方向、临时上下文应删或压缩。
- 精确优于冗长：一段只说清一件事。
- 绝对时间：使用 `YYYY-MM-DD`，不写"今天""最近"。
- 尊重项目现有结构：没有 docs/ 时不主动创建 docs/；没有项目指引文件时按需创建。

## 判断纪律（判例）

- 判例「append 而非 merge」：某条事实与项目指引已有条目说的是同一件事，模型却平行写了第二个版本 → 错误。应更新旧条目，不新建平行条目。
- 判例「写给人看的文档」：模型把「模型该知道的规则」写进 README 而非 CLAUDE.md/AGENTS.md → 错误。模型下次会话读指引、不读 README，规则写进 README 等于没沉淀。

## 完成回复格式

```markdown
## 同步完成

### 已编辑
- `<文件>` — `<改动>`

### 已检查无需改动
- `<文件>`

### WORKLOG 清理
- `<清理内容>`

### 建议手动同步到全局 CLAUDE.md
- `<如有跨项目协作风格事实>`

### 未处理
- `<需要用户决定的事项>`
```
