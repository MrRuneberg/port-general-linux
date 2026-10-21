# Reverse engineering workflow

## Establish evidence

Record input files, hashes where useful, file types, executable architecture, likely compiler/runtime, entry points, sections, imports/exports, embedded resources, strings, symbols, and dependencies. Keep tool output and notes in the game workspace.

For Windows PE files, inspect headers and imports with static tools such as `file`, `llvm-readobj`, `objdump`, PE-aware utilities, and a disassembler/decompiler such as Ghidra, IDA, or radare2 when available. Do not treat a DOS `MZ` marker as proof of a valid PE or infer a game's full engine from one marker.

Do not use `ldd` on an untrusted executable: some implementations may run code from the target. Use static ELF dependency inspection such as `readelf -d` when inspecting Linux binaries.

## Collect evidence for feasibility

Reverse engineering should answer whether a viable native port route exists, not merely describe the binary. Assess:

- Is source available and buildable, or is the input binary-only?
- What CPU architecture, compiler/runtime, and executable format are involved?
- Which Windows APIs, graphics/audio/input APIs, drivers, and external libraries are required?
- Is there a plausible Linux implementation or compatible portable dependency for each critical subsystem?
- Are online services, DRM, anti-cheat, activation, or unavailable server dependencies essential?
- Which capabilities are understood, and what would require substantial reimplementation?

Issue a **GO**, **CONDITIONAL**, or **NO-GO** feasibility verdict before substantial porting changes. Support it with observed evidence, confidence, unknowns, and explicit prerequisites or blockers. If there is not enough evidence, use CONDITIONAL rather than claiming feasibility or impossibility prematurely. Follow [the workflow](workflow.md) for verdict definitions.

## Reconstruct relevant behavior

Start from the requested feature or first observed failure. Follow callers and callees, imported APIs, data structures, resource lifetime, threads, and state transitions until behavior is explained well enough to change safely. Use symbol names, strings, RTTI, debug metadata, assertions, logs, or known engine conventions as clues, not proof.

Build an evidence-backed map of relevant subsystems: startup and main loop; module boundaries and external libraries; rendering and shader path; audio and input; filesystem, saves, configuration, and registry assumptions; threading, timing, synchronization, and lifecycle; and networking, protection, and external services if present.

Keep observed facts, hypotheses, and unresolved questions distinct. Prefer the smallest investigation that answers the current engineering question over exhaustively decompiling unrelated code.

## Static and dynamic analysis

Use static analysis first for unknown binaries. For dynamic work, use a debugger, tracing, API logging, controlled inputs, and crash dumps to collect evidence from the first failing operation. Execute binaries only when the user is authorized to use them and the environment is appropriate; isolate unknown or suspicious executables and avoid exposing credentials or personal data.

Record reproducible steps and relevant addresses, symbols, call stacks, and environment details. Do not assume a debugger trace from one build or machine applies to all versions.

## Limits

Decompiled output is an approximation and rarely recreates the original source structure. Native recompilation may require instruction translation, calling-convention and ABI handling, memory/runtime support, and extensive API implementations. If the game depends on unsupported graphics APIs, kernel behavior, drivers, protection, online services, or unavailable source, document the specific blocker rather than implying it can be removed automatically.
