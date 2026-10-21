# Porting to Linux x86_64

## Target assumptions

The deliverable is a native Linux x86_64 build. Identify whether the original is 32-bit x86 or 64-bit Windows, and distinguish guest executable conventions from the Linux host ABI. Pointer width, structure layout, alignment, calling conventions, exception handling, thread behavior, and shared-library interfaces must be handled deliberately when bridging or translating code.

Do not assume Windows APIs or libraries are available on Linux. Map each required service to a suitable portable library, a Linux API, a source-level redesign, or a narrowly defined compatibility layer based on actual program behavior.

## Common platform differences

Investigate only differences the game relies on:

- **Filesystem:** case-sensitive paths, drive letters, separators, current working directory, Unicode paths, file locking, permissions, and save/config locations.
- **System services:** registry reads, environment variables, process/module APIs, timers, thread priorities, synchronization primitives, COM, window messages, and DLL loading.
- **Graphics:** Direct3D or other Windows APIs, shader formats, presentation, fullscreen/resolution, GPU capabilities, synchronization, and resource lifetime. Select a Linux-capable graphics path based on the actual API and available source or translation layer.
- **Audio:** device enumeration, format conversion, latency, mixing, streaming, timing, and device changes.
- **Input:** keyboard layouts, mouse capture, controllers, focus loss, hot-plugging, and remapping.
- **Networking and services:** socket behavior, TLS/certificates, online authentication, platform APIs, telemetry, and server dependencies.
- **Packaging:** shared-library dependencies, runtime assets, relative paths, permissions, launchers, configuration, and clean-machine requirements.

## Implementation strategy

1. Build the unmodified project for Linux, if possible, to establish the first blocker.
2. Identify Windows-specific code and dependency boundaries from actual source, imports, logs, and traces.
3. Replace one subsystem at a time behind existing abstractions where possible.
4. Prefer maintained, available libraries over reimplementing complex protocols or APIs without need.
5. Keep Linux-specific changes isolated, but do not add abstraction layers without a demonstrated use.
6. Rebuild and exercise the affected feature after each meaningful change.
7. Verify on the intended Linux distribution and x86_64 toolchain; note assumptions about drivers, desktop environments, and external libraries.

Use the original behavior as a reference for edge cases. A successful compile alone does not establish runtime compatibility. When source is unavailable, use reverse-engineering evidence to estimate what can be recreated and how much work is required.
