# Specification

## Purpose

Provide coding-agent instructions and technical references for reverse engineering, porting, rebuilding, and optimizing Windows games for native Linux x86_64.

## Scope

The repository is documentation only. Its deliverable is the skill and the workflow it teaches an agent to follow for a specific game. It has no executable implementation, engine detector, recompiler, build adapter, test suite, benchmark system, or CI pipeline.

The skill guides the agent to inspect the actual game, reconstruct relevant behavior from evidence, assess feasibility before changes, select a game-specific route to Linux x86_64, work incrementally in the target workspace, verify the result using the target project's own tools, measure optimizations, and report outcomes honestly.

## Required feasibility decision

Before substantial porting changes, the agent must issue one explicit verdict for the requested native Linux x86_64 outcome:

- **GO:** evidence supports a credible route and core prerequisites are available.
- **CONDITIONAL:** a plausible route exists but major blockers, assumptions, or missing evidence remain.
- **NO-GO:** no credible route fits the current inputs and constraints, or a legal/access restriction blocks the requested approach.

The verdict must cite evidence about source availability, engine/toolchain, executable architecture, platform APIs, dependencies, and relevant protection or service constraints. It must state confidence, unknowns, prerequisites, and what could change the verdict. If evidence is insufficient, choose CONDITIONAL. NO-GO refers to current conditions, not permanent impossibility. A GO is not a guarantee of a successful build or playable game.

## Target and terminology

- **Native port:** the game or reimplemented components build and run as a Linux x86_64 program.
- **Source rebuild:** the source project is built for Linux with the appropriate engine/toolchain. Platform porting may still be needed.
- **Binary recompilation or translation:** machine-code behavior is translated or recompiled through a specific technique; this does not automatically recover original source or remove API incompatibilities.
- **Compatibility run:** the Windows build runs through Wine/Proton or another compatibility layer. This is not a native Linux port.
- **Optimization:** a measured change to performance, load time, memory use, or binary/package size, with correctness considered.

The skill must not presume a particular game is portable or promise success.

## Constraints

- Target Linux x86_64 and account for Linux ABI, filesystem, libraries, process model, and platform services.
- Work from evidence and tools available for the actual game; do not claim a fixed set of supported engines or binaries.
- Keep changes and generated artifacts in the target game workspace.
- Do not upload or publish game material without authorization and explicit approval.
- Keep this repository limited to skill, architecture, scope, and workflow documentation.
