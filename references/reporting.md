# Reporting and verdicts

## Verdict scale

| Verdict | Required evidence |
|---|---|
| no shit | Within the representative scope reviewed, developers can explain responsibilities and behavior, predict the effects of changes, and verify the results. State that scope in the report. |
| little shit | Maintenance obstacles exist, but their boundaries are identifiable. Recurring structural problems within or across modules have not been established. |
| some shit | Related structural obstacles recur within a module or feature, making it difficult to understand, change, or verify. State the confirmed scope of impact. |
| holy shit | Obstacles across boundaries recur in major modules or representative features. Ordinary changes require extra coordination or knowledge of implicit conventions. Provide the supporting evidence. |
| insufficient evidence | Key source code, call paths, context, or representative coverage is missing, so the requested scope cannot be assessed. Confirmed local findings may still be reported. |

Keep the verdict within the evidence's scope. For a file or module review, say that the file or module is maintainable within the reviewed scope. If local problems are clear but the wider picture is not, report insufficient evidence for the project as a whole alongside the confirmed mess in the affected module. Use this scale; do not average file scores or invent uncalibrated overall scores, percentiles, or rankings.

## Default report structure

Use the user's language and adjust the length to the review's scope.

1. **Verdict:** State the conclusion and scope, and summarize the maintenance obstacles. If a verdict is not possible, explain why the evidence is insufficient.
2. **Coverage:** List the modules, feature flows, and verification methods examined. Disclose coverage gaps that affect the judgment.
3. **Findings and recommendations:** Order findings by maintenance impact, group those with the same root cause, and provide evidence and a recommended change for each finding.
4. **Limitations:** List unresolved questions and the evidence needed to answer them. If no substantive problems were found, keep the report short and omit unsupported recommendations.

These elements may fit in a single paragraph. Link to files in the current environment and verify line numbers. When citing command results, state whether the command ran, including any failures or inability to execute it.

## Priorities

Rank findings by maintenance consequences, importance to core flows, affected scope, and known trigger frequency, then consider the cost of the change. Mark unknown frequency as unknown.

Suggested labels are "address first," "address next," and "monitor / verify." Prioritize the core maintenance obstacles and describe concrete changes.
