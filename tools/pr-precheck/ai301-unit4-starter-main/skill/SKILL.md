---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Determine whether exactly one pull request package is ready to submit.

A PR package contains a title, description, commits, diff, test evidence, implementation plan, and related issue context. Compare the implementation against the plan and issue requirements rather than judging presentation alone.

Answer only whether the package is ready to submit.

## Inputs and modes

Operate in exactly two modes.

**Live mode:**

Read the student's actual pull request materials:

- The issue and its discussion from the scoped repository.
- `plan.md`, including its scope, verification plan, and deviation notes.
- The complete branch diff relative to the repository's default branch, using `git diff main...HEAD` from the working copy when `main` is the default branch.
- The draft or existing PR title and description.
- Test commands, results, and regression evidence.
- Repository requirements, including its PR template and disclosure policies.

For a house-chain student, use the supplied house plan and reproduction package instead of the student's own plan and reproduction evidence.

Do not assume that a passing test or a confident PR description proves the implementation is correct.

**Eval mode:**

Use only the provided evaluation package bundle. Treat that bundle as the entire available evidence source.

Do not fetch external information, inspect a live repository, or import facts from another package.

Grade every rubric check and apply the complete verdict rule.

## The scope seam (live mode only)

Before gathering other live-mode evidence, read `scope.md`.

Identify the repository named on its `Repo:` line and follow the repository rules described there.

If the repository is an unfilled placeholder, stop without grading and instruct the student to complete the `Repo:` line.

Refuse to grade work belonging to a repository outside the declared scope.

Ignore `scope.md` entirely in eval mode.

## The voice seam (live mode only)

Read `voice-guide.md` and compare the outgoing PR title and description against its communication rules.

Report any violations in the readable summary, identifying the specific rule and offending text.

Voice-guide violations do not independently change the verdict unless a rubric check explicitly evaluates the same issue.

Ignore `voice-guide.md` in eval mode.

## Component reads

Read and execute the following components:

1. `rubric.md`: Defines the checks, pass conditions, weights, and verdict rule.
2. `references/evidence-guide.md`: Identifies where each evidence family is found in the PR package.
3. `procedure.md`: Defines the sequence for collecting evidence, grading checks, and producing the verdict.

Follow `procedure.md` exactly as written.

If the procedure omits a necessary step, report the gap rather than inventing an alternative workflow.

If `rubric.md` or `procedure.md` contains no substantive instructions, refuse to grade and explain which component is incomplete.

Do not create additional grading checks at runtime.

## Verdict and output

Produce exactly one binary verdict:

- `accept`: The PR is ready to submit according to the rubric.
- `reject`: The PR must be held because at least one required check fails or is unclear.

Grade every rubric check as `pass`, `fail`, or `unclear`.

Before the final JSON, provide a concise readable summary explaining the important evidence and any blockers.

End the response with the following fenced JSON block. Preserve its exact field names, ordering, and structure. Do not write anything after it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- **Evidence first:** Every grade must identify the specific fact, quote, or observable result supporting it.
- **Grade the implementation:** Compare the actual diff, behavior, and evidence with the issue and plan. Do not grade writing polish instead of substance.
- **Follow the rubric:** Apply each written pass condition consistently, even when an intuitive judgment differs.
- **Follow the procedure:** Execute the documented steps without silently inventing missing ones.
- **Treat uncertainty conservatively:** If a required claim cannot be verified, grade it `unclear` and treat it as failing for the final verdict.
- **Respect honest disclosures:** A documented limitation does not automatically require rejection. Evaluate whether the remaining evidence satisfies the relevant rubric check.
- **Keep the verdict binary:** Never output a third verdict or an `accept with reservations` result.