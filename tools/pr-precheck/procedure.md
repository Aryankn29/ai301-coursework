
# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides where the plan sits in the order (before the diff? before the
description?) and says why the order matters for the side-by-side
checks that come later. -->

1. Establish the mode. In live mode, validate `scope.md` and read
   `voice-guide.md`. In eval mode, use only the frozen bundle.

2. Read the issue, thread, repo requirements, and accepted plan.
   Record the intended behavior, files or areas allowed, exclusions,
   reproduction, expected result, test plan, and deviations.

3. Read the candidate commits and unified diff. Record every changed
   file and substantive change. In live mode, use `git diff
   main...HEAD` and `git log main..HEAD --oneline`.

4. Read the PR title, description, checklist, and test evidence.
   Record each claim and each captured command result.

5. Read `rubric.md` and `references/evidence-guide.md` to prepare
   the side-by-side comparisons. Keep the plan's requirements
   separate from what the PR author claims to have completed.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which file, diff,
or page per your evidence guide) to pull the fact from, and what to
record. The load-bearing gathers this week are pairings: diff files
against plan scope, claimed evidence against the plan's test plan
and the repo's checks, description claims against diff contents. A
complete procedure leaves no check whose evidence an executor would
have to hunt for. -->

1. For `Plan_fidelity`, pair every changed file and substantive hunk
   with the plan's allowed scope or an explained deviation. List
   planned work not implemented and whether it was disclosed.

2. For `Claim_accuracy`, pair each claim in the title, description,
   and checklist with a supporting diff hunk or command output.
   Record contradictions and unsupported success claims.

3. For `Test_evidence`, pair the issue reproduction and plan's
   expected outcome with the actual before/after commands and
   printed output. List each repo-required check, its result,
   and any disclosed limitation.

4. For `Test_coverage`, list the plan's named cases and controls.
   Match each to a test fixture or equivalent observed verification.
   Record missing cases, disclosures, and unsupported test claims.

5. For `Diff_quality`, inspect every changed hunk and the commits
   for unrelated work, debug output, dead code, temporary artifacts,
   and unrelated formatting changes.

6. For `Standards`, list explicit requirements from the repo-facts
   block or live PR template, contribution guide, and issue thread.
   Match each requirement to the candidate description or relevant
   artifact. Include required AI-use disclosure when applicable.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade
the same package the same way. -->

1. Grade the six checks in the exact order listed in `rubric.md`.
   Use the corresponding recorded comparisons and pass conditions.

2. Assign `pass` when the stated condition is established, `fail`
   for a demonstrated contradiction or violation, and `unclear`
   when decisive evidence is genuinely absent or ambiguous.

3. Do not replace missing command output with a prose assertion.
   Distinguish observed results from claimed results.

4. Apply the honest-outcome rule: a disclosed limitation may pass
   where the check allows it, but a false completion claim cannot.
   Do not require extra tests or policies beyond those stated.

5. Record one concrete fact, quote, file, or missing result for
   every check. Re-read only the relevant source when evidence
   remains ambiguous; in eval mode, never go outside the bundle.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check: the
check whose failure the verdict turned on. When more than one check
failed, your procedure picks which one gets quoted (first failing
required check in rubric order is a fine rule); nothing picks it for
you, so write the rule down. A complete procedure produces the same
verdict from the same grades, every time. -->

1. Apply `rubric.md` exactly: accept if every required check passes;
   otherwise reject. Treat unclear required checks as failures.
   Preferred checks never change the verdict.

2. If rejecting, lead with the first failing or unclear required
   check in rubric order. Quote its decisive evidence or identify
   the specific missing proof. Then summarize any other failures.

3. Show the per-check grades and evidence in a readable summary.
   Use the PR URL in live mode or package id in eval mode.

4. End with the contract's exact fenced JSON structure containing
   `item`, `checks`, and `verdict`, in that order. Include every
   rubric check and no text after the JSON block.
