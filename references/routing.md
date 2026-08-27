# 稳定事实路由规则

## 判断是否应该沉淀

一条信息值得 tidyup 的标准：未来读者需要知道它，且它不只是当前会话进度。

## 默认路由

| 事实类型 | 默认目标 | 判断要点 |
|---|---|---|
| 项目级硬规则、踩坑教训、约定、禁忌 | 项目级 `CLAUDE.md` / `AGENTS.md` | 影响「模型怎么做」，模型每次会话读 |
| 架构、模块边界、数据流、技术选型 | 项目级 `CLAUDE.md` / `AGENTS.md` | 影响系统如何工作 |
| 项目目的、安装、运行、快速上手 | README.md | 第一次接触项目的人需要 |
| 对外 API、接口、集成示例 | README.md 或 docs/ | 外部接入需要 |
| 跨项目协作风格、习惯 | 提醒同步到全局 `~/.claude/CLAUDE.md` | 不替用户改全局配置 |

## 项目级指引的选择

项目级指引文件是 `CLAUDE.md` 或 `AGENTS.md`（二者常互为软链，本质同一份）。路由时：

- 项目有 `AGENTS.md` → 写 `AGENTS.md`（现代通用标准，workbuddy/claude/agents 三家通用）。
- 只有 `CLAUDE.md`（无 `AGENTS.md`）→ 写 `CLAUDE.md`。
- 两者都有 → 判断哪个是权威（软链指向的那个），写权威那份。

## 不主动创建原则

- 主目标只有两个载体：项目级 `CLAUDE.md` / `AGENTS.md`（模型读）+ README（人读）。
- ARCHITECTURE / ROADMAP / PRINCIPLES / CHANGELOG / openspec 等软件工程文档：**项目已有才更新，没有不主动创建**。
- 不主动创建 docs/，除非项目已有 docs/ 或用户明确要求。
- 不主动创建 `.agent/INTEGRATION.md` 等自造接入文件——项目级 `CLAUDE.md`/`AGENTS.md` 本身就是标准接入点。

## 冲突处理

如果事实既像「模型该知道的规则」又像「人该知道的说明」：

- 影响模型怎么做 → 项目级 `CLAUDE.md` / `AGENTS.md`
- 影响人怎么用 → README
- 两者都需要 → 两边都写，但不要复制同一段；互相引用即可。
