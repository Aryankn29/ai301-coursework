# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

## Your identity upstream

**GitHub username**

Aryankn29

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60#issuecomment-5864493794

I'd like to investigate this issue. I'll reproduce the reported faithfulness-checker crash when a context chunk has `text: None`, trace how that value reaches the failing path, and post my reproduction results here before making changes.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60#issuecomment-5864952912

I reproduced this on Windows 11 with Python 3.12.5 at commit `2f4e82f52efbcfcc57d65b3fa5348672163ca088`.

Setup:

```bash
git clone https://github.com/Aryankn29/pathreview-ai301-fa26-s3.git
cd pathreview-ai301-fa26-s3
git checkout 2f4e82f52efbcfcc57d65b3fa5348672163ca088
python -m pip install -e .
```

Then I ran:

```bash
python -c "from rag.evaluator.faithfulness_checker import FaithfulnessChecker; FaithfulnessChecker().check('Knows Python.', [{'text': None}])"
```

Observed:

```text
TypeError: sequence item 0: expected str instance, NoneType found
```

The traceback points to `rag/evaluator/faithfulness_checker.py:38`:

```python
context_text = " ".join([chunk.get("text", "") for chunk in context_chunks])
```

Expected: a context chunk whose `text` value is `None` should be handled without crashing.

Actual: `chunk.get("text", "")` returns `None` when the key exists with a `None` value, and `" ".join(...)` raises the reported `TypeError`.

So I can reproduce issue #60 on the commit above.

---

## Eval iterations

**Run history**

The eval runs, in order, were:

```text
agreement: 1/1 scored items
```

```text
agreement: 18/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in disclosure)
```

After revising the two checks involved in the disagreements, I ran:

```text
agreement: 2/2 scored items
```

The final full run recorded in `eval-run.txt` was:

```text
agreement: 19/20 scored items  (bar: 18/20: PASS)
```

**Package analysis**

I analyzed `pkg-20`.

On the first full run, my rubric produced:

```text
pkg-20  reject  accept   NO     graded accept
```

The gold label said:

> "excellent repro on every proof check; ghostty's stated AI policy requires disclosing all AI usage and the comments do not disclose (course packages are treated as AI-assisted work); the one-item category the floor exists for"

My rubric initially accepted the package because the reproduction evidence was strong, but my `Comms` check did not make the consequence of omitting a repository-required disclosure explicit enough. The gold label rejected it because Ghostty required AI-use disclosure and the candidate comments omitted it.

**Check rationale**

The final check in `rubric.md` reads:

> `| Comms | Claim comment and repro comment compared with the issue thread, repo contribution rules, templates, and disclosure requirements. | Pass if the claim identifies the specific issue and honestly states the next investigation step, and the repro comment reports the student's own evidence while following all repo-specific posting, template, and disclosure rules. If the repository requires disclosure of AI assistance, a comment that omits that required disclosure fails. | required |`

I revised this check after `pkg-20` showed that merely referring to disclosure requirements was too ambiguous. The new wording makes omission of a repository-required AI disclosure an explicit failure.

**Trade-offs**

I also revised `Output_similarity`. The final check reads:

> `| Output_similarity | Issue description compared with the observed output, error, logs, or other result. | Pass if the observed behavior matches the issue's reported failure, or is an equivalent manifestation of the same failure. An honest cannot-reproduce also passes when the same trigger was attempted, the actual result is shown, and important environment differences are stated. A different or adjacent error presented as reproduction does not pass. | required |`

This gives up a stricter rule that only successful reproductions can pass `Output_similarity`. I accepted that trade-off because an honest cannot-reproduce can still provide useful evidence when the same trigger was attempted and the differing environment and actual result are recorded.

I re-ran the affected packages as a targeted canary:

```text
pkg-10  accept  accept   yes
pkg-20  reject  reject   yes

agreement: 2/2 scored items
```

Then I ran the full suite again:

```text
categories: clear-accept 7/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4
agreement: 19/20 scored items  (bar: 18/20: PASS)
```

---

Related paths: `eval-run.txt` in this directory; my skill's files in `tools/repro-check/`.