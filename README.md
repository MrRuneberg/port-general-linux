# port-general-linux

A documentation-only coding-agent skill for reverse engineering, porting, rebuilding, and optimizing Windows games for **native Linux x86_64**.

## Install

Install globally for agents supported by the [Skills CLI](https://skills.sh/docs/cli):

```bash
npx skills add 'https://github.com/MrRuneberg/port-general-linux/tree/main/plugins/port-general-linux/skills/port-windows-game-linux' --global --agent '*' --yes
```

For unsupported agents, copy the skill directory into their documented skills location.

## Use the skill

Start with [the skill instructions](plugins/port-general-linux/skills/port-windows-game-linux/SKILL.md) and consult the relevant references. Work in the game's own source tree or a separate per-game workspace, not in this documentation repository.

Before substantial changes, the skill requires an explicit feasibility verdict: **GO**, **CONDITIONAL**, or **NO-GO**, grounded in evidence and constraints. A verdict assesses the current route; it does not guarantee a successful port or declare permanent impossibility.

This repository intentionally contains no game implementation, detector, recompiler, engine adapter, build scripts, test harness, benchmark automation, or CI workflow. The agent investigates the actual game, uses its available tools, makes game-specific changes, and reports evidence and limitations.

A native Linux port, source rebuild, binary recompilation, and running a Windows build through Wine/Proton are different outcomes. Do not claim one when only another was achieved.

## Documents

- [Skill instructions](plugins/port-general-linux/skills/port-windows-game-linux/SKILL.md)
- [Architecture](ARCHITECTURE.md)
- [Specification](SPEC.md)
- [Reverse engineering](plugins/port-general-linux/skills/port-windows-game-linux/references/reverse-engineering.md)
- [Linux x86_64 porting](plugins/port-general-linux/skills/port-windows-game-linux/references/linux-porting.md)
- [Rebuilding](plugins/port-general-linux/skills/port-windows-game-linux/references/rebuilding.md)
- [Optimization](plugins/port-general-linux/skills/port-windows-game-linux/references/optimization.md)
- [Workflow, feasibility, and reporting](plugins/port-general-linux/skills/port-windows-game-linux/references/workflow.md)

## Safety

Do not upload, publish, or redistribute game files or builds without authorization and explicit approval. Keep proprietary game assets and generated artifacts out of version control.
