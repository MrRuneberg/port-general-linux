# Architecture

## Repository boundary

This repository is a documentation-only coding-agent skill. It contains the skill prompt, architecture and scope documents, and reference guides. It does not implement game detection, reverse engineering, compilation, recompilation, engine adapters, tests, or automated build workflows.

All game-specific source changes, scripts, builds, disassembly databases, logs, and generated output belong in the target game's own repository or a separate per-game workspace.

## Skill workflow

1. **Intent and constraints:** determine the requested result, target Linux x86_64 environment, available source/assets, and legal or technical constraints.
2. **Evidence gathering:** inspect source, metadata, build files, binary format, imports, dependencies, and runtime behavior as appropriate. Keep observations separate from hypotheses.
3. **Architecture reconstruction:** identify engine and subsystem boundaries, executable entry points, platform-specific code, external services, and relevant data/control flow.
4. **Feasibility gate:** before substantial changes, issue GO, CONDITIONAL, or NO-GO with supporting evidence, confidence, unknowns, and prerequisites/blockers. Insufficient evidence means CONDITIONAL, not an unsupported claim.
5. **Route selection and implementation:** choose a justified game-specific route, preserve originals, make focused changes in the game's workspace, and resolve the earliest blocking failure first. Wine/Proton is compatibility, not a native port.
6. **Agent-led verification:** use the target project's build commands, tools, and direct runtime checks. This repository provides no test runner or validation automation.
7. **Reporting:** record commands, changes, observed outcomes, assumptions, unresolved issues, and whether new evidence changed the feasibility verdict.

## Technical boundaries

- The output target is native Linux x86_64 unless the user explicitly changes it.
- No engine, game, graphics API, executable format, or porting technique is assumed to be supported in advance.
- Prefer an existing source project and its matching build system when available.
- Treat packaged binaries as evidence about behavior, not as recovered source.
- Distinguish guest Windows APIs that the game expects from host platform integrations that must be replaced for Linux.
- Use project-specific architecture decisions; do not impose a shared runtime or implementation framework.

## Working principles

Use evidence before assumptions, small reversible changes before broad rewrites, and direct measurements before optimization claims. Keep game-specific artifacts out of this documentation repository. State uncertainty and feasibility limits explicitly.
