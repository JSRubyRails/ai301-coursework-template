# Toolkit Portfolio

Path: `beat-3-portfolio/toolkit-portfolio.md`

This file is Assignment 6, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. It has been waiting here since you created the repo in unit 1;
unit 9 is when you write it.

**Only this page is read.** Your `tools/` folders and your installed skill folders are never
opened, so every piece of evidence you want seen has to live inline here: an output excerpt,
a before/after pair, a dated commit reference.

**Write every sentence yourself.** AI may gather diffs, dates and excerpts for you; it does
not draft entries.

**Keep every section header below under its exact name** — Featured Tools, Inventory, The
Arc, and Limitations and What's Next. Feature three or four tools, each in the entry shape
shown below; give every other tool one inventory line.

**Some lines below are labelled, and the label is how they are read.** Three places on this
page use a `Label: your words` shape — the arc's beats, the tool-limits list, and nothing
else. Keep those labels exactly as written, one per line, and never delete a labelled line:
where you have nothing to put after a label, write `none` and move on. A deleted label reads
as a deleted answer.

**Before you finish**, replace every `[bracketed prompt]` with your own words, then delete
the unused `[Tool name]` entry stub, its copy-me sentence, and the prompt sentences under
each header. A leftover bracketed prompt reads as unfilled.

**Student:** Elias Zegeye

## Featured Tools

- I chose these four tools because they show different parts of the work involved in making a contribution to ITK: finding a suitable issue, checking whether a reproduction report is reliable, reviewing the wording of outgoing posts, and verifying that the branch is ready to ship. Each tool was tested against real work connected to ITK issue #6354 and PR #7191, although the tools did not all operate in the same way. The dated evidence also shows that a passing check is not the same as proof that a contribution is correct. In particular, issue-scout and repro-check exposed problems in their own judgments, the voice guard only covered posts sent through one route, and the ship manifest could verify build and test results without checking whether the code changes fulfilled the issue.

**issue-scout**

**What it is, and the judgment hole I wrote:** 

- issue-scout is a skill for finding and evaluating contribution issues. It can search for issues or take an issue URL supplied directly, then rank and grade candidates against five required checks: Maintainer activity, Repository in use, scope-feasible, Issue availability, and Contribution policy. I wrote the supporting search-strategy.md, rubric.md, scope.md, and fit profile to make those judgments more consistent. The judgment problem I was trying to address was how to distinguish an issue that is genuinely feasible for a contributor from one that only looks promising based on its title or a few search terms.

**How it evolved, dated:** 

- The first version was installed on 2026-09-28 as issue-select during unit 1 and scored 18/20 on its evaluation. On 2026-09-29, I corrected scope.md in commit 34f40e4 (fixed scope.md). During a live scan of the Path Review repository on 2026-11-07, I recorded several problems in scan-notes.md: the text query python matched 17 of 71 open issues, while the label queries matched zero; four of the five highest-ranked issues failed the availability check because a classmate already had an open PR; and scope.md still described Path Review only. On 2026-11-07 and 2026-11-08, I updated search-strategy.md, SKILL.md, and rubric.md. The scope-feasible rule was changed so that an open design edge raises the difficulty note instead of automatically making an issue fail. On 2026-11-08, I graded five candidate issues. The scout accepted CTSM #1390 but rejected four others, including ITK #6354.

**Evidence:**

The following is the scope-feasible row in rubric.md after the 2026-11-08 patch:
- "It fails only when there is no single piece of work in it: a codebase-wide checklist, an 'improve X everywhere', or a container issue tracking many sub-tasks. An open design edge, an 'etc.', or several files involved never fails this check; that raises the difficulty note instead."

The scout's verdict on the issue I later worked on, from the 2026-11-08 scan, was:
```json
{"name": "scope-feasible", "grade": "fail", "evidence": "Title 'Improve tests.'; body 'The existing tests should be improved' with four convention bullets and no module or file named"}
A friction note from scan-notes.md, dated 2026-11-07, reads:
"scope.md still says Path Review only. The direct-URL input form in SKILL.md accepts 'any issue the student already has in hand', but scope.md ... was written for unit 1 and never widened."
```

