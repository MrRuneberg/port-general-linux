# Rebuilding and binary-only routes

## When source is available

Treat the source project as canonical. Identify its engine/compiler version, build system, SDK, submodules, generated code, native dependencies, assets, licenses, and project-specific instructions. Establish a clean baseline build before modifying the project.

Use the matching official engine toolchain and supported Linux target first. Read build scripts rather than guessing commands. Preserve reproducible configuration, make small changes, and keep generated files separate from hand-maintained source. Port platform-specific dependencies only where the original Linux build path is insufficient.

If a game uses a custom engine, trace the startup and platform layer before changing rendering, timing, or threading. Avoid replacing an entire subsystem until evidence shows that smaller changes will not work.

## When source is unavailable

First distinguish these objectives:

- **Play the existing Windows build:** evaluate Wine/Proton or another suitable compatibility route when acceptable. This preserves the Windows executable and is not a native port.
- **Produce native Linux x86_64 output:** establish the executable architecture, APIs, runtime assumptions, and whether a suitable translation/recompilation technique exists. Expect substantial game-specific engineering.
- **Rebuild or change game logic:** this normally requires source or a separately reconstructed implementation. Extracting assets or decompiling functions does not automatically restore a maintainable source project.

Use binary translation or static recompilation only when the method fits the executable's instruction set, calling conventions, runtime behavior, and APIs. Explain the work needed for missing instructions, OS services, graphics/audio APIs, generated code, and runtime semantics. Do not force an unrelated game through a narrow tool simply because it is available.

## Build discipline

Keep a known-good original and a clear working diff. Use the target project's build system, preserve necessary compiler/linker flags, check return codes, and inspect the first meaningful error rather than hiding it. Separate compile-time failures, link errors, startup failures, and in-game behavioral failures. Record prerequisites and exact commands in the game workspace.

The documentation repository itself provides no build system or engine adapter.
