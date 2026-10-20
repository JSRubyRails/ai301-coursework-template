# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

**Where it lives**

- **Eval mode:** Read the package's plan-context block, including the issue, planned scope, implementation boundary, expected changed files, and deviation notes. Compare these with the candidate PR's unified diff, changed-file list, and description.
- **Live mode:** Read `beat-1-sandbox/unit-3/plan.md`, including its Deviations section, the issue and its discussion on GitHub, and the complete branch diff using `git diff main...HEAD` from the issue repository when `main` is the default branch. Compare the diff against the PR title and description.

**What good looks like**

Every material change in the diff is within the plan's intended boundary or supported by a documented, justified deviation. Planned behavior is implemented or any shortfall is accurately disclosed and its impact explained. A description that claims functionality the diff does not deliver, or conceals material additional changes, is evidence of silent drift.

## Test evidence (harness category: not-tested)

**Where it lives**

- **Eval mode:** Compare the plan-context block's test plan and the reproduction steps with the candidate PR's test-evidence section, reported commands and outcomes, regression tests in the diff, and applicable repository checks in repo-facts.
- **Live mode:** Read the verification section of `beat-1-sandbox/unit-3/plan.md`, the actual test output from the issue repository, relevant test changes in the branch diff, and repository testing requirements in `CONTRIBUTING.md` or other stated project instructions.

**What good looks like**

Evidence identifies the behavior tested, the command or reproduction used, and the observed outcome. Relevant regression behavior is demonstrated, and applicable repository checks are reported accurately. A general statement such as "tests pass" without observable results is insufficient. A disclosed test limitation can be acceptable when the remaining evidence adequately verifies the change.

## Diff quality (harness category: unreviewable)

**Where it lives**

- **Eval mode:** Inspect the candidate PR's unified diff, changed-file list, and commit list. Compare the changed files and hunks against the issue and plan-context scope.
- **Live mode:** Inspect the GitHub PR's Files changed and Commits tabs, or use `git diff main...HEAD` and `git log main..HEAD` in the issue repository when `main` is the default branch.

**What good looks like**

The relevant fix and supporting tests are identifiable in the diff. Changed files serve the issue or a justified supporting purpose. Unrelated refactors, debug leftovers, generated debris, dead code, and excessive formatting changes do not obscure the implementation. Multiple commits are acceptable when the resulting change remains reviewable.

## Standards and comms (harness category: standards-wall)

**Where it lives**

- **Eval mode:** Read the repo-facts block for PR-template requirements, contributing instructions, stated policies, AI-use disclosure requirements, and explicit maintainer directions. Compare these with the candidate PR title, description, and issue discussion included in the bundle.
- **Live mode:** Read the scoped repository's `.github/PULL_REQUEST_TEMPLATE.md` or other applicable PR templates, `CONTRIBUTING.md`, stated repository policies, and relevant maintainer comments on the issue. Compare those requirements with the actual GitHub PR title and description. Also check `voice-guide.md` for personal communication rules.

**What good looks like**

The PR satisfies applicable repository requirements with meaningful information rather than empty template text. Required disclosures, including AI-use disclosure when the repository asks for it, are present and accurate. Explicit maintainer directions are addressed or their limitations are explained. Personal voice-guide violations are reported separately unless they also violate a rubric check.

A repository requirement must be grounded in the supplied repo-facts block or actual live repository evidence; do not invent standards that were never stated.