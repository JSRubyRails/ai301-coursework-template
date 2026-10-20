# Procedure: how this tool grades a PR package

## Read order

1. Determine whether the tool is running in live mode or eval mode. Evaluate exactly one PR package per run.
2. In live mode, read `scope.md` first. Stop without grading if the repository is outside scope or the `Repo:` line contains a placeholder. Read `voice-guide.md` and record its communication requirements. In eval mode, ignore both files and use only the supplied bundle.
3. Read `rubric.md` to identify the checks, their pass conditions, weights, and verdict rule. Read `references/evidence-guide.md` to locate the evidence for each check. Refuse to grade if the rubric or procedure has no substantive content.
4. Read the issue context and repository facts. Record the reported problem, expected behavior, repository checks, PR-template requirements, and applicable disclosure rules.
5. Read `plan.md` before inspecting the diff. Record the intended scope, expected changed files, implementation steps, verification plan, and documented deviations.
6. Read the complete branch diff and commit information. In live mode, use `git diff main...HEAD` from the working copy when `main` is the default branch. Record every changed file and the behavior introduced or removed.
7. Read the test evidence. Record commands, observed results, relevant regression coverage, failures, and explicitly disclosed omissions.
8. Read the PR title and description last. Record claims about scope, implementation, tests, limitations, and issue references. Compare these claims with the evidence already collected.

Read the plan before the diff and description to avoid treating the author's claims as proof of compliance.

## Evidence gathering

### Plan fidelity

- Extract the issue's required behavior and the plan's stated implementation boundary.
- List the files and behaviors changed in the diff.
- Compare each material change with the plan and its deviation notes.
- Identify missing planned work, additional behavior, and deviations that were or were not disclosed.
- Compare the PR description's scope claims with the actual changes.
- Record the exact file, behavior, plan statement, or description claim supporting the grade.

### Test evidence

- Extract the plan's verification steps and the repository's applicable test requirements.
- Identify test commands, reported results, regression cases, and any test-related changes visible in the diff.
- Determine whether the evidence exercises the issue's relevant behavior rather than merely reporting that tests passed.
- Identify required checks that were not run, failures without explanation, and unsupported claims.
- For disclosed omissions, assess whether the remaining evidence adequately verifies the submitted change.
- Record the specific test command, outcome, or missing evidence supporting the grade.

### Diff quality

- Review the changed-file list and relevant hunks.
- Identify unrelated changes, generated artifacts, accidental modifications, or changes that obscure the implementation.
- Distinguish necessary supporting edits from unrelated work using the issue and plan.
- Determine whether a reviewer can identify the actual fix and its supporting tests.
- Record the changed files or hunks supporting the grade.

### Standards and communication

- Read repository standards and PR-template requirements from the issue context or repo-facts block.
- Compare the PR title and description against those requirements.
- Verify that the description accurately represents the diff, test results, and remaining limitations.
- Check required disclosures and issue references when the repository explicitly asks for them.
- In live mode, separately report any violations of `voice-guide.md`.
- Record the exact requirement, statement, or omission supporting the grade.

In eval mode, never fetch missing evidence from outside the package.

## Check execution

Execute the rubric checks in their listed order:

1. Plan fidelity
2. Test evidence
3. Diff quality
4. Standards and communication

For each check:

1. Retrieve the evidence collected for that check.
2. Compare the evidence against the check's written pass condition.
3. Assign `pass` when the available evidence satisfies the condition.
4. Assign `fail` when the evidence establishes that the condition is violated.
5. Assign `unclear` when essential evidence is missing or insufficient to determine whether the condition is satisfied.
6. Write one evidence line identifying the specific fact, quotation, or absence that determined the grade.

Do not automatically fail a package because it reports a limitation. Determine whether the limitation materially violates the applicable pass condition.

Do not invent new checks, standards, or requirements.

Do not substitute description length, commit count, or formatting preferences for implementation evidence.

Reuse previously gathered evidence rather than rereading the entire package unless a contradiction requires verification.

Grade every check, even when an earlier required check has already failed.

## Verdict assembly

1. Collect all check grades in the same order as `rubric.md`.
2. Treat `unclear` as failing for verdict purposes.
3. Return `accept` only when every required check passes.
4. Return `reject` when any required check fails or is unclear.
5. Preferred checks, if present, never independently change the verdict.
6. When rejecting, identify the first failing or unclear required check in rubric order as the primary blocker. Quote its decisive evidence in the readable summary.
7. Report other failing checks and relevant limitations without changing the primary-blocker selection rule.
8. In live mode, report voice-guide violations separately unless they also violate a rubric check.
9. End with the exact fenced JSON structure specified in `SKILL.md`, including the package identifier, every check's name, grade, and evidence, and the binary verdict.
10. Do not place any text after the final JSON block.

Apply the rubric's written conditions consistently. If a procedure step cannot be executed because its required evidence is unavailable, report that limitation and grade the affected check according to the rubric rather than inventing evidence.
