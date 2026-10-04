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

Aryankn29

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60#issuecomment-5977303060

I reproduced the `text: None` crash and traced it to the context concatenation in `FaithfulnessChecker.check()`. My plan is to normalize a context chunk whose `text` value is `None` to empty text before the chunks are joined, keeping the change local to `rag/evaluator/faithfulness_checker.py`. I'll use the existing issue-#60 coverage in `tests/unit/test_faithfulness_checker.py` as the focused regression check, then run the full faithfulness-checker unit test file and re-run the original reproduction. I don't plan to change the scoring algorithm or refactor unrelated retrieval/evaluator behavior.

---

## Your branch

**Branch**

`fix/60-none-context-text`

**Evidence**

Before the fix, I reproduced the issue on Windows 11 with Python 3.12.5 at commit `2f4e82f52efbcfcc57d65b3fa5348672163ca088`.

Command:

```bash
PYTHONUTF8=1 python - <<'PY'
from rag.evaluator.faithfulness_checker import FaithfulnessChecker

print("Input:", [{"text": None}])
print("Calling FaithfulnessChecker.check()...")

FaithfulnessChecker().check(
    "Knows Python.",
    [{"text": None}],
)
PY
```

Output before the fix:

```text
Input: [{'text': None}]
Calling FaithfulnessChecker.check()...
Traceback (most recent call last):
  File "<stdin>", line 6, in <module>
  File "C:\Users\k_raj\OneDrive\Desktop\NewProjectsLaptop\A301\pathreview-ai301-fa26-s3\rag\evaluator\faithfulness_checker.py", line 38, in check
    context_text = " ".join([chunk.get("text", "") for chunk in context_chunks])
                   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
TypeError: sequence item 0: expected str instance, NoneType found
```

After the fix, I re-ran the same bug-triggering input against the changed implementation:

```bash
PYTHONUTF8=1 python -c "from rag.evaluator.faithfulness_checker import FaithfulnessChecker; print(FaithfulnessChecker().check('Knows Python.', [{'text': None}]))"
```

Output after the fix:

```text
2026-10-03 23:20:13 [info     ] faithfulness_checked           claims_count=1 score=0.0 supported_count=0
0.0
```

The reproduction now completes normally instead of raising `TypeError`.

I also ran the focused faithfulness-checker unit tests:

```bash
PYTHONUTF8=1 python -m pytest tests/unit/test_faithfulness_checker.py -q
```

Output:

```text
..x...x......x........                                                   [100%]
19 passed, 3 xfailed in 0.34s
```

The three remaining xfails are unrelated to issue #60. The strict xfail marker for `test_none_context_chunk_text` was removed, and that regression test now runs normally.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

I completed one scored full eval run:

```text
categories: clear-accept 5/7  scope-creep 4/4  thread-convention 2/2  unbuildable 3/3  wrong-cause 4/4
agreement: 18/20 scored items  (bar: 18/20: PASS)
```

That is the final run recorded in `eval-run.txt`.

**Package analysis**

I analyzed `pkg-09`.

The gold label was:

```text
accept
```

My rubric produced:

```text
reject
```

The eval reported:

```text
pkg-09  clear-accept  accept  reject   NO     failed: Test_plan
```

The package proposed a Windows-gated fixture test for the reproduced `--glob --full-path` bug and described the expected results for the three glob patterns, the regex-mode control, and the Linux control.

My rubric read the package as failing `Test_plan`. The plan described the intended fixture behavior and named `tests/tests.rs`, but it did not give a concrete test invocation or explicitly frame the regression check as a before-fails/after-passes check. My `Test_plan` condition deliberately requires the plan to connect the original trigger to an observable post-fix result and a regression check that distinguishes the broken behavior from the fixed behavior. Under that wording, the grader treated the package as not explicit enough even though the gold label considered the plan ready.

**Check rationale**

The `Test_plan` check in my final `rubric.md` reads exactly:

> `| Test_plan | The plan's test plan read against the repro evidence's trigger, steps, observed failure, and expected behavior. | Pass if the plan exercises the same bug-triggering condition through the real code, names an observable expected result after the fix, and includes a regression check that distinguishes the broken behavior from the fixed behavior. | required |`

I wrote the check this way because a plan saying only "run the tests" does not prove that the reported bug will actually be exercised. I wanted the test plan tied directly to the reproduction: use the same trigger, state what observable behavior should change after the implementation, and include regression coverage that can distinguish the broken state from the fixed state.

This carries forward the same idea I used in Unit 2 when separating whether the correct input was exercised from whether the observed output actually matched the target behavior, but adapts it for a forward-looking implementation plan.

**Trade-offs**

The `Test_plan` check is intentionally strict, and `pkg-09` shows the trade-off.

`pkg-09` was a gold-label accept, but my rubric rejected it only on `Test_plan`. Its plan gave a reasonable Windows fixture, expected outputs, and control cases, but my rule demanded a more explicit connection between the reproduction and a regression check that distinguishes the broken and fixed states.

I accept that this stricter wording can reject some otherwise reasonable plans like `pkg-09`. The benefit is that plans which pass the check should leave less ambiguity about how the contributor will prove that the actual reported bug was fixed rather than merely running a nearby test suite.

The final full eval still reached:

```text
agreement: 18/20 scored items  (bar: 18/20: PASS)
```

and every category had at least one match.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.