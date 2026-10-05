# Feature-level review

## Scope

Choose a complete behavior, such as submitting a request or importing data. Trace its triggers, rule execution, state changes, and outcome across directories and modules.

Assess whether a developer can explain and change the complete business behavior. Review module dependencies at the system level and function clarity at the implementation level. Judge maintenance cost by the work needed to coordinate the flow; module count is only a navigation clue.

## Selecting and tracing flows

Use entry points, documentation, and code to identify core flows, then inspect flows that cross boundaries or involve complex state. Investigate the user's reported concern first, then examine normal flows to establish its reach. Support claims that an area changes frequently with historical evidence.

Record each flow's triggers, rule ownership, state writes, external side effects, and success and failure exits. Follow the consumers of asynchronous callbacks, events, jobs, and subscriptions until the business outcome can be explained. Mark the boundary where external behavior is not visible.

## Questions and evidence

| Area | What to ask | How to investigate |
|---|---|---|
| Rule ownership | Who determines the outcome? Have business rules diverged? | Find implementations and callers of the same rule. Compare semantics, input sources, and responsibilities at each boundary. |
| State transitions | Are states valid and transition conditions explicit? | Trace state reads, writes, and transition entry points. Check combinations of boolean flags, implicit ordering, and the source of truth. |
| Interaction contracts | Do callers and callees depend on extensive unwritten conventions? | Compare parameters, return values, error semantics, event payloads, and caller handling. Check whether correct use requires knowledge of internal details. |
| Failure paths | Can the resulting business state be explained after a partial failure? | Trace exceptions, rollback, compensation, and partial success. Check for hidden errors and resources left behind. |
| Repeated and concurrent execution | Can retries, duplicate triggers, or parallel execution violate constraints? | Where these triggers are possible, inspect transactions, deduplication, locks, versioning, or idempotency. Do not assume every flow needs these mechanisms. |
| Change and verification | What must change together for a reasonable business requirement, and how can correctness be confirmed? | Use the actual flow to identify rule and contract changes. Check whether existing behavior tests, assertions, or other verification methods cover the key outcomes. |

## Common signals and counterevidence

- **Similar validation in several places:** Determine whether the checks express the same business fact. Input validation at different trust boundaries is not necessarily redundant.
- **A feature passes through many forwarding layers:** Verify the contract, authorization, or isolation work each layer performs. Explain the extra tracing needed to understand the behavior.
- **New requirements accumulate special cases:** Locate interactions between conditions and determine how far they spread. Compatibility branches with a clear scope and conditions for retirement may be reasonable technical debt.
- **Exceptions are swallowed or failures appear successful:** Check how callers detect failure, and verify the fallback contract and resulting business state.
- **The feature cannot be verified in isolation:** Determine whether this comes from excessive infrastructure coupling or necessary integration behavior. Integration tests can provide effective assurance; do not insist on unit tests.

## Requirements for a finding

Identify obstacles involving rules, state, or collaboration between components. Explain how they make the feature harder to understand, change, or verify. For a risk that has not been reproduced, state its trigger conditions without presenting it as an observed incident.

Group issues within a feature when they stem from scattered rules. Before reporting system-level effects, verify that the same root cause affects other features or modules. If only one flow was reviewed, limit the conclusion to that flow.
