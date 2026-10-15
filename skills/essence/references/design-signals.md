# Essence Candidate Signals

Use these signals to find candidates, never as proof by themselves.

## Strong candidates

- A cross-module interface or protocol shapes several subsystems.
- A design document or RFC explains a non-obvious architecture decision.
- Direct tests cover lifecycle, fallback, failure, or compatibility behavior of the design.
- Implementation comments explain why a structural choice exists.
- A core algorithm or state machine controls an important project path.

## Supporting signals

- README presents a specific architecture claim.
- The project differs from comparable tools in a documented way.
- A file is unusually large for its responsibility and contains non-trivial coordination.
- A public API exposes an unusual but repeated contract.

## Exclusions

Do not treat clean formatting, language choice, repository popularity, modern dependencies, generic CRUD, or an isolated utility as a standout design.

## Candidate note

For each candidate, record the signal, the direct evidence that needs checking, and the reason it could matter to another project. If the direct evidence is absent, retain it as a hypothesis or discard it.