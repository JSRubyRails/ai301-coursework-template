# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

JSRubyRails

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/69#issuecomment-6074405493

Implementation plan for issue #69

I reproduced the JSON-array parser crash on the current main branch using:

python3 -m pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback -vv --runxfail

The test fails with AttributeError: 'list' object has no attribute 'items' at rag/generator/output_parser.py:68.

Root cause: parse_review_output() decodes JSON and passes it to _parse_json_output() without verifying that the decoded value is a dictionary. When the response contains a top-level JSON array, _parse_json_output() attempts to call .items() on a list.

Proposed fix:

Add dictionary type checks after JSON decoding for both fenced and raw JSON responses.
Route non-dictionary JSON to the existing _parse_plaintext_output(raw) fallback, preserving the original response.
Preserve the existing parsing behavior for valid JSON objects.
Strengthen the existing test_json_array_fallback regression test, remove its xfail marker after the fix, and add coverage for fenced JSON arrays.
Verification: Rerun the reproduction test with --runxfail, then run python3 -m pytest tests/unit/test_output_parser.py -vv to check for regressions.

Scope: Only rag/generator/output_parser.py and tests/unit/test_output_parser.py will be changed. No new dependencies or unrelated refactors are planned.

Risk: The existing plaintext fallback must preserve the complete original response. I'll verify this in the regression tests.

---

## Your branch

**Branch**

fix/69-json-array-parser



**Evidence**

### Before implementation

**Command:**
```bash
python3 -m pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback -vv --runxfail
```

**Output:**
```text
tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback FAILED [100%]

rag/generator/output_parser.py:68: AttributeError
AttributeError: 'list' object has no attribute 'items'

1 failed in 0.13s
```

The parser crashed because `_parse_json_output()` attempted to call `.items()` on a JSON array.

### After implementation

**Command:**
```bash
python3 -m pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback -vv --runxfail
```

**Output:**
```text
tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback PASSED [100%]

1 passed in 0.05s
```

### Additional regression testing

**Command:**
```bash
python3 -m pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback tests/unit/test_output_parser.py::TestOutputParser::test_fenced_json_array_fallback -vv
```

**Output:**
```text
tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback PASSED [ 50%]
tests/unit/test_output_parser.py::TestOutputParser::test_fenced_json_array_fallback PASSED [100%]

2 passed in 0.12s
```

### Full parser test suite

**Command:**
```bash
python3 -m pytest tests/unit/test_output_parser.py -q
```

**Output:**
```text
.................... [100%]
20 passed in 0.07s
```

All 20 parser tests passed, confirming that the JSON-array fallback works and existing parser tests continue to pass.



## Eval iterations

**Run history**

1. Initial full evaluation: **18/20 — PASS**. Both disagreements were false rejections: pkg-09 and pkg-14.
2. Targeted evaluation after revising the diagnosis, implementation, uncertainty, and communication checks: **4/5**. pkg-09 and pkg-14 were correctly accepted, but pkg-20 was incorrectly accepted.
3. Targeted evaluation after clarifying the AI-use disclosure requirements: **4/4**. pkg-04 and pkg-20 were correctly rejected; pkg-09 and pkg-14 were correctly accepted.
4. Final full evaluation: **20/20 — PASS**. All five categories passed: clear-accept 7/7, scope-creep 4/4, thread-convention 2/2, unbuildable 3/3, and wrong-cause 4/4.

**Package analysis**

I analyzed pkg-20 (ghostty-org/ghostty#11261).

The instructor's gold label was `reject`. My initial rubric correctly rejected it, but after loosening the communication check, the revised rubric incorrectly returned `accept`.

The plan proposed a bounded fix for stale pointers during page-capacity changes. However, the repository's AI policy requires disclosure of AI assistance, including the tool and extent of use, for AI-assisted issue comments. The candidate plan comment contained no such disclosure.

I revised the communication check to distinguish policies applying to pull requests from those applying to issue comments. After this correction, pkg-20 returned `reject`, matching the gold label.

**Check rationale**

| Thread and repository conventions | The proposed plan comment compared with the issue thread highlights and the contribution conventions in the repo-facts block and `references/evidence-guide.md`. | Pass if the proposed comment respects applicable maintainer guidance, existing work, and repository contribution requirements. Read the repo-facts block carefully to determine whether AI-use disclosure applies to issue comments, pull requests, or all contributions. If the repository explicitly requires disclosure for AI-assisted comments, the comment must disclose the tool and extent of assistance; if disclosure is only required for pull requests, do not impose that requirement on an issue comment. Fail if the comment contradicts maintainer decisions, ignores consequential existing work, or omits a disclosure required by the repository's stated policy. | required |

I revised this check after a targeted evaluation incorrectly accepted pkg-20, even though its repository policy explicitly required AI-use disclosure for assisted issue comments. The previous wording was too permissive about communication requirements. I clarified that the evaluator must distinguish between policies applying only to pull requests and policies applying to all AI-assisted contributions. This preserved the correct acceptance of pkg-09 while correcting pkg-20 to reject.

**Trade-offs**

Making the communication check more specific introduces additional dependence on accurately interpreting the repository's contribution policy. However, this prevents a blanket disclosure rule from incorrectly rejecting acceptable plans.

I tested this trade-off using pkg-09 and pkg-20, along with pkg-04 as a thread-convention canary. The final targeted evaluation correctly classified all three packages, and the subsequent full evaluation achieved 20/20 agreement.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
