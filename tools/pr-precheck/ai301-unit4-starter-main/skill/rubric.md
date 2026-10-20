# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Plan fidelity | Compare the issue requirements, plan.md scope and deviation notes, changed files and behavior in the diff, and PR description. | The implementation addresses the issue and matches the plan or explicitly documented, justified deviations. The description accurately identifies any remaining scope gaps. Reject unsupported claims of plan fidelity or unexplained material drift. | required |
| Test evidence | Compare the plan's verification steps with the package's test commands, results, regression evidence, and changed behavior in the diff. | Evidence demonstrates the relevant behavior was exercised and reports observable outcomes. Required repository checks were run when applicable, or any omissions are explicitly explained with sufficient alternative evidence. Honest, bounded limitations alone do not fail this check. | required |
| Diff quality | Inspect changed files, hunks, generated artifacts, unrelated modifications, and the issue's intended scope. | The change is reviewable and focused on the issue. Unrelated changes or generated debris do not obscure the implementation. Necessary supporting changes are allowed when their purpose is clear. | required |
| Standards and communication | Compare the PR title and description with the diff, issue discussion, and repository standards or PR-template requirements in repo-facts. | The PR communicates its actual changes and verification truthfully, satisfies applicable repository requirements, and provides required disclosures. Concise descriptions are acceptable if they convey the necessary information. | required |

## Verdict rule

Grade every check as `pass`, `fail`, or `unclear`, using a specific fact or quotation from the package as evidence.

- **accept:** Every required check passes.
- **reject:** At least one required check fails or is unclear.
- Preferred checks, if introduced later, never change the verdict.
- Treat `unclear` as failing for verdict purposes because unverifiable claims cannot establish submission readiness.
- Evaluate disclosed limitations by their actual impact on the issue and the evidence. Do not automatically reject a PR merely because it honestly identifies unfinished or out-of-scope work.
- Never substitute formatting preferences, description length, or commit count for evidence about the implementation.
