---
name: port-windows-game-linux
description: Reverse engineer, assess feasibility, port, rebuild, or optimize Windows games for native Linux x86_64 using game-specific evidence and tools.
---

# Work on a Windows game for native Linux x86_64

Use these instructions for the user's actual game and requested outcome. This skill provides workflow and engineering guidance; it does not supply a game detector, recompiler, engine adapter, build scripts, or test automation.

## Core rules

- Target a native Linux x86_64 result unless the user explicitly requests a different outcome.
- Infer the task from the user's request. Do not make them choose again when their goal is clear.
- Inspect the supplied game and project before deciding how to proceed.
- **Assess feasibility before making porting changes.** Issue an explicit GO, CONDITIONAL, or NO-GO verdict supported by evidence. Do not merely list risks or assume the game is portable.
- Prefer original source and the matching engine/toolchain when available.
- Treat reverse engineering as evidence gathering, not proof that source can be recovered or that a port is feasible.
- Work in the target game's own repository or a separate workspace. Preserve the original and make incremental, reversible changes.
- Use the project's actual build and runtime tools. Never claim success for a build, feature, or milestone that was not observed.
- Do not add general-purpose tooling to this skill repository; game-specific implementation belongs in the game workspace.

## Workflow

### 1. Establish inputs and constraints

Locate the user's game, source tree, executable, assets, build instructions, and existing port work. Identify the requested outcome, target Linux x86_64 environment, source availability, license constraints, dependencies, and external services or hardware requirements.

Ask only for missing information or approval that materially blocks progress. Do not ask the user to repeat a clear goal.

### 2. Inspect and reconstruct

Read project documentation and build files before changing anything. Determine the engine or custom framework, language, compiler, architecture, entry point, asset pipeline, libraries, graphics/audio/input systems, filesystem assumptions, platform APIs, networking, and distribution format as applicable.

For binary-only inputs, begin with static inspection: file format and architecture, sections, imports/exports, strings, symbols, resources, dependencies, and disassembly. Build a map of relevant functions and data flow. Use dynamic analysis only when needed and safe, and record how observations were obtained. See [reverse engineering](references/reverse-engineering.md).

### 3. Issue an explicit feasibility verdict

Before porting changes, state whether the requested native Linux x86_64 outcome is realistically achievable with the available inputs, tools, time/constraints, and required behavior. Use one of these verdicts:

- **GO — Feasible route identified:** concrete evidence supports a viable path, usually an editable source project with a usable Linux build path or a well-understood set of platform dependencies.
- **CONDITIONAL — Potentially feasible with blockers:** a route exists, but major assumptions or prerequisites remain unresolved, such as unavailable SDKs, unsupported APIs, missing source, incomplete reimplementation, proprietary services, or unverified runtime behavior. Name what must be established first.
- **NO-GO — Not currently feasible under the stated constraints:** no credible route has been identified with the available source, binary, tools, and constraints, or a legal/access restriction blocks the requested approach. Explain the evidence and what would need to change to reassess.

Base the verdict on concrete findings about source availability, binary architecture, engine/toolchain, APIs, dependencies, protection, external services, and target-platform support. State confidence and separate facts from hypotheses. A GO is not a guarantee of successful gameplay; a NO-GO means not feasible under current conditions, not necessarily impossible in principle.

If the evidence is insufficient for a reliable decision, use CONDITIONAL and identify the specific missing evidence. Do not begin a speculative rewrite after a NO-GO. Present the verdict and recommended route before substantial changes.

### 4. Select the route and proceed

- **Source project:** establish a baseline build with its matching engine and tools, then make the required Linux changes.
- **Source available but Windows-bound:** identify the platform-dependent subsystems and replace or isolate them incrementally.
- **Packaged Windows binary:** determine whether the goal can be met by a native port, a specific recompilation/translation approach, or a compatibility run. These are distinct routes.
- **No viable native route:** explain the concrete blockers and alternatives. Do not present Wine/Proton as native Linux output.

Do not assume that engine detection, decompilation, an available library, or a successful compile proves the game is portable.

### 5. Port and rebuild

Keep changes focused and tied to observed behavior. Use the target project's build system and compiler where possible. Address Linux x86_64 ABI and platform assumptions, libraries, paths, case sensitivity, threading, synchronization, timing, rendering, audio, input, storage, networking, and packaging only as relevant to this game. See [Linux porting](references/linux-porting.md) and [rebuilding](references/rebuilding.md).

Resolve the earliest reproducible failure before making broader changes. Keep a concise PORTING_LOG.md in the game workspace for multi-stage work.

### 6. Verify the result

Use existing project checks and direct build/runtime checks where available. Verify relevant milestones, such as startup, rendering, controls, audio, saves/configuration, networking, clean exit, and packaging. Compare behavior with the Windows build or reference captures when possible.

If required hardware, source, SDKs, accounts, or services are unavailable, state what could not be verified. This repository contains no test harness or automated verification tools.

### 7. Optimize against measurements

Define the target metric and record a baseline under repeatable conditions. Profile before editing, make one focused change at a time, repeat the same workload, and check correctness and quality regressions. See [optimization](references/optimization.md). If reliable measurements are unavailable, label the result unverified.

### 8. Report

Start the report with the feasibility verdict, confidence, supporting evidence, and main blockers. Then summarize the route, findings, changes, exact commands, build/runtime observations, and remaining work. State whether the outcome is a native port, source rebuild, binary translation/recompilation, or compatibility run. Separate facts, hypotheses, and unverified claims.

## Safety and ownership

Do not download or redistribute games. Ask before installing system-wide dependencies, uploading files, deploying, or publishing anything. Keep proprietary assets, game binaries, saves, credentials, and generated artifacts out of version control.
