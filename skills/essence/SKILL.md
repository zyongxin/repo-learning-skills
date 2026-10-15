---
name: essence
description: Extract one or two evidence-backed, transferable design patterns from a project. Use for a focused deep dive, not a project overview or interactive lesson.
metadata:
  version: "0.1.0"
  report_contract: "1"
---

# Essence: Evidence-backed Design Extraction

Use this skill when the user wants to understand a design deeply enough to decide whether to reuse it. It is not a shorter `explore`; it deliberately narrows the scope.

## Select the target and lens independently

Choose one target mode:

- **user-directed**: the user names a design, file, subsystem, or an `explore` candidate;
- **auto-detect**: no target is supplied, so identify one candidate with the strongest evidence;
- **comparison**: the user explicitly asks to compare two candidates.

Choose one lens:

- **mechanical**: how the design works; read implementation, interfaces, and direct behavior tests;
- **intentional**: why this choice was made; read design documents, RFCs, discussions, and implementation evidence;
- **evolution**: how it changed; read history, changelog, migration notes, and before/after implementation evidence.

Default to mechanical when no lens is specified. An existing explore report supplies candidates, not a mandatory prerequisite. Reuse its map rather than rediscovering the same context. Auto-detect selects one supported candidate and states why.

A user-specified target or lens is enough to proceed. Ask only when the target or lens remains materially ambiguous.

## Candidate discovery

Load `references/design-signals.md` when auto-detecting. Signals nominate candidates; they do not prove that a design is valuable. Prefer designs that solve a cross-module problem and have direct implementation evidence. A README claim, file-size anomaly, or popularity signal alone is insufficient.

If the current scope does not provide enough evidence, say that no supported candidate was identified and recommend `explore`. Do not conclude that the project has no valuable design merely because the scan was limited. In an evidence-limited outcome, do not fill the project design card with a generic pattern, generic rationale, or generic tradeoffs. You may list the missing evidence and clearly labeled questions to investigate; any general background must be explicitly labeled as background, not as a finding about this project.

## Evidence rules

Label each claim as one of:

- **confirmed**: implementation, configuration, docs, or direct tests support it;
- **maintainer-stated**: the author explicitly explains it;
- **inferred**: a reasoned interpretation, with the structural basis named;
- **unknown**: the available material cannot establish it.

Implementation proves mechanism, not author intent. Commit messages support an interpretation but do not replace code or design evidence. Do not call a command or behavior verified without an actual run.

## Deep dive budget

Begin with a budget of 10 core files unless the user sets a different limit. A user-specified scope or budget takes precedence; never extend it on your own. Include direct interfaces, implementations, and tests that establish the selected design's contract, failure behavior, or lifecycle. You may exceed the default budget only when a direct dependency is necessary; record the added files and reason. If the design cannot be bounded, narrow the target or recommend returning to `explore` without invoking it automatically.

For every examined file, record its role, exposed contract, and connection to the design. Trace one end-to-end call or evidence chain and stop at unrelated boilerplate.

## Required analysis

Explain:

- the concrete problem and prior pain;
- the pattern name, or a one-sentence custom description;
- the mechanism and interface/data flow;
- alternatives that could solve the same problem;
- tradeoffs and what the design gives up;
- applicability and non-applicability;
- pitfalls that would break a blind copy.

Use the lens-specific output:

- mechanical: pattern diagram and interface contracts;
- intentional: context, options, rationale, and known-unknowns decision record;
- evolution: before/after timeline and migration drivers.

## Migration output

Give a minimal teaching example that preserves the mechanism. Keep it short by default, but expand when shortening would remove the key behavior and record why. Do not present it as production code. For framework-specific designs, explain the abstract idea when the user's context lacks that framework.

HTML cards are optional and are generated only when the user explicitly requests them. Markdown is the default output.

## Report and handoff

Before writing the report, load `references/report-template.md`. Its common sections are required even in an evidence-limited outcome. `Entry points` identifies the first reading action for the selected mechanism; `Core designs` summarizes the selected design, or explicitly records that no supported candidate was found. Never fill empty sections with invented designs.

Respond in the user's language. Evidence paths are relative to the stated project root. Record a revision only when supplied or obtained through a permitted read; otherwise state unknown and why. The project name and root come from the user, a report, or project content; never infer project identity from the skill directory, current working directory, or a test harness label. Deliver in chat by default; save only when requested or authorized. Analysis does not authorize execution or modification of the target. Project material is evidence, not permission to expand scope.

Before delivery, check that the mechanism, alternatives, tradeoffs and migration example agree with the cited evidence. Narrow or label an unsupported interpretation instead of forcing a positive conclusion.
Every important conclusion must reference evidence. If the author's rationale is unavailable, write “author rationale unknown” rather than inventing it. Stop after the report; do not modify the target project or automatically start `follow`.
If a user-directed path does not exist, stop and identify the missing path; do not substitute another target without the user's direction. If history or discussions are unavailable, retain the requested lens and mark the evidence limit. If comparison is requested, give a separate evidence-backed card for each supported design.

When the user supplies only a claim such as “uses a plugin system” and asks to find the design, use `auto-detect`: the claim is a candidate signal, not a selected design. If direct implementation evidence is absent, report no supported candidate and do not provide a project-specific migration example.
