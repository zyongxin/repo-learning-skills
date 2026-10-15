# Follow Session Guide

Read after checking the report and before the first exercise. The report must supply `report_version`, `report_kind`, `project`, `revision`, `project_type`, and common sections `Scope`, `Entry points`, `Core designs`, `Evidence`, `Uncertainties`, `Next actions`. These are handoff fields, not prerequisites for rigid parsing: map older prose to their meaning where possible.

## Opening

State the project, prerequisite report, mode, learning goal and first observation point. Cite the source node. Teach enough context to make the question meaningful; leave the requested reasoning for the user. End after the question. With a legacy report that names only a file/symbol, read that node or request an excerpt before claiming its mechanism. Do not import implementation facts from another report or a previous evaluation scenario.

## Response handling

- Correct: explain why the evidence supports the answer, then offer one transfer or tradeoff question.
- Partly correct: acknowledge the valid part and point at the missing relationship; give a smaller question without answering it first.
- Stuck: provide one hint. If still stuck, simplify or show a minimal explanation.
- Skip: reveal only what is needed and mark understanding unverified.

## Continuation summary

At a requested pause or session review, preserve this compact state. Do not dump it after every normal teaching turn.

```text
Project: {name and root}
Report: {identity/path, format and project revision}
Mode: {Reader|Runnable}
Goal: {learning goal}
Current node: {path and symbol/heading}
What the learner said: {answer or not answered}
Correction or hint given: {details or none}
Exercise status: {not-started|in-progress|completed|skipped|too-hard}
Next node: {pending action}
```

## Evidence limits

A documented command is supported, but not necessarily executed. A user-reported output must be attributed to the user. A source test expresses expected behavior; it is not a passing run. If the report supplies no source excerpt and the repository is unavailable, teach the report's stated mechanism conditionally and disclose that its source evidence has not been checked.
