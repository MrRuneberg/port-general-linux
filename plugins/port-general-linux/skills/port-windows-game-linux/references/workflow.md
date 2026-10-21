# Feasibility assessment and workflow

## Feasibility verdict comes first

Before porting or rewriting code, assess whether the requested native Linux x86_64 outcome is realistically feasible with the available game files, toolchain, dependencies, and constraints. Record the verdict in the game workspace.

- **GO — Feasible route identified:** evidence supports a credible technical route and its major prerequisites are available.
- **CONDITIONAL — Potentially feasible with blockers:** a route may work, but major dependencies, technical assumptions, source availability, unsupported APIs, or runtime requirements remain unresolved.
- **NO-GO — Not currently feasible:** no credible route fits the current inputs and constraints, or a legal/access restriction blocks the requested approach.

The verdict must cite concrete evidence: source availability, engine/toolchain, architecture, graphics and system APIs, dependencies, protection, online services, and Linux target support. State confidence and unknowns. If evidence is insufficient, choose CONDITIONAL and identify what information would change the decision. NO-GO describes present constraints, not impossibility in principle. Do not start a speculative rewrite following NO-GO; explain which inputs or constraints would need to change.

A GO is not a promise that the game will build or play correctly. Update the verdict if new evidence materially changes the assessment.

## Establish the work

Identify the goal, source and assets, build instructions, engine/version, runtime dependencies, binary architecture, target distribution, external services, and legal constraints. Do not ask the user to repeat a clear request.

## Choose the route

Prefer the least speculative route that meets the request:

1. Build the source project with its matching toolchain and then port platform-specific code as needed.
2. Port source-available custom engines or platform-bound dependencies incrementally.
3. For packaged binaries, assess a technically appropriate native translation/recompilation method.
4. Use Wine/Proton only when running the Windows build is acceptable; describe it as compatibility, not a native port.

Do not infer support from a filename, engine marker, successful compile, or another game's result.

## Keep durable notes

For work spanning sessions, maintain a concise PORTING_LOG.md in the game workspace. Include:
- goal and intended Linux x86_64 output;
- feasibility verdict, confidence, supporting evidence, blockers, and reassessment triggers;
- input files/source availability and relevant versions;
- baseline build/runtime result;
- architecture findings;
- changes made and rationale;
- commands run and observed outcomes;
- first unresolved blocker and next concrete step.

Do not put proprietary game material, credentials, full memory dumps containing personal data, or generated binaries in this documentation repository.

## Work in small steps

Choose milestones tied to the requested outcome. Build or run at the smallest useful interval and diagnose the earliest failing stage. Keep changes reversible and avoid mixing unrelated refactors with porting work. Use the target project's existing checks when available; otherwise perform targeted direct checks. The skill repository itself has no test runner or test automation.

## Completion report

Report the feasibility verdict and whether it changed during the work, the chosen route, why it fits the evidence, main findings and changes, exact commands, what built and actually ran, optimization results, and remaining blockers. Use precise outcome labels: native Linux port, Linux source rebuild, binary translation/recompilation, or Windows compatibility run. If only compilation succeeded, say so. If the game could not be run, do not claim gameplay works.
