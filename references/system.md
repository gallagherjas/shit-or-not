# System-level review

## Scope

Inspect module responsibilities, dependencies, and data ownership. Trace the modules a developer must change to complete a typical task. Identify architectural units—packages, services, libraries—by their responsibilities.

Review function readability at the implementation level and rule execution at the feature level. Report a system-level problem only when there is evidence of effects across modules.

## Questions and evidence

| Area | What to ask | How to investigate |
|---|---|---|
| Responsibility boundaries | Does each rule have a clear owner? Do modules expose too much of their internals? | Trace calls from entry points and public interfaces. Check whether business code bypasses interfaces to read internal data or manipulate internal state. |
| Dependency direction | Are high-level rules constrained by unrelated implementation details? Are there actual dependency cycles? | Follow imports, calls, registrations, and configuration. Distinguish type references from runtime and build dependencies. |
| Data and state ownership | Who can change critical state? How are multiple copies kept consistent? | Locate definitions and writes. Check synchronization protocols, invalidation mechanisms, and the source of truth. |
| Shared infrastructure | Do shared modules tie unrelated business areas together? | Inspect consumers, business-specific branches, and global state. Identify who is affected by a local change. |
| Change propagation | Does a reasonable change require extensive coordination across boundaries? | Choose a change scenario grounded in actual functionality. List the places that must change together and why. Use history, when available, to verify which files actually changed together. |
| Builds and configuration | Are environment assumptions clear and builds reproducible? | Compare build entry points, dependency declarations, configuration, and documentation. Check how direct and transitive versions are fixed in development and CI through lockfiles, pins, or equivalent mechanisms. Identify implicit requirements and their effects. Do not claim the project cannot build without trying the build. |
| Project documentation | Can developers find the setup steps, environment requirements, and key constraints? | Compare available guidance with actual entry points and configuration. Identify knowledge developers must rediscover; equivalent guidance can replace a README. |

Keep the dependency map focused on the modules and relationships needed to explain behavior.

## Common signals and counterevidence

- **The same business rule appears in several layers:** Establish whether each copy independently determines the outcome. Before recommending consolidation, distinguish boundary input validation from enforcement of the core rule.
- **Dependency cycles:** Verify whether they obstruct initialization, isolation, or changes. A cycle alone does not make a project unmaintainable.
- **Multiple sources of mutable state:** Look for explicit authority, synchronization, and invalidation. Caches, read models, and event projections are not defects simply because they store duplicate data.
- **Customer-specific or business-specific branches in shared modules:** Determine whether conditions keep spreading without a stable extension boundary. A suitable adapter may isolate the differences.
- **A small project has no formal layering:** Do not require more modules or services when responsibilities are understandable, changes remain local, and verification is effective.
- **Complex platform constraints or external dependencies:** Check how the code isolates these constraints. Separate platform requirements from maintenance work introduced by the implementation.

## Requirements for a finding

Show the relationships across modules and their maintenance consequences. For shared core modules, establish which internal details callers must know or which changes they must coordinate.

Before calling a codebase a systemic mess, verify that similar structural obstacles recur across major modules or representative flows. One bad module, untidy directories, or numerous local issues do not establish effects across modules. Disclose gaps if the review has not covered the main boundaries.
