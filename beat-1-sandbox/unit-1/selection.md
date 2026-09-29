# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/69 

**Verdict output**

Issue 69, output parser crashes on top-level JSON array. Fit: a bounded Python fix in one file with a covering test already written and marked xfail, so the spec is concrete. It touches real code rather than config, which matches the profile's wish to learn on familiar technology. Estimated 2 to 4 hours.


```json
{
    "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/69",
    "checks": [
      {"name": "Maintainer activity", "grade": "pass", "evidence": "Last 5 default-branch commits all by human user Aburke225, newest 2026-09-16 (12 days ago); same COLLABORATOR closed issues #52 and #43 with comments on 2026-09-16."},
      {"name": "Repository in use", "grade": "pass", "evidence": "archived=false; pushed_at 2026-09-16 (12 days ago); no releases but push is within 180 days."},
      {"name": "Newcomer scope", "grade": "pass", "evidence": "One bounded fix: handle list in fallback path of rag/generator/output_parser.py and remove the xfail marker on the covering test; maintainer-authored, labeled good first issue and tier-1, estimated 2-4 hours."},
      {"name": "Issue availability", "grade": "pass", "evidence": "assignees=[]; 0 comments; timeline has only label events; none of the repo's 4 PRs reference #69."},
      {"name": "Contribution policy", "grade": "pass", "evidence": "No root CONTRIBUTING.md, AI_POLICY.md, AI_USAGE_POLICY.md, or AGENTS.md; docs/CONTRIBUTING.md and PR template contain no AI ban or AI mention."}
    ],
    "verdict": "accept"
  }

```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

- 18/20: PASS

**Issue analysis**

issue-19 — Rubric decision: reject. Gold label: accept. The rubric rejected issue-19 because it failed the Newcomer scope check. The evaluation output explicitly records “failed: Newcomer scope,” while the gold label was accept. This disagreement shows that the rubric's definition of newcomer scope was stricter than the gold standard for this case.

**Check rationale**

Newcomer scope | Issue body and comment thread | Pass if the issue asks for one bounded piece of work that a newcomer can reasonably complete. Fail if it is explicitly an umbrella/tracking issue, remains unresolved as a design debate, requires changes to core internals, is purely a usage/support question, or otherwise describes work that is not reasonably bounded for a first contribution. | required

- I made this check required because a first contribution should have a clearly defined and manageable scope. The check focuses on whether the issue describes one bounded piece of work rather than simply relying on labels such as "good first issue." This is especially useful for distinguishing a small bug fix like issue #69 from an issue that may appear beginner-friendly but actually requires a large or unclear change.

**Trade-offs**

- The trade-off is that an issue can be technically bounded but still be more difficult than expected because of unfamiliar code or hidden implementation details. This check also cannot fully measure how much I will learn from an issue or whether the technology matches my personal interests. For issue #69, the check accepted the issue because the work was clearly bounded, while I separately considered that the Python and pytest work matched my existing skills and learning goals.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. Issue #69 fits my interests because it involves Python code and pytest debugging, which are technologies I am already familiar with and want to continue improving. The estimated 2–4 hour time requirement also fits the amount of time I can reasonably dedicate to a first contribution.

2. The verdict correctly identified that issue #69 is a bounded, active issue with a clear bug, an existing test, and no one currently working on it. Beyond the rubric, I also considered how much I would actually learn from solving the issue and whether the work matched the programming skills I want to develop.

3. I expect claiming the issue to be relatively straightforward because the issue currently has no assignee or comments indicating that another student has claimed it. Since this is the course's Path Review repository, I will still follow the course's claiming process and make my claim before beginning the work.


---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