This rejection was a useful example of the difference between the information in an issue body and the full history of an issue. ITK #6354 had been transferred from the archived ITKMinimalPathExtraction repository, whose name identified the module involved. issue-scout only read the issue body when judging scope, so it did not use that transfer context. I checked the issue history manually, claimed the issue, and continued with the contribution. The maintainer assigned me, and PR #7191 was approved on 2026-11-18.

**repro-check**

**What it is, and the judgment hole I wrote:** 

- repro-check grades a claim comment and reproduction report against five checks: Environment recorded, Steps followable, Behavior matches issue, Outcome honest, and Repository conventions. It then runs a voice-guide pass. I wrote its rubric.md, scope.md, and voice-guide.md. Its purpose is to catch gaps between what a report claims and what another contributor could actually reproduce by following the documented environment and commands.

**How it evolved, dated:** 

- I built repro-check during unit 2, from 2026-10-03 to 2026-10-05. Its rubric was last edited on 2026-10-05, and it scored 19/20 on its evaluation. On 2026-11-08, I added voice-guide.md and widened scope.md for live use. On 2026-11-09, I graded the ITK claim draft and then graded the reproduction report twice. The first report grade failed the Steps followable check. After I added the module-enable flag and corrected the environment information, the regrade passed the checks. On 2026-11-11, the final grade was "accept", and I posted the report on the issue. I did not change the skill after this ITK run, even though the run showed that its rubric assumes the issue describes a failing behavior.

**Evidence:**

The first grade of my real reproduction report, dated 2026-11-09, said:
- "Steps followable: fail. The module is marked EXCLUDE_FROM_DEFAULT in its itk-module.cmake, and the configure-release task the report cites does not enable it. A stranger following the report gets an unknown build target and zero tests under the label."

I regraded the report the same day after adding -DModule_MinimalPathExtraction:BOOL=ON. The regrade said:
- "Steps followable: pass. The configure command now passes the module-enable flag and the report explains why it is required."

It also identified an environment detail that needed correction:
- "One inaccuracy to fix before posting: the table says CMake 4.4.5, but the cache shows the build was configured by the Pixi cxx-environment CMake, version 4.1.2."

The posted report is available in https://github.com/InsightSoftwareConsortium/ITK/issues/6354#issuecomment-6813398282.

This catch made the report more useful to someone who did not already know how the module was configured. Without the module-enable flag, a reader would have encountered an unknown build target and no tests under the label. The CMake correction also made the recorded environment match the build cache instead of leaving an inaccurate version in the report.

**voice guard**

**What it is, and the judgment hole I wrote:** 

- The voice guard is a Claude Code PreToolUse hook on Bash. Its check_voice.py script checks an outgoing gh post against the voice guide before the command is sent. I wrote the voice-guide.md used by the guard and shared that guide with repro-check, plan-check, and pr-precheck. The judgment problem it addresses is whether a post written with assistance still follows the expected voice and wording guidelines before it is published under my name.

**How it evolved, dated:** 

- I built and installed the voice guard on 2026-11-08, consolidating the voice guide and linking it into the three check skills. At 20:13 on 2026-11-08, the hook stopped gh issue comment --help because the command had no readable body. At 00:48 on 2026-11-09, it passed the ITK claim comment sent with --body-file. The reproduction report, PR description, issue comment, and review replies from 2026-11-11 and 2026-11-18 have no corresponding guard log entries. The PR and replies were posted in the browser, so those posts did not pass through the Bash hook.

**Evidence:**

The complete `guard-log.md` excerpt contains two entries:

```text
- 2026-11-08 20:13 [hook] stop: no body the guard can read (interactive and --help forms are stopped on purpose) | target: gh issue comment --help
- 2026-11-09 00:48 [hook] pass | target: gh issue comment https://github.com/InsightSoftwareConsortium/ITK/issues/6354 --body-file
```

