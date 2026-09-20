# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

---

## Selected issue

**Issue link**

[https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60)

**Verdict output**

All evidence gathered. Here's the full live-mode grading.

---

## Repo-level facts (apply to all three issues)

- **Repo:** `codepath/pathreview-ai301-fa26-s3` — confirmed in scope per `scope.md`.
- **Archived:** false. **Created:** 2026-09-10. **Last push:** 2026-09-16T21:50:20Z (4 days before today, 2026-09-20). **Releases:** none.
- **Recent commits:** all by "Andrew Burke" (`Aburke225`, human, `author_association: COLLABORATOR`), dated 2026-08-20 through 2026-09-16 — dozens of commits, several explicitly co-authored with an AI assistant (`Co-Authored-By: Claude Opus 5`).
- **Contribution policy:** `docs/CONTRIBUTING.md` (6.6KB) — detailed workflow, branch/commit conventions, CI requirements, and a whole section on seeded-bug xfail markers. No mention of AI at all, no ban, no `AGENTS.md`/`AI_POLICY.md` found in repo root.
- **Open PRs across entire repo:** 0 (`GET /pulls?state=all` → `[]`). No PR has ever been linked to any of the three candidate issues.
- All three issues: opened by `Aburke225` (COLLABORATOR) on 2026-09-10, labeled `bug` + `good first issue` + `tier-1`, **0 comments, 0 assignees**, only `labeled` events in their timelines (no assignment/cross-reference events).

---



## Issue 1 — [#60 Faithfulness checker crashes when a context chunk has](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60) `text: None`


