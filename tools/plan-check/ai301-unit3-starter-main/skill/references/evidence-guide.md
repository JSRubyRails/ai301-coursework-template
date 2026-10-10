
# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

**Where it lives:**
- Eval package: The issue context, reproduction-evidence block, and candidate plan's diagnosis or proposed cause.
- Live mode: The GitHub issue description, posted reproduction comment and artifacts, relevant repository code, and the draft plan.

**What good looks like:**
The plan identifies a cause consistent with the observed failure and explains how the proposed change addresses it. A diagnosis must be supported by the available reproduction evidence or clearly identified as a hypothesis requiring verification. A diagnosis that contradicts the reproduced behavior does not pass.

## Scope

**Where it lives:**
- Eval package: The issue context, candidate plan's in-scope and out-of-scope statements, proposed file changes, and thread highlights.
- Live mode: The GitHub issue description and maintainer discussion compared with the draft plan's intended changes and boundaries.

**What good looks like:**
The plan describes one bounded change that addresses the reported issue without adding unrelated features or unnecessary refactoring. Its proposed file changes and exclusions agree with the issue's requested outcome and any maintainer-imposed restrictions.

## Executability

**Where it lives:**
- Eval package: The candidate plan's implementation approach, target files, ordered work steps, prerequisites, and the repo-facts block.
- Live mode: The draft implementation plan compared with the repository's actual files, structure, dependencies, and setup documentation.

**What good looks like:**
A contributor unfamiliar with the issue could identify where to begin, what to change, and what prerequisites are necessary without guessing a critical step. The proposed actions target the demonstrated failure mechanism rather than suppressing errors, disabling tests, or changing unrelated behavior.

## Test plan

**Where it lives:**
- Eval package: The candidate plan's test plan compared with the reproduction-evidence block, including its commands, inputs, observed output, and expected behavior.
- Live mode: The draft plan's proposed tests compared with the posted reproduction comment, existing regression tests, and relevant repository testing instructions.

**What good looks like:**
The tests can distinguish the original failure from the expected corrected behavior using observable assertions, outputs, or error conditions. The plan also identifies relevant regression checks that would detect damage to existing behavior. Merely running a command without checking its result is insufficient.

## Honesty

**Where it lives:**
- Eval package: The candidate plan's assumptions, risks, unresolved questions, stated confidence, and any recorded deviations, compared with the issue context and reproduction evidence.
- Live mode: The draft plan, posted reproduction evidence, implementation notes, and any deviations documented during the build.

**What good looks like:**
The plan distinguishes demonstrated facts from assumptions and identifies material uncertainties that could affect implementation or verification. Unknown behavior is not presented as proven, and any significant deviation during implementation is recorded with its reason and effect on testing or scope.

## Comms

**Where it lives:**
- Eval package: The proposed plan comment compared with the issue's thread highlights and the repo-facts block, including contribution instructions, templates, and AI-use disclosure requirements.
- Live mode: The draft or posted GitHub plan comment compared with the issue thread, maintainer instructions, repository contribution documentation, and applicable templates.

**What good looks like:**
The comment accurately summarizes the intended change and relevant verification steps without claiming unperformed work is complete. It respects maintainer guidance, acknowledges relevant prior discussion, and follows the repository's actual contribution requirements. If AI-use disclosure is required, it must be included; if the repository does not require disclosure, its absence is not a failure.