The comment that passed: https://github.com/InsightSoftwareConsortium/ITK/issues/6354#issuecomment-6733254925. The maintainer replied the same day: "Tackling all the recommendations together is preferred."

The two log lines show both sides of the guard's behavior: it stopped a command when it could not inspect the post body, and it allowed a readable comment to proceed. They also show the narrow scope of the protection. The guard did not monitor every contribution-related message; it only saw posts sent through gh from Claude Code. Posts made in the browser bypassed it.

**ship manifest**

**What it is, and the judgment hole I wrote:** 

- The ship manifest is a checklist in ship-manifest.md in the ITK clone. It lists the checks that must pass before a ship, along with the command and source for each check. The ship-gate hook was installed on 2026-10-28 and is intended to run the manifest, along with pr-precheck, before Claude Code opens a PR. I wrote the manifest's four required rows and its empty exclusions table. The judgment problem it addresses is whether the branch has passed the build, focused tests, full module tests, and repository pre-commit checks before it is treated as ready.

**How it evolved, dated:** 

- I installed the ship-gate hook on 2026-10-28. On 2026-11-12, I wrote the manifest for the ITK branch with four must-pass checks and no exclusions. On 2026-11-18, all four checks were green on the first-pass commit b708f2c51. They were green again after the rework on 4a80e85a3, and on each of the two review-round commits. However, the first-pass commit had a significant implementation gap: testStatus existed in name only and stored a return value without implementing the required failure handling. The manifest itself was not edited after 2026-11-12. The PR was opened in the browser on 2026-11-18, so the ship-gate hook did not fire when PR #7191 was opened.

**Evidence:**

The manifest's must-pass table:

| Check | Command |
|---|---|
| Build MinimalPathExtraction test driver | `pixi run -e cxx cmake --build build-release --target MinimalPathExtractionTestDriver -j4` |
| Run focused GradientDescent tests | `pixi run -e cxx ctest --test-dir build-release -L MinimalPathExtraction -R GradientDescent --output-on-failure` |
| Run full MinimalPathExtraction test suite | `pixi run -e cxx ctest --test-dir build-release -L MinimalPathExtraction --output-on-failure` |
| Run repository pre-commit hooks | `pixi run -e pre-commit pre-commit-run` |

Results on 2026-11-18: focused 10 of 10, full label 20 of 20, hooks passing, on a commit where `testStatus` only stored a return value. The review of that commit said:

- "The `testStatus` claim is weaker than the instructions say... the shared functions still return early on the first failure. A reviewer may well say item 3 is not addressed."

The green checks established that the branch built and the selected tests passed, but they did not establish that the code changes satisfied the issue's four requested behaviors. I had to compare the diff with the issue by hand, identify the incomplete implementation, and rework the four shared test functions before pushing again. The manifest was useful for build and test verification, but it was not a substitute for reviewing the actual change against the issue.

## Inventory

- plan-check: A planning-review skill built on 2026-10-08 and 2026-10-09. It scored 20/20 on its evaluation, but it was not run on the ITK contribution.
- pr-precheck: A pre-PR review skill built on 2026-10-19 and scoring 19/20 on its evaluation. Its scope.md was updated on 2026-11-11, but it was not run on PR #7191.
- CLAUDE.local.md project memory: Project notes written on 2026-11-08 for the MinimalPathExtraction tests. The file was kept out of commits using .git/info/exclude, but its scope section was already out of date by 2026-11-09.
- PR monitor: On 2026-11-18, Claude Code used gh to read the reviews and inline comments on PR #7191 and draft a response. I pushed the changes and posted the replies myself.

## The Arc

**Beat 1**

Date: 2026-09-28 to 2026-09-29

Friction: The first issue-selection version had a scope-file problem. The scope guidance did not accurately cover the issues I needed to evaluate, which made the tool's feasibility judgment too narrow.

Change: I corrected scope.md on 2026-09-29. The fix was recorded in commit 34f40e4, titled fixed scope.md.

Result: The scope-file correction became part of the issue-selection tool's early development. The later issue-scout work continued to expose scope problems, leading to another round of changes in November.


