# Implementation-level review

## Scope

Inspect files, components, and functions alongside their callers and dependencies. Verify how the code is used and assess the effort needed to understand and change it. Support architectural claims with evidence across modules.

## Questions and evidence

| Area | What to ask | How to investigate |
|---|---|---|
| Responsibilities and cohesion | Does one unit handle unrelated responsibilities that change independently? | Compare callers, shared state, and reasons for changes in different parts of the logic. Explain how a split would reduce the effort to understand the code or narrow the impact of changes. |
| Control flow | Does the outcome depend on branches, jumps, or execution order that are hard to follow? | Trace actual inputs to outputs. Inspect how nesting, early returns, exceptions, and asynchronous branches interact. Treat line count only as a clue. |
| State and side effects | What does a call change, and does its contract tell the caller? | List external state reads and writes, input mutations, shared mutable objects, and hidden I/O. Check whether correct use depends on knowing the order of operations. |
| Duplication | Must copies of logic stay in sync? Have they diverged, or are they likely to? | Compare business semantics and differences. Avoid forcing an abstraction onto code that looks similar but changes independently. |
| Abstraction overhead | Do indirection, generalization, and parameter combinations reduce actual complexity? | Inspect real consumers. Look for catch-all utilities, mode switches, excessive forwarding, and interfaces that expose internal details. |
| Local contracts | Are inputs, outputs, failures, and lifecycle requirements clear? | Compare declarations, implementations, and callers. Check return paths, sentinel values, implicit preconditions, type ambiguity, conversions, and error handling. Verify external inputs are validated here or upstream, accounting for existing type guarantees. |
| Resources and asynchronous work | Is cleanup appropriate after success, failure, cancellation, and repeated execution? | Based on actual usage, inspect acquisition and release of connections, files, timers, subscriptions, and tasks. Check whether stale results can overwrite current state. |
| Verification and diagnosis | Can key behavior be verified and failures diagnosed? | Inspect existing tests, compiler or lint checks, and diagnostic points. Confirm tests cover observable outcomes and static checks catch relevant errors. Missing tests do not automatically mean the code is untestable. |

## Common signals and counterevidence

- **Large files or functions:** Length alone is not a finding when the logic is coherent, contracts are clear, responsibilities are stable, and behavior can be verified.
- **Dense expressions or deep nesting:** Identify expressions or paths that are hard to follow or easy to miss. Check evaluation order, side effects, and whether branches simply enumerate required business cases.
- **Magic values, vague names, or inadequate comments:** Explain the misunderstanding or implicit contract they create. Check whether non-obvious decisions have an accessible, accurate rationale. Do not stop at cosmetic suggestions.
- **Inconsistent style or comment language:** Check whether naming, formatting, or comment language impedes the team's understanding, using its conventions and actual needs.
- **No formal interfaces or design patterns:** Verify calling contracts and change boundaries. Explain the specific obstacle an added abstraction would remove.
- **Static methods, singletons, or global state:** Examine lifecycle, mutability, and implicit dependencies. Do not judge by form alone.
- **Return values vary by branch:** First check for an explicit union type, discriminant, or calling convention before deciding the contract is ambiguous.
- **Limited automated checks:** Assess behavioral risk and existing verification methods. Where tests exist, verify which business outcomes they cover.
- **Apparently unused or redundant code:** Inspect unused variables, parameters, results, unreachable branches, and commented-out code. Verify callers, dynamic references, public contracts, and side effects before recommending deletion; preserve compatibility behavior with consumers.

## Findings and recommendations

Identify the relevant execution path, calling relationship, or state change and explain its maintenance consequences. Assess defect severity separately from maintainability; a vulnerability or bug alone does not justify labeling the entire codebase a mess.

Prefer removing unused logic, consolidating duplicate rules, clarifying contracts, or narrowing the scope of mutable state. When recommending a split, an abstraction, or more tests, explain the obstacle it addresses and preserve business behavior and compatibility contracts. Base recommendations on maintenance consequences rather than refactoring checklists driven by line counts or naming preferences.
