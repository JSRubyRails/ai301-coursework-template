# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis supported | The plan's stated cause compared with the issue description and reproduction evidence, including observed errors, logs, commands, and relevant code paths. | Pass if the proposed diagnosis is consistent with the reproduced behavior and provides a plausible explanation grounded in the available evidence. A hypothesis may pass when it is explicitly testable during implementation. Fail if the diagnosis contradicts the evidence or presents an unsupported explanation as established fact. | required |
| Scope bounded | The plan's scope statement, proposed file changes, and intended behavior compared with the issue's requested outcome. | Pass if the proposed changes address one clearly defined issue without introducing unrelated functionality or unnecessary refactoring. | required |
| Root cause addressed | The proposed implementation steps compared with the failure mechanism identified in the reproduction evidence. | Pass if the proposed change targets a plausible failure mechanism supported by the reproduction evidence, with a way to verify the mechanism during implementation when it is not yet proven. Fail if the change merely suppresses symptoms or leaves the reported failure mechanism unaddressed. | required |
| Implementation actionable | The plan's implementation steps, target files, relevant repository structure, and prerequisites recorded in the repo-facts block. | Pass if another contributor could begin the change using the identified components, implementation approach, and available repository context. Exact function names are not mandatory when the plan provides a concrete method for locating them. Fail if a critical target, prerequisite, or implementation action must be guessed. | required |
| Tests demonstrate outcome | The plan's proposed tests compared with the original reproduction steps, observed failure, and expected behavior. | Pass if the proposed checks would demonstrate whether the original failure is resolved and provide meaningful evidence that relevant existing behavior remains intact. Tests that cannot distinguish success from failure do not pass. | required |
| Uncertainty acknowledged | The plan's assumptions, unresolved questions, and confidence statements compared with the issue discussion and reproduction evidence. | Pass if material uncertainties are identified or handled through concrete verification steps, risk mitigations, or clearly stated limitations. Do not require an explicit unknowns section or speculative uncertainty when the evidence already supports the plan. Fail if a consequential unverified assumption is presented as certain without a way to check it. | required |
| Thread and repository conventions | The proposed plan comment compared with the issue thread highlights and the contribution conventions in the repo-facts block and `references/evidence-guide.md`. | Pass if the proposed comment respects applicable maintainer guidance, existing work, and repository contribution requirements. Read the repo-facts block carefully to determine whether AI-use disclosure applies to issue comments, pull requests, or all contributions. If the repository explicitly requires disclosure for AI-assisted comments, the comment must disclose the tool and extent of assistance; if disclosure is only required for pull requests, do not impose that requirement on an issue comment. Fail if the comment contradicts maintainer decisions, ignores consequential existing work, or omits a disclosure required by the repository's stated policy. | required |

## Verdict rule

Accept if every required check passes. Preferred checks, if present, never change the verdict. Unclear counts as fail. Reject if any required check fails or is unclear.
