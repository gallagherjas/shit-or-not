# Shit or Not

English | [简体中文](README.zh-CN.md)

An Agent Skill for assessing how hard code is to understand, change, and verify.

Ask for a review of a project, module, or file. You receive findings with code locations, maintenance consequences, affected scope, and prioritized recommendations in your language.

## Review approach

- **System:** Module boundaries, dependencies, state ownership, and the reach of changes.
- **Feature:** Complete flows, business rules, state transitions, and failure handling.
- **Implementation:** Control flow, side effects, duplication, contracts, and verification.

## Verdicts

| Verdict | Meaning within the reviewed scope |
|---|---|
| no shit | Developers can understand, change, and verify the code. |
| little shit | Maintenance obstacles have identifiable boundaries. |
| some shit | Related structural obstacles recur within a module or feature. |
| holy shit | Recurring obstacles span major modules or representative flows. |
| insufficient evidence | The reviewer lacks key code, context, or coverage needed for a verdict. |

## license

[MIT License](LICENSE).
