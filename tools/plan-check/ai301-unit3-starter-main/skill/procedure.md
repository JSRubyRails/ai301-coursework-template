# Procedure: how this skill grades a plan package

## Read order

1. Read the issue description first. Record the reported problem, expected behavior, affected functionality, and requested scope. This establishes what the plan must address.

2. Read the reproduction evidence next. Record the environment, reproduction commands, observed behavior, error messages, relevant code paths, and any limitations. Distinguish demonstrated facts from assumptions. Reading the reproduction before the plan prevents the proposed solution from influencing how the original failure is interpreted.

3. Read the repo-facts block. Record the relevant repository structure, existing tests, dependencies, contribution conventions, and any requirements affecting implementation or communication.

4. Read the issue thread highlights. Record maintainer instructions, previously attempted solutions, scope restrictions, and unresolved questions. Distinguish maintainer decisions from contributor suggestions.

5. Read the proposed implementation plan. Record its diagnosis, intended changes, affected files, implementation steps, tests, assumptions, and stated boundaries. Compare these claims against the evidence gathered in steps 1–4.

6. Read the proposed plan comment last. Record what it promises to change, what tests it mentions, and whether its claims agree with the implementation plan, thread discussion, and repository conventions.

Do not assign grades until the available evidence has been gathered. If a package lacks a source, record it as missing rather than inventing its contents.

## Evidence gathering

For each check in `rubric.md`, gather and record the following evidence:

1. **Diagnosis supported**
   - Extract the proposed cause from the plan.
   - Compare it with the issue description and reproduction artifacts.
   - Record the observed failure and whether it supports, contradicts, or does not establish the proposed diagnosis.
   - Do not treat a proposed cause as proven merely because the plan states it.

2. **Scope bounded**
   - Extract the intended outcome, affected files, and proposed modifications from the plan.
   - Compare them with the issue's requested behavior and any maintainer scope restrictions.
   - Record unrelated changes, broad refactoring, or additional features that are not necessary to resolve the issue.

3. **Root cause addressed**
   - Identify the demonstrated failure mechanism from the reproduction evidence.
   - Identify the exact implementation action intended to correct it.
   - Record whether that action prevents the failure or merely hides it through error suppression, skipped tests, or cosmetic changes.
   - If the mechanism is not established, record that limitation rather than assuming a cause.

4. **Implementation actionable**
   - Extract the target files, implementation sequence, required dependencies, and prerequisites from the plan.
   - Compare those instructions with the repository structure and repo-facts block.
   - Record whether another contributor could begin the change without guessing a critical action or target.

5. **Tests demonstrate outcome**
   - Extract the original reproduction command, input, expected result, and observed failure.
   - Extract the proposed test commands, test cases, and success criteria from the plan.
   - Record whether the tests would distinguish a corrected implementation from the original failure.
   - Check whether the plan also protects relevant existing behavior against regression.

6. **Uncertainty acknowledged**
   - Identify assumptions and claims of certainty in the plan.
   - Compare them with the reproduction evidence, issue discussion, and repository facts.
   - Record any material unknown that could affect the implementation or its tests.
   - Determine whether the plan identifies a concrete way to investigate that unknown before relying on it.

7. **Thread and repository conventions**
   - Extract maintainer requests and relevant discussion from the issue thread highlights.
   - Extract contribution and communication requirements from the repo-facts block and `references/evidence-guide.md`.
   - Compare the proposed plan comment against these requirements.
   - Record contradictions, unsupported promises, missing required disclosures, or other violations of applicable conventions.
   - Do not impose a disclosure requirement unless the repository actually requires one.
   - Check the repo-facts block for the exact scope of any AI-use policy. If the policy applies to all AI-assisted contributions, including issue comments, verify that the proposed comment includes the required tool and extent disclosure. If the policy applies only to pull requests, do not require disclosure in the plan comment.


Use the evidence locations specified in `references/evidence-guide.md`. For evaluation packages, use the supplied package sections and artifacts. For live issues, inspect the corresponding repository files and issue discussion when available.

## Check execution

Execute the seven checks in the order listed in `rubric.md`.

For each check:

1. Use the evidence already gathered for that check. Revisit a source only if a specific fact needs clarification.

2. Apply the check's pass condition exactly as written in `rubric.md`. Judge whether the proposed work achieves the required outcome, not whether the document follows a particular format or contains a particular number of sections.

3. Assign one grade:
   - `pass`: the available evidence satisfies the check's pass condition.
   - `fail`: the available evidence demonstrates that the condition is not satisfied.
   - `unclear`: the available evidence is insufficient to determine whether the condition is satisfied.

4. Record a concise explanation citing the relevant evidence. Include the specific contradiction, missing prerequisite, untested behavior, or violated convention when applicable.

5. If evidence is absent, assign `unclear` unless the available evidence independently demonstrates a failure. Never invent missing facts or treat silence as proof of success.

6. Evaluate every check independently. A failure in one check does not automatically cause another check to fail. Use the same evidence across checks only when it directly supports each decision.

7. Do not penalize a package for an optional detail unless its absence prevents the required outcome or violates an applicable repository requirement.

8. Distinguish evidence-supported, testable hypotheses from unsupported certainty. A plan may be actionable before the exact root cause or function name is confirmed, provided it identifies a plausible mechanism and a concrete way to verify it. Do not require uncertainty to appear in a dedicated section.

9. Apply repository requirements only in their stated context. A pull-request-specific requirement does not automatically apply to an issue plan comment. Do not penalize a plan for omitting an optional disclosure or for acknowledging existing work without duplicating it.


Complete all checks even if an earlier required check fails.

## Verdict assembly

1. Collect the grades for all seven checks.

2. Apply the verdict rule from `rubric.md`:
   - `accept` only when every required check is `pass`.
   - `reject` when any required check is `fail` or `unclear`.
   - Preferred checks, if any are added later, never change the verdict.

3. For a rejected package, identify the required checks that prevented acceptance. Quote the relevant evidence and explain the specific reason each deciding check failed or remained unclear.

4. For an accepted package, identify the evidence supporting the required checks without claiming that the proposed implementation has already been completed or tested successfully.

5. Return the per-check grades, their evidence-based explanations, and the final binary verdict using the output format required by `SKILL.md`.

6. Ensure the final verdict agrees with the individual grades. Never return `accept` if any required check is `fail` or `unclear`.