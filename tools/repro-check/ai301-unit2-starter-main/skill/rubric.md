# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment recorded | The repro report's environment record, including the relevant repository, branch/commit, runtime or dependency versions, and other issue-relevant setup details. | Pass if the recorded environment contains enough information to identify the conditions under which the reproduction was performed and does not omit a detail that is necessary to interpret the result. | required |
| Steps followable | The reproduction steps in the repro report, read together with any commands or setup instructions they reference. | Pass if another person could follow the stated steps in the recorded environment without having to guess a missing action or prerequisite that could change the result. | required |
| Behavior matches issue | The artifacts read against the issue's description, especially the output excerpt, error, logs, or other observed behavior that is evidence for the reproduction. | Pass if the observed behavior demonstrates the same target behavior described by the issue. An adjacent, similar, or unrelated failure does not pass. | required |
| Outcome honest | The claim comment and the repro report's stated outcome, checked against the artifacts and observed behavior. | Pass if the stated outcome is supported by the evidence. A correctly evidenced cannot-reproduce result passes; a confident claim that the wrong behavior was reproduced fails. | required |
| Repository conventions | The repo-facts block and the conventions identified in `references/evidence-guide.md`, including any AI-use disclosure requirements, checked against the claim comment and reproduction report. | Pass if the claim comment and reproduction report follow the repository's relevant contribution conventions. If the repository requires an AI-use disclosure, the required disclosure must be present; a missing required disclosure fails this check. If no disclosure is required, its absence does not fail the check. | required |

## Verdict rule

Accept if every required check passes. Preferred checks, if present, never change the verdict. Unclear counts as fail. Reject if any required check fails or is unclear.
