# Plan for issue #60

## Diagnosis

The failure happens while `FaithfulnessChecker.check()` combines the retrieved context text.

The reproduction from Unit 2 used:

```python
FaithfulnessChecker().check(
    "Knows Python.",
    [{"text": None}],
)
```

and produced:

```text
TypeError: sequence item 0: expected str instance, NoneType found
```

The failing line is:

```python
context_text = " ".join([chunk.get("text", "") for chunk in context_chunks])
```

`dict.get("text", "")` uses the default only when the key is absent. When the key exists with the value `None`, the expression returns `None`, which is then passed to `" ".join(...)` and causes the `TypeError`.

The fix should therefore normalize a present-but-`None` text value before the values reach `join()`.

## Scope

In scope:

- Handle a context chunk whose `text` value is `None` without crashing.
- Keep the existing behavior for normal string context values and missing `text` keys.
- Add or enable focused regression coverage for the `text: None` case.

Out of scope:

- Changing the faithfulness scoring algorithm.
- Changing how claims are extracted or supported.
- Refactoring unrelated retrieval or generation code.
- Broad validation changes for other chunk fields or unrelated invalid input types.

## Files to touch

- `rag/evaluator/faithfulness_checker.py`
  - Normalize a `None` context text value to an empty string before joining context chunks.

- `tests/unit/test_faithfulness_checker.py`
  - Use the existing issue-#60 regression coverage for `text: None`, removing any known-failure marker if necessary once the implementation is fixed.

## Approach

1. Change the context-text construction so a missing `text` key and a `text` key whose value is `None` both contribute an empty string instead of `None`.
2. Keep the normalization local to the context concatenation path so the change does not affect unrelated evaluator behavior.
3. Run the focused issue-#60 regression test and the existing faithfulness-checker unit tests.
4. Re-run the exact Unit 2 reproduction against the real implementation.

A minimal implementation should be sufficient, such as normalizing the retrieved value before it reaches `" ".join(...)`.

## Test plan

First re-run the exact Unit 2 trigger:

```bash
python -c "from rag.evaluator.faithfulness_checker import FaithfulnessChecker; print(FaithfulnessChecker().check('Knows Python.', [{'text': None}]))"
```

Before the fix, the observed result was:

```text
TypeError: sequence item 0: expected str instance, NoneType found
```

After the fix, I expect the call to complete without raising `TypeError` and return a valid faithfulness score.

Then run the focused/unit test file:

```bash
python -m pytest tests/unit/test_faithfulness_checker.py -q
```

The issue-#60 `text: None` regression case should pass, and existing faithfulness-checker tests should remain passing.

## Risks and unknowns

The intended change treats `None` as empty context text. That matches the current handling of a missing `text` key, but this plan does not broaden validation for arbitrary non-string values.

The focused fix should not change scoring for valid string chunks. The existing unit tests will be used to check that surrounding behavior remains intact.

## Deviations

There was no implementation deviations. The change followed the plan: `None` context text is normalized to an empty string before joining, and the issue-#60 strict xfail marker was removed so the regression test now runs normally. The original reproduction now completes with a valid score instead of raising `TypeError`, and the faithfulness-checker test file passes with 19 tests passed and 3 unrelated xfails.