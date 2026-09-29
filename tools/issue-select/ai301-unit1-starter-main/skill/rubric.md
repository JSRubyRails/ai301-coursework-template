# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer activity | Repo facts: "last 5 default-branch commits"; commit history for authors; recent issue threads showing Owner, Member, or Collaborator responses | Pass if there is at least one default-branch commit within the last 90 days authored by a human, OR there is evidence of a human Owner/Member/Collaborator responding to an issue within the last 90 days. Bot-only activity does not count as maintainer activity. | required |
| Repository in use | Repo facts: "latest release", "last push", "archived"; repository front page for stars or "Used by" count when available | Pass if the repository is not archived and there is evidence of recent activity: a push to a branch or a release within the last 180 days. | required |
| Newcomer scope | Issue body and comment thread | Pass if the issue asks for one bounded piece of work that a newcomer can reasonably complete. Fail if it is explicitly an umbrella/tracking issue, remains unresolved as a design debate, requires changes to core internals, is purely a usage/support question, or otherwise describes work that is not reasonably bounded for a first contribution. | required |
| Issue availability | Issue Assignees box; Development box for linked PRs; issue comment thread; label event history | Pass if the issue has no current assignee, no open formally linked PR, and no recent comment indicating that another contributor has claimed or is actively working on it. An old closed/unmerged PR alone does not count as a current claim. | required |
| Contribution policy | `CONTRIBUTING.md`, `.github/` contributor documentation, `AI_POLICY.md`, `AI_USAGE_POLICY.md`, `AGENTS.md`, and issue/PR templates | Pass if the repository does not explicitly ban AI-generated or AI-assisted contributions. Disclosure, testing, personal-understanding, and human-review requirements count as conditions to follow rather than bans. If the repository explicitly states that AI-generated or AI-assisted code is not accepted, fail. | required |

## Verdict rule

Accept an issue only if every required check passes. Reject the issue if any required check fails. If a check is unclear because the available evidence does not establish that its pass condition is satisfied, treat the check as failed and reject the issue.