**Beat 2**

Date: 2026-11-07 to 2026-11-08

Friction: Live scans rejected most of the candidate issues. scope.md still limited the scout to Path Review, and the search strategy was not finding useful candidates consistently: the python text query matched 17 of 71 open issues, while the label queries matched zero.

Change: I widened the scope, revised the search strategy, and patched the scope-feasible rule so an open design edge would raise the difficulty note instead of automatically rejecting an issue.

Result: On 2026-11-08, the scout accepted CTSM #1390 but still rejected ITK #6354 on scope. I checked the issue history manually, found the archived-repository transfer context, and claimed #6354 despite the scout's rejection.


**Beat 3**

Date: 2026-11-08 to 2026-11-09

Friction: There was no check on a post before it went out under my name through the Claude Code workflow. The first guard test was gh issue comment --help, which had no readable body for the guard to inspect.

Change: I built the voice guard hook and consolidated the shared voice guide. The hook stops posts when it cannot read a body to check.

Result: The claim comment passed the guard at 00:48 on 2026-11-09. The maintainer, dzenanz, answered the scope question that day.


**Beat 4**

Date: 2026-11-09 to 2026-11-11

Friction: repro-check failed the reproduction report on "Steps followable" because the module-enable flag was missing. It also caught that the report listed CMake 4.4.5 even though the build cache showed CMake 4.1.2.

Change: I added -DModule_MinimalPathExtraction:BOOL=ON and explained why the module-enable flag was required. I corrected the CMake version and cited Documentation/AI/testing.md.

Result: repro-check's final grade was "accept", and I posted the report on 2026-11-11. No one upstream questioned the reproduction steps. The skill itself was not changed after this run.

**Beat 5**

Date: 2026-11-12 to 2026-11-18

Friction: All four manifest checks were green on a commit where testStatus existed in name only. The checks did not expose that the implementation still returned early on the first failure instead of meeting the requested behavior.

Change: I compared the diff with the issue's four bullets by hand and reworked the four shared test functions before pushing the corrected version.

Result: hjmjohnson approved PR #7191 on 2026-11-18 with the response, "Approving as is."

**Beat 6**


Date: 2026-11-18

Friction: The PR, issue comment, and review replies were posted in the browser. As a result, the voice guard and ship-gate did not run on those browser actions, and pr-precheck was never run on PR #7191.

Change: No tool changed during this event. The work exposed a gap between the command-line workflow the hooks monitor and the browser workflow used to open the PR and post replies.

Result: none

## Limitations and What's Next

The toolkit helped with issue selection, reproduction quality, post wording, and build/test checks, but it did not cover the full contribution workflow. Two of the check skills, plan-check and pr-precheck, were evaluated but not run on the real ITK contribution. The hooks only monitor actions sent through Claude Code, so browser-based posts and PR actions can bypass them. The ship manifest verifies that the branch builds and the selected tests pass, but no tool compares the actual diff against the issue's requested changes. The manifest also did not catch the machine-generated author email. repro-check assumes that an issue describes a failing behavior, so it has no clear path for a convention issue where nothing fails.

The next improvements should address these gaps rather than simply add more checks. I would add an issue-to-diff review that compares each requested change with the implementation and its tests. I would also add a check for commit author identity, and investigate how to apply the voice review consistently to browser-posted content as well as gh commands. repro-check needs a way to assess convention-based issues without requiring a failing behavior. Finally, plan-check and pr-precheck should be run on a future real contribution so their evaluation scores can be compared with how they perform in actual use.

**Tool limits.** 

- issue-scout: It reads only the issue body when judging scope, so it missed that ITK #6354 had been transferred from the archived ITKMinimalPathExtraction repository, whose name identified the module.

- repro-check: Its rubric assumes a failing behavior and has no path for a convention issue where nothing fails.

- voice guard: It only sees posts sent with gh from Claude Code; anything posted in the browser bypasses it.

- ship manifest: It checks that the branch builds and passes tests, not whether the diff does what the issue asks. It also did not catch the machine-generated author email.
