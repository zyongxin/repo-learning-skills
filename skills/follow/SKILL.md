---
name: follow
description: Guide an interactive learning session from an existing explore or essence report. Uses Runnable or Reader mode and waits for the user's response at each learning step.
metadata:
  version: "0.1.0"
  report_contract: "1"
---

# Follow: Guided Learning Session

Use this skill only when an `explore` or `essence` report is available. It teaches from the report; it is not a new project analyzer.

## Preconditions

1. Load the report supplied by the user, or the report already present in the current session.
2. Check `report_version`, project identity, project type, entry points, evidence, and next action.
3. If no report exists, say:

> I need an existing `explore` or `essence` report before starting a follow-along session. Please provide one or run `explore` or `essence` first.

4. If the report lacks the project identity or learning target, ask for that missing information. If only optional fields are absent, enter limited Reader mode and list the limitation.

For an older report without a version, map its existing content to the fields you need; do not force a rerun. If multiple reports refer to different targets and the intended one is ambiguous, ask which to use. For an unsupported newer report version, read available content conservatively in Reader mode and disclose that compatibility is unverified. Report claims remain claims until their cited evidence is available; do not invent unavailable source content. If the report supplies only a project name, target and file/symbol but no mechanism, first inspect that cited node within the allowed scope or ask for its excerpt. Do not invent a multiple-choice mechanism from the symbol name. If source access is unavailable or forbidden, disclose the limit and ask for the missing excerpt rather than teaching an unestablished implementation. Keep evidence from different projects or evaluation scenarios separate.

Load `references/session-guide.md` after the report check. Resolve this path relative to this SKILL.md's directory, not the working directory or target project root. Use a supplied continuation summary to resume the named node. Reuse the user's stated goal and experience; ask about them only if the answer changes the first learning action. Respond in the user's language, including missing-report guidance.

Do not rescan the whole project to repair a missing report.

## Mode selection

- `explore` + code or template with a supported runnable path and available environment + user wants to run/change it: **Runnable**;
- `explore` + docs, skill, unknown, a template without a supported runtime, or a preference for reading: **Reader**;
- `essence`: **Reader** by default; use Runnable only when the user explicitly asks and the report supports a runnable path.

All other cases default to Reader. A supported project command is sufficient to start a learner-run step; a prior successful run is not a prerequisite.

State the selected mode and why before the first exercise. There are only these two modes.

## Session state

Track this state in the conversation and include a compact continuation summary when the session pauses:

```text
source_report: path or pasted report identity
mode: runnable | reader
learning_goal: one sentence
current_node: ...
answered: ...
misconceptions: ...
exercise: not-started | in-progress | completed | skipped | too-hard
next_node: ...
```

Do not mark an exercise completed before the user answers or explicitly reports the result.

## One-turn teaching protocol

Each teaching turn contains:

1. one learning goal and why it matters to the architecture;
2. one observation point or user action;
3. one prediction, explanation, or choice question;
4. an explicit pause for the user's response.

After asking the question, stop. Do not reveal the answer in the same turn unless the user asks for the answer or asks to skip. Keep the observation focused on the report's cited file, symbol, command, or diagram.

Leave a meaningful inference for the learner. A hint may direct attention to a line or explain unfamiliar syntax, but must not first state the complete conclusion and then ask the learner to repeat it. On resume, preserve the previous attempt and hints; use a smaller unanswered question or a new transfer problem if the original conclusion has already been revealed.

When the user responds:

- **correct**: confirm the mechanism, then ask one transfer or tradeoff question;
- **partly correct**: name the missing relationship and give a smaller observation;
- **stuck**: give one hint, then a second hint or a short explanation if needed;
- **skip**: reveal the minimum needed, mark the exercise skipped, and continue.

Questions should test reasoning about the design, not only “what happens next?”.

## Runnable rules

Let the user run commands and make one safe change. Commands must come from the report, project documentation, or clearly marked generic setup guidance. Do not claim that a command worked until the user reports output or an actual run confirms it. Do not install dependencies, run the project, or edit code on the user's behalf inside this skill.

A project-documented command may be offered to the learner without having been executed. Distinguish supported command from observed successful execution. If no supported command is available, the environment is unavailable, or the user prefers reading, switch to Reader and explain the reason. Do not infer the runtime, version or package manager solely from a config filename; use the report and direct project documentation.

## Reader rules

Teach the design as problem → approach → implementation → tradeoff. Explain what each cited file embodies, why it matters to the architecture, and what the user should inspect. You may perform a targeted read of the current node's direct dependency when needed; do not rescan the repository. If the report revision is stale, check only the current node and its direct dependencies. If the mechanism changed materially, disclose the mismatch and ask for an updated report; do not teach outdated facts as current.

## Boundaries and completion

- Do not invent missing evidence or author intent.
- Do not automatically invoke `explore` or `essence`.
- Do not add a third mode.
- Do not modify files, install dependencies, or execute project/setup commands for the user. Targeted read-only inspection is allowed; explanatory code snippets are allowed. A separate request to delegate execution changes the task scope and must be handled explicitly outside the teaching step.
- Deliver in chat by default. Save reports or continuation files only when requested or already authorized.
- End with a review of the learned idea, exercise result, misconceptions, and next direction.

Outcome:

```text
Follow Session: {project}
Mode: runnable | reader
Prerequisite report: explore | essence
Exercise result: completed | partial | skipped | too-hard
Next direction: ...
Status: complete | paused
```

After the review, ask whether the user wants another exercise or to end the session.
