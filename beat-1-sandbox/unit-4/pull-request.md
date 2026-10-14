
# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

<!--
[Link to the pull request you opened. It must be the pull request's own page on the Path
Review repo, not your fork's branch page.]
-->

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/216

**Branch**

<!--
[The name of the branch the pull request comes from, exactly as it appears in your fork.
The naming shape is a type prefix, then the issue number, then a short description. **The
issue number in the branch name must be the number of the issue the pull request fixes** —
a name carrying any other number does not satisfy this field.]
-->

`fix/60-none-context-text`

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

<!--
[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]
-->

1. Initial partial run: no score (Claude authentication error).
2. Partial run: 3/3 agreement.
3. Initial full run: no score (Windows Unicode encoding error).
4. Final full run: **19/20 agreement (PASS)**, all five categories matched.

**Package analysis**

<!--
[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]
-->

Package: `pkg-02` (Textualize/rich #4208)

- Rubric verdict: `accept`
- Gold label: `accept`

The PR fixes recorded console output being cleared before a file write succeeds. The diff changes `save_text`, `save_html`, and `save_svg` to export without clearing and clear only after successful writes.

Diff evidence:
`text = self.export_text(clear=False, styles=styles)`

After-reproduction output:
`'IMPORTANT OUTPUT\n'`

Test evidence:
`pytest tests/ -q` passes (1462 passed, 12 skipped).

The diff follows the plan, includes a regression test and changelog entry, and contains no unrelated changes. The required checks therefore passed.

**Check rationale**

<!--
[Quote one check from the `rubric.md` you uploaded to `tools/pr-precheck/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]
-->

Exact check from `rubric.md`:

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Claim_accuracy | Candidate title, description, and checklist read against the actual diff, test fixtures, and observable results. | Pass if material claims about implementation, added tests, unchanged behavior, and successful checks are supported or clearly qualified. Reject false completion claims and assertions of nonexistent changes or passing tests. | required |

I chose this rule because PR descriptions can claim changes or test results that the actual diff does not support. I preferred requiring evidence for material claims over judging the description's length or polish, while allowing honestly qualified limitations.

**Trade-offs**

<!--
[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]
-->

`pkg-11` was incorrectly rejected (`gold: accept`) because `Claim_accuracy` and `Test_evidence` failed.

This shows the rubric can be overly strict about evidence presentation. I kept the checks unchanged because the final evaluation reached 19/20, correctly rejected all four not-tested packages, and matched every category.

The trade-off is potentially rejecting an acceptable PR rather than accepting unsupported success claims.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
