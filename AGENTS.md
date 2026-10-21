# Repository instructions

- This repository contains only the coding-agent skill and its documentation.
- Keep it focused on reverse engineering, porting, rebuilding, and optimizing Windows games for native Linux x86_64.
- Do not add game implementations, engine adapters, detectors, build or setup scripts, test harnesses, benchmark automation, or CI workflows. Such tools belong in the target game's own workspace and are outside this repository's scope.
- Keep the README, specification, architecture, skill, and references consistent. Prefer specific instructions over claims of universal support.
- The skill must investigate each game's actual source, binary, engine, dependencies, and APIs rather than assuming a fixed engine or backend.
- Act on a clear request without asking the user to repeat the desired operation. Ask only for information or approval that materially blocks progress.
- Distinguish native Linux output from Wine/Proton compatibility, source rebuilds, and binary recompilation.
- Preserve original files, avoid destructive changes, and record meaningful findings in the game workspace.
