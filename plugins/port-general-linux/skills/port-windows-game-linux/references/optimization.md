# Game optimization workflow

Optimize only the target and metric requested by the user. A port that is incorrect or unstable is not an optimization success.

## Measure first

Record a baseline using a repeatable workload and the same machine, operating system, graphics driver, game build, resolution, settings, scene, and warm-up period. Choose relevant metrics: frame time and frame pacing, CPU/GPU time, memory, load time, stutter, I/O, power where measurable, or packaged size.

Profile to identify the limiting subsystem before changing code. Separate CPU, GPU, storage, asset decoding, shader compilation, synchronization, and external-service delays. Avoid inferring a bottleneck from a single noisy sample.

## Make controlled changes

- Change one likely bottleneck at a time.
- Prefer algorithmic or data-flow improvements before platform-specific micro-optimizations.
- Keep rendering, physics, timing, saves, networking, and deterministic behavior correct.
- On Linux, account for compiler settings, allocator behavior, thread scheduling, graphics-driver and API overhead, synchronization, and asset path/layout changes where relevant.
- Preserve a way to compare against the previous build.

## Compare and report

Repeat the same workload and capture the same metrics after each change. Include absolute values and percentage change where meaningful, plus the measurement method and environment. Check gameplay correctness and quality regressions. Reject or qualify changes where benefits are within measurement noise or results are not repeatable.

If a metric cannot be measured reliably, state that explicitly and describe the change as unverified. Do not claim performance improvements without comparable measurements.
