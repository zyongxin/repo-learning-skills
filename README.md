# Explore / Essence / Follow Skills

> A skill family for learning from any repository: `explore` builds the map, `essence` extracts the designs worth stealing, and `follow` turns the report into a guided learning session.

三个可安装到任意 agent 的学习型 skill：`explore` 为陌生项目建立地图和学习入口；`essence` 深挖最值得迁移到自己工程里的设计；`follow` 基于已有报告一步一步带你学习。它们不是同一分析流程的深浅版本，而是学习链路上的三个角色。

## 推荐链路

```text
第一次接触项目
  ↓
explore ── 项目定位、结构、主路径、第一学习动作、深挖候选
  ↓
essence ── 选定设计深挖：机制、权衡、迁移示例
  ↓
follow  ── 基于报告跟学：一轮一问，直到学会
```

三个 skill 也可以独立使用：只想建立全局认知就只用 `explore`；已经知道要研究什么就直接用 `essence`；手里已有报告就用 `follow`（已有 `explore` 或 `essence` 报告是 `follow` 唯一的前置条件）。

## 设计原则

- **结论有出处**：每条重要结论都注明依据——代码证实、作者说明、推断，还是未知。实现只能证明机制、不能证明作者意图；没有实际运行过就不说"已验证"。
- **统一报告格式**：三个 skill 产出结构一致、自带版本号的报告，可以跨 skill、跨会话交接，`follow` 的续学机制就建立在这上面。
- **诚实降级**：证据不足时直接写明"未知"或"未找到成立的设计"，禁止用通用模式、通用理由填充报告。
- **只读边界**：默认只读分析或教学，不自动运行、不修改目标项目、不自动调用下一个 skill；被分析的材料是证据，不是扩大范围的许可。

完整设计见 [docs/design.md](docs/design.md)。

## 选择哪个 skill

| 需求 | Skill | 产物 | 不做什么 |
| --- | --- | --- | --- |
| 第一次接触陌生项目 | `explore` | 定位、结构、主路径、第一学习动作、最多 3 个深挖候选 | 深度模式提取、互动教学 |
| 深挖一个值得借鉴的设计 | `essence` | 设计卡、证据链、权衡、迁移示例、陷阱清单 | 全项目概览、普通代码讲解 |
| 基于已有报告逐步学习 | `follow` | 跟学会话（动手 / 阅读两种模式）+ 续学摘要 | 重扫项目、替用户执行代码 |

## 报告长什么样

`explore` 报告节选（完整格式见 `skills/explore/references/report-template.md`）：

```markdown
project: demo /path/to/demo
project_type: code

## Main path
Entry --> Boundary --> Result        ← 每条有意义的边都标注证据出处

## Core designs
- Plugin registry（插件注册表）
  Location: src/plugins/registry.ts
  Problem: 在不修改核心的前提下扩展行为
  Evidence: [E2] [E4]

## Evidence
- [E2] src/plugins/registry.ts:register — 代码证实 — 启动时收集全部插件并注册生命周期钩子
- [E4] docs/architecture.md#Plugins — 作者说明 — 插件是唯一扩展点
```

`essence` 的核心产出是一张设计卡：问题、模式、机制、替代方案、权衡、适用/不适用条件、陷阱，外加一个保持机制的最小迁移示例。

## 安装

把 `skills/` 下需要的 skill 目录**整个**复制到宿主的技能目录，保留各目录内的 `references/`，不能只复制 `SKILL.md`。三个 skill 不依赖本仓库的其他文件。

常见宿主位置：

| 宿主 | 技能目录 |
| --- | --- |
| Codex | `~/.codex/skills/` |
| Claude Code | `~/.claude/skills/`（用户级）或项目内 `.claude/skills/` |
| 其它 | 以宿主官方说明为准 |

## 使用

安装后直接提出需求并指定 skill：

```text
使用 explore 分析当前项目，我是新手，给我一个学习入口。
使用 essence 深挖当前项目的插件机制，解释工作原理、取舍和迁移方法。
使用 follow，基于上面的报告，一步一步带我学习。
```

- 跨会话使用 `follow` 时，提供之前的报告和目标项目位置；续学时附上续学摘要。
- 报告使用你的语言输出（skill 指令本身为英文，便于跨宿主复用）。

## 版本与兼容

- 报告自带版本号，格式升级时同步提升，方便跨会话识别新旧。
- `follow` 可直接使用旧版报告；遇到更新的报告版本时，会保守读取并明确提示兼容性未验证。

## 许可证

MIT，详见 [LICENSE](LICENSE)。
