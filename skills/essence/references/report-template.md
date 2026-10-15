# Essence Report Template

Load before final delivery. Keep the common metadata and six handoff sections even when no candidate is supported; use “not applicable (reason)” rather than filling gaps with invented content.

````markdown
report_version: 1
report_kind: essence
project: {name and project root}
revision: {commit/version/unknown with reason}
project_type: {code|docs|skill|template|unknown}

## Scope
- Target boundary: {mechanism or subsystem}
- Examined: {key materials}
- Omitted: {excluded areas}
- Initial budget: 10 core files; additions and reasons: {actual additions or none}

## Entry points
{One first reading action: relative path, symbol/heading, expected observation, evidence ID. For Runnable handoff, also include project-supported command, prerequisites, source and execution status.}

## Core designs
{Selected mechanism and evidence IDs, or “no supported candidate identified in this scope”.}

## Selection
- Target mode: {user-directed|auto-detect|comparison}
- Candidate basis: {signals and checked direct evidence}

## Lens
{mechanical|intentional|evolution}

## Design card
- Problem: {specific pain}
- Pattern: {recognized name or one-sentence custom description}
- Mechanism: {structure, contracts and evidence chain}
- Alternatives: {options with conditions; label hypothetical alternatives}
- Tradeoffs: {benefits and costs, separating interpretation from documented rationale}
- Applicability: {conditions that support reuse}
- Non-applicability: {conditions that favor another approach}

For an evidence-limited outcome, write `No supported candidate identified in this scope` and leave mechanism, alternatives, tradeoffs, applicability and migration example as unknown/not applicable. Generic background must be labeled as background and must not be phrased as a project finding.

{Mechanical: diagram + contracts. Intentional: context/options/rationale or unknowns. Evolution: dated changes and drivers, with missing history disclosed.}

## Evidence
- [E1] {path:Symbol/Heading, optional line} — {confirmed|maintainer-stated|inferred|unknown} — {claim}

## Uncertainties
{Unknown author rationale, untested behavior, missing history or limitations.}

## Migration example
{Minimal teaching code, pseudocode, decision checklist or migration steps appropriate to the lens. Mark execution status and any deliberate simplification.}

## Pitfalls
{Specific failure conditions when copied blindly.}

## Next actions
{Learning or applicability-check suggestions; no automatic invocation.}
````
