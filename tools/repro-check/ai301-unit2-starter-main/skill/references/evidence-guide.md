# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

**Where it lives:** In the repro report's environment record and the repo-facts block. Also compare the recorded environment against the issue context when the issue identifies a specific version, branch, dependency, operating system, runtime, or other relevant condition.

**What good looks like:** The recorded environment identifies the conditions needed to interpret the reproduction. Versions or other issue-relevant details match the issue's target, or any meaningful difference is explicitly called out.


## Steps

**Where it lives:** In the reproduction steps of the repro report, including any commands, setup instructions, inputs, or starting-state information needed to trigger the issue.

**What good looks like:** A stranger using the recorded environment can follow the steps from the stated starting state to the reported outcome without guessing about a missing prerequisite or action that could change the result.


## Behavior shown

**Where it lives:** In the artifacts attached or referenced by the repro report, including output excerpts, error messages, logs, screenshots, or other observable results. Read these artifacts against the issue description and expected behavior.

**What good looks like:** The evidence demonstrates the behavior described by the issue, including the relevant error, output, or failure condition. Similar or adjacent behavior that does not establish the issue's target does not count.


## Honesty

**Where it lives:** In the claim comment and the repro report's stated outcome, checked against the reproduction steps and supporting artifacts.

**What good looks like:** The claim accurately describes what the evidence establishes. A clearly evidenced reproduction is reported as reproduced, while a clearly evidenced failure to reproduce is reported as cannot reproduce. The package does not claim that the issue was reproduced when the evidence shows a different behavior.


## Comms

**Where it lives:** In the claim comment against the issue, the reproduction report, the repo-facts block, and the repository's stated documentation, templates, contribution guidance, and AI-use disclosure requirements.

**What good looks like:** The package follows the repository's relevant contribution conventions and makes specific, evidence-supported claims. When the repository requires an AI-use disclosure, the disclosure must be present in the required place; a missing required disclosure is not acceptable. If the repository does not require a disclosure, its absence is not a problem. The comment avoids unsupported conclusions or generic boilerplate.