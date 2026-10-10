## Issue

**Repository:** codepath/pathreview-ai301-fa26-howard
**Issue:** https://github.com/codepath/pathreview-ai301-fa26-howard/issues/69

**Problem:** The output parser crashes when a model returns a valid JSON array instead of a JSON object.

The parser currently assumes that decoded JSON supports `.items()`. When the decoded value is a list, calling `.items()` raises an `AttributeError` instead of allowing the parser to handle the unexpected output gracefully.

## Diagnosis

The reported failure occurs in `rag/generator/output_parser.py`, where the parser iterates over the decoded JSON as though it were a dictionary.

A top-level JSON array is valid JSON, but it does not have the `.items()` method.

The fix should validate the decoded JSON's structure before attempting dictionary-specific operations.

## Scope

**In scope:**
- Update `rag/generator/output_parser.py` to handle a top-level JSON array without crashing.
- Preserve the existing behavior for valid JSON objects.
- Add or maintain a regression test in `tests/unit/test_output_parser.py` for the reported array input.

**Out of scope:**
- Changing the model's output format or prompts.
- Refactoring unrelated parser functionality.
- Introducing new dependencies.
- Changing the behavior of unrelated JSON-processing components.

## Implementation Steps

1. Inspect the existing JSON-decoding and fallback logic in `rag/generator/output_parser.py`.
2. Add a type check before the code that calls `.items()`.
3. For both fenced and raw JSON responses, route decoded JSON arrays through the existing _parse_plaintext_output(raw) fallback instead of attempting to process them as dictionaries. Preserve the original response text.
4. Confirm that valid JSON objects continue through the original parsing path.
5. Update the existing regression test as necessary to verify that the array input no longer raises `AttributeError`.

## Verification

**Before the fix**, reproduce the issue using:

```bash
python3 -m pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback -vv --runxfail
```

The expected pre-fix behavior is an `AttributeError` caused by calling `.items()` on a list.

**After the fix:**

1. Run the same reproduction command and verify that the regression test passes.
2. Run the parser's unit tests:

```bash
python3 -m pytest tests/unit/test_output_parser.py -vv
```

3. Verify that ordinary dictionary-based JSON output still parses correctly.
4. Review the final diff to confirm the change remains limited to the parser and relevant tests.

## Risks and Assumptions

- The parser's existing fallback path must be checked before implementation to ensure it can handle a JSON array correctly.
- The type guard must not alter behavior for valid dictionary responses.
- If the fallback path cannot safely handle the array, the implementation will need a minimal adjustment, documented below.

## Deviations

The implementation followed the posted plan. I added dictionary type checks for both fenced and raw JSON, reused the existing plaintext fallback, strengthened the original regression test, and added a fenced-array regression test. No changes to the planned scope were necessary. All 20 parser tests passed.
