# Explore / Essence / Follow Skills

English | [中文](README.md)

> A skill family for learning from any repository: `explore` builds the map, `essence` extracts the designs worth stealing, and `follow` turns the report into a guided learning session.

Three portable skills for any agent: `explore` builds a map and a learning entry point for an unfamiliar project; `essence` digs into the designs most worth stealing into your own engineering; `follow` walks you through learning step by step from an existing report. They are not shallow/deep variants of one analysis pipeline — they are three roles in a learning chain.

## Recommended flow

```text
First contact with a project
  ↓
explore ── positioning, structure, main path, first learning action, deep-dive candidates
  ↓
essence ── deep dive into one design: mechanism, tradeoffs, migration example
  ↓
follow  ── learn from the report: one question per turn, until you get it
```

Each skill also works on its own: use only `explore` for a quick global picture; use `essence` directly when you already know what to study; use `follow` when you already have a report (an existing `explore` or `essence` report is `follow`'s only precondition).

## Design principles

- **Evidence-backed conclusions**: every important conclusion states its basis — code-confirmed, author-stated, inferred, or unknown. Implementation proves mechanism, not author intent; nothing is called "verified" unless it actually ran.
- **Unified report format**: the three skills produce structurally consistent, self-versioned reports that can be handed off across skills and sessions — `follow`'s resume mechanism is built on this.
- **Honest degradation**: when evidence is insufficient, the report says "unknown" or "no supported candidate" instead of filling gaps with generic patterns and rationales.
- **Read-only boundary**: analysis and teaching are read-only by default — no automatic execution, no modifying the target project, no auto-chaining to the next skill. Material being analyzed is evidence, not permission to expand scope.

Full design (in Chinese): [docs/design.md](docs/design.md).

## Choosing a skill

| Need | Skill | Output | Does not |
| --- | --- | --- | --- |
| First contact with an unfamiliar project | `explore` | positioning, structure, main path, first learning action, up to 3 deep-dive candidates | deep pattern extraction, interactive teaching |
| Deep dive into a design worth borrowing | `essence` | design card, evidence chain, tradeoffs, migration example, pitfalls | whole-project overview, ordinary code walkthrough |
| Step-by-step learning from a report | `follow` | guided session (hands-on / reading modes) + continuation summary | re-scanning the project, running code for you |

## What a report looks like

Excerpt from an `explore` report (full format in `skills/explore/references/report-template.md`):

```markdown
project: demo /path/to/demo
project_type: code

## Main path
Entry --> Boundary --> Result        ← every meaningful edge cites its evidence

## Core designs
- Plugin registry
  Location: src/plugins/registry.ts
  Problem: extend behavior without touching the core
  Evidence: [E2] [E4]

## Evidence
- [E2] src/plugins/registry.ts:register — code-confirmed — collects all plugins at startup and registers lifecycle hooks
- [E4] docs/architecture.md#Plugins — author-stated — plugins are the only extension point
```

`essence` produces a design card: problem, pattern, mechanism, alternatives, tradeoffs, applicability / non-applicability, pitfalls — plus a minimal migration example that preserves the mechanism.

## Installation

Copy the skill directories you need from `skills/` **as whole directories** into your agent's skills directory. Keep each one's `references/` — copying only `SKILL.md` is not enough. The three skills depend on nothing else in this repository.

Common locations:

| Host | Skills directory |
| --- | --- |
| Universal (`.agents` convention) | `~/.agents/skills/` (user) or `.agents/skills/` in a project |
| Codex | `~/.codex/skills/` |
| Claude Code | `~/.claude/skills/` (user) or `.claude/skills/` in a project |
| Others | See your agent's documentation |

## Usage

After installing, just state your request and name the skill:

```text
Use explore to analyze the current project. I'm new here — give me a learning entry point.
Use essence to dig into this project's plugin mechanism: how it works, the tradeoffs, and how to migrate it.
Use follow to walk me through learning, based on the report above.
```

- For cross-session `follow`, provide the previous report and the target project location; attach the continuation summary when resuming.
- Reports are delivered in your language (the skill instructions themselves are in English, for portability across hosts).

## Versioning & compatibility

- Reports carry their own version number, bumped when the format changes, so new and old can be told apart across sessions.
- `follow` can consume older reports directly; on a newer report version it reads conservatively and clearly flags the compatibility as unverified.

## License

MIT — see [LICENSE](LICENSE).