| Check                      | Grade | Evidence                                                                                                                                                                                                                       |
| -------------------------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| maintained                 | pass  | Human commits by Aburke225 through 2026-09-16, 4 days ago.                                                                                                                                                                     |
| repo-active                | pass  | Not archived; pushed 2026-09-16; active commit history in the last 10 days.                                                                                                                                                    |
| in_scope                   | pass  | Body pinpoints exact line/cause (`chunk.get("text", "")` doesn't cover an explicit `None`), gives a copy-pasteable repro, and names the covering test `test_none_context_chunk_text`. One bounded deliverable, no open design. |
| unclaimed                  | pass  | 0 comments, 0 assignees, no linked/mentioned PR anywhere in the repo.                                                                                                                                                          |
| contribution-allowed       | pass  | CONTRIBUTING.md has no AI restriction; maintainer's own commits are AI-co-authored.                                                                                                                                            |
| easy-to-verify (preferred) | pass  | Exact repro script in the body plus a named unit test.                                                                                                                                                                         |


**Verdict: accept** — every required check passes.

## Issue 2 — [#62 Health check references](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/62) `settings.redis_host`[, which does not exist on Settings](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/62)


| Check                      | Grade | Evidence                                                                                                                                                                                                                                                                                                                                                                                         |
| -------------------------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| maintained                 | pass  | Same repo-wide commit evidence.                                                                                                                                                                                                                                                                                                                                                                  |
| repo-active                | pass  | Same repo-wide evidence.                                                                                                                                                                                                                                                                                                                                                                         |
| in_scope                   | pass  | Root cause named precisely (`Settings` has `redis_url`, not `redis_host`/`redis_port`) and the fix direction is stated by the maintainer ("should use instead") — a settled, single-file bug fix. Corroborated independently: CONTRIBUTING.md cites this exact defect ("`api/routes/health.py` `attr-defined` is issue #62") as a live `mypy` baseline suppression to remove as part of the fix. |
| unclaimed                  | pass  | 0 comments, 0 assignees, no linked PR.                                                                                                                                                                                                                                                                                                                                                           |
| contribution-allowed       | pass  | Same as above.                                                                                                                                                                                                                                                                                                                                                                                   |
| easy-to-verify (preferred) | pass  | Concrete repro: call `GET /health` with Redis up, observe 503 + `AttributeError` for `redis_host` in the log.                                                                                                                                                                                                                                                                                    |


**Verdict: accept** — every required check passes.

## Issue 3 — [#69 Output parser crashes on a top-level JSON array fallback](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69)


| Check                      | Grade | Evidence                                                                                                                                                                                                                                                                                                                                                                                                                         |
| -------------------------- | ----- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| maintained                 | pass  | Same repo-wide commit evidence.                                                                                                                                                                                                                                                                                                                                                                                                  |
| repo-active                | pass  | Same repo-wide evidence.                                                                                                                                                                                                                                                                                                                                                                                                         |
| in_scope                   | pass  | Root cause named (`.items()` called on a list), fix direction stated ("fallback path should handle array responses" — an implementation choice for a diagnosed bug, not open design per the rubric's own clarification), covering test and manifest id (H-02) named, effort estimated at 2–4 hours. Corroborated by the 2026-08-20 commit message describing this exact seeded bug ("output parser `.items()` on a JSON array"). |
| unclaimed                  | pass  | 0 comments, 0 assignees, no linked PR.                                                                                                                                                                                                                                                                                                                                                                                           |
| contribution-allowed       | pass  | Same as above.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| easy-to-verify (preferred) | pass  | Named xfail test (`tests/unit/test_output_parser.py`) to un-xfail as the acceptance criterion; no literal repro snippet in the body (weaker than #60's), but a practical test path clearly exists.                                                                                                                                                                                                                               |


**Verdict: accept** — every required check passes.

---



## Ranked read-out (per your fit: Python/backend-comfortable, want RAG/LLM exposure)

1. **#60 (**`rag/evaluator/faithfulness_checker.py`**)** — best fit: lives in the RAG pipeline you want exposure to, and it's the most concretely verifiable of the three (a literal copy-pasteable repro plus a named test), so you can confirm the fix works in minutes before writing anything.
2. **#69 (**`rag/generator/output_parser.py`**)** — also squarely in RAG, and still easy to verify via its named xfail test, but the body describes the failure conceptually rather than with a runnable repro, and the maintainer's own 2–4 hour estimate marks it as a bit more involved than #60.
3. **#62 (**`api/routes/health.py + core/config.py`**)** — accepted with equally strong evidence (arguably the most concrete repro of the three, and independently corroborated by CONTRIBUTING.md), but it sits in the API/infra layer rather than RAG, so it fits your stated preference less well. Good backup if the top two get picked up by classmates first.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60",
    "checks": [
      {"name": "maintained", "grade": "pass", "evidence": "Human commits by Aburke225 as recently as 2026-09-16, 4 days before today."},
      {"name": "repo-active", "grade": "pass", "evidence": "Not archived; pushed_at 2026-09-16; dozens of commits in the last 10 days."},
      {"name": "in_scope", "grade": "pass", "evidence": "Body: '`.get()` returns None (the default applies only to missing keys), and the subsequent `\" \".join(...)` raises TypeError' with an exact repro script and named test test_none_context_chunk_text."},
      {"name": "unclaimed", "grade": "pass", "evidence": "comments: 0, assignees: [], no linked/mentioned PR in a repo-wide PR search (0 PRs total)."},
      {"name": "contribution-allowed", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI restriction; maintainer's own commits carry 'Co-Authored-By: Claude Opus 5'."},
      {"name": "easy-to-verify", "grade": "pass", "evidence": "Body includes a literal copy-pasteable repro snippet plus the exact failing test name."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69",
    "checks": [
      {"name": "maintained", "grade": "pass", "evidence": "Same repo-wide commit evidence (last human commit 2026-09-16)."},
      {"name": "repo-active", "grade": "pass", "evidence": "Same repo-wide evidence (not archived, active commits)."},
      {"name": "in_scope", "grade": "pass", "evidence": "Body: 'output_parser.py calls .items() on the parsed value and raises AttributeError... The fallback path should handle array responses,' with named test and manifest id H-02; corroborated by 2026-08-20 commit message describing the same seeded bug."},
      {"name": "unclaimed", "grade": "pass", "evidence": "comments: 0, assignees: [], no linked/mentioned PR in a repo-wide PR search."},
      {"name": "contribution-allowed", "grade": "pass", "evidence": "Same CONTRIBUTING.md evidence as issue #60."},
      {"name": "easy-to-verify", "grade": "pass", "evidence": "Named xfail test (tests/unit/test_output_parser.py) and a maintainer-estimated 2-4 hour effort give a practical way to test the fix, though no literal repro snippet is given."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/62",
    "checks": [
      {"name": "maintained", "grade": "pass", "evidence": "Same repo-wide commit evidence (last human commit 2026-09-16)."},
      {"name": "repo-active", "grade": "pass", "evidence": "Same repo-wide evidence (not archived, active commits)."},
      {"name": "in_scope", "grade": "pass", "evidence": "Body: 'Settings in core/config.py doesn't define either field; it carries a single redis_url, which the probe should use instead,' independently corroborated by CONTRIBUTING.md naming 'api/routes/health.py attr-defined is issue #62' as a mypy baseline suppression to remove."},
      {"name": "unclaimed", "grade": "pass", "evidence": "comments: 0, assignees: [], no linked/mentioned PR in a repo-wide PR search."},
      {"name": "contribution-allowed", "grade": "pass", "evidence": "Same CONTRIBUTING.md evidence as issue #60."},
      {"name": "easy-to-verify", "grade": "pass", "evidence": "Body gives a concrete repro: call GET /health with Redis running, observe a 503 with 'redis_health_check_failed' and an AttributeError for redis_host in the log."}
    ],
    "verdict": "accept"
  }
]
```

---



## Eval iterations

**Run history**

My initial smoke test scored `agreement: 0/1 scored items`.

My first full run scored `agreement: 16/20 scored items`. It disagreed with the gold labels on issue-01, issue-04, issue-15, and issue-19.

I revised `in_scope` to accept clearly defined tasks even when they involve multiple files or brief bug reports, while rejecting unresolved design decisions and repeated abandoned implementation attempts.

The targeted retry scored `agreement: 9/9 scored items`.

My final full run, saved in `eval-run.txt`, produced:

`agreement: 19/20 scored items  (bar: 18/20: PASS)`

Issue-04 was the only remaining disagreement. The category floor was also satisfied.

**Issue analysis**

I analyzed `issue-15`. My first rubric accepted it, but the gold label was `reject`.

The first evaluation reported:

`issue-15  reject  accept   NO     graded accept`

The issue appeared manageable because it included a sample payload. However, the comments revealed years of unresolved design discussions and two abandoned PRs.

I updated `in_scope` to account for these warning signs. My final evaluation correctly rejected issue-15:

`issue-15  reject  reject   yes`

**Check rationale**

Check: `in_scope` — required

Current pass condition:

> Pass when the issue names one coherent deliverable whose intended outcome is identifiable from the body or a settled maintainer comment. A terse bug report that states the missing or broken behavior is enough; multi-file edits and optional lower-priority follow-ons still pass when they serve that same deliverable. Listed root causes or implementation ideas for a diagnosed bug are ordinary engineering choices, not open design. Fail when any of these hold: umbrella/tracking lists or open-ended "anywhere in the codebase" campaigns; support questions; major architectural rewrites; a product/design choice required for success that remains unresolved (including required assets or specs marked TBD); prolonged design debate in the thread with no maintainer settlement; OR two or more linked closed-unmerged implementation PRs (repeated abandoned attempts signal the work is not settled for a first contribution).

I changed this check because my original wording rejected manageable tasks that involved several files or had short descriptions. The revised check focuses on whether the issue has one clear outcome and whether important design decisions are settled.

I kept it required because an issue with unresolved requirements could turn into a much larger task than expected.

**Trade-offs**

The rule about two or more closed, unmerged PRs could reject an issue that is now well-defined but had two unsuccessful attempts for unrelated reasons.

I accepted that trade-off to avoid issues with repeated abandoned attempts, like issue-15. I also retested issue-09, which had one closed PR and remained accepted:

`issue-09  accept  accept   yes`

---



## Selection rationale

**Selection rationale**

1. **Fit and time available:** I chose issue #60 because it involves Python and RAG, combining my backend experience with my interest in AI. Its reproduction steps and named unit test make it manageable within the time available.
2. **What the verdict captured and what I considered separately:** My skill correctly identified that the repository is active, the issue is unclaimed, and the bug has a clear scope and a practical test. Beyond the rubric, I preferred this issue because I want more experience working with RAG pipelines.
3. **Anticipated difficulty in claiming:** Another student may choose the same issue, although PathReview allows shared contributions. I will follow the Unit 2 claim procedure. My main technical challenge will be understanding the faithfulness checker and reproducing the bug before fixing it.

---

Related paths: `eval-run.txt` in this directory; your skill's files in `tools/issue-select/`.