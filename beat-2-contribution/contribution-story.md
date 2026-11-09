# Contribution: Improve tests

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Elias Zegeye
**GitHub Username:** JSRubyRails
**Issue:** https://github.com/InsightSoftwareConsortium/ITK/issues/6354
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 9: Built and tested an issue-scout skill for evaluating open-source issues**

I built and customized the issue-scout skill by developing a search strategy, issue-evaluation rubric, scope rules, and supporting reference files tailored to my programming experience. During testing, I found that some issues surfaced through the external issue tracker did not fit the skill's repository restrictions, while other seemingly suitable issues had competing pull requests or work that was too broad for a first contribution. I used the grading workflow to evaluate three candidate issues and distinguish the one accepted issue from the two rejected ones, reinforcing the importance of checking issue availability and scope rather than relying on labels alone.

**Unit 10: Built a voice guard and repository-specific Claude memory for the ITK contribution**

I built a voice guard that checks outgoing GitHub posts before they are sent, then tested it against a help command that lacked a readable comment body; the guard blocked that attempt rather than allowing an unverified post. I consolidated its guidance into a shared voice guide and linked it into `repro-check`, `plan-check`, and `pr-precheck`. I also created a focused `CLAUDE.local.md` for ITK's MinimalPathExtraction tests, checked it against `AGENTS.md` and `CLAUDE.md`, and added it to `.git/info/exclude` so the local memory stays out of commits. The orientation confirmed the file was readable and consistent with repository guidance; the remaining limitation is that the memory file records context, not a fix for the redundant nested exception handling in the current patch.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I used my customized issue-scout skill to evaluate five potential open-source contributions on November 8, 2026. All five issues were supplied directly rather than discovered through a search, so no ranking signals were applied. The scout accepted ESCOMP/CTSM #1390 as a straightforward contribution because all required checks passed. It rejected AcademySoftwareFoundation/MaterialX #2813 because an existing open draft PR already referenced the issue, GTNewHorizons/GT-New-Horizons-Modpack #21056 because its scope covered approximately 30 handlers across a dozen mods, and LilyFirefly/django-rusty-templates #17 because the repository prohibits LLM use on issues labeled "good first issue." Finally, it rejected InsightSoftwareConsortium/ITK #6354 because the issue did not identify a specific module or file. The scan did not assign ITK a difficulty rating.

I chose ITK #6354 despite the rejection because I wanted to investigate whether the issue's scope could be identified through additional repository research. I discovered that the issue had been transferred from the archived ITKMinimalPathExtraction repository into the current ITK repository. I then confirmed that the corresponding MinimalPathExtraction module and its test header existed in the current codebase.

This issue fits my background because I have experience with C++, software development, and computer vision projects using OpenCV. I also want to gain more experience contributing to a large open-source C++ project. I hope to learn ITK's testing conventions, understand how its test drivers and regression baselines work, and improve my ability to identify and correct weaknesses in an established codebase. My claim comment was posted here: https://github.com/InsightSoftwareConsortium/ITK/issues/6354#issuecomment-6733254925.

The scout was useful for screening issues and identifying concrete reasons to accept or reject candidates. However, its evaluation of ITK #6354 exposed a limitation: it treated the absence of a named module or file as evidence that the work was too broad without investigating the issue's repository history. Manual research revealed that the issue had been transferred from an archived repository and that its relevant module still existed. This experience showed me that an automated issue evaluator can narrow a search, but repository history and manual verification are still necessary before making a final decision.

**Toolkit**

- **Tool:** My customized issue-scout skill, including its search strategy, evaluation rubric, scope rules, and supporting reference files.
- **What it produced:** Five evaluations from directly supplied issue URLs. CTSM #1390 was accepted as straightforward. MaterialX #2813, GTNH #21056, django-rusty-templates #17, and ITK #6354 were rejected for issue availability, scope-feasibility, or contribution-policy reasons.
- **Difficulties:** The scout incorrectly rejected ITK #6354 because it could not identify a specific module or target file from the issue description. It did not recognize that the issue had been transferred from an archived repository. The scan also exposed judgment calls involving repository-specific AI policies and restrictions on AI co-author attribution.
- **What changed:** I patched the scope rules so that open design questions can influence difficulty rather than automatically causing rejection. The verdict still requires mandatory checks to pass, and unclear scope remains a rejection reason when the work cannot be identified or bounded. I manually investigated the transferred issue and verified the relevant module in the current ITK repository before claiming it.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
