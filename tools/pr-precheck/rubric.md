
# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Plan_fidelity | Plan context's intended behavior, scope, exclusions, files, and deviations compared with the candidate diff and commits. | Pass if every substantive change belongs to the accepted plan or an explicitly explained, issue-related deviation, and any omitted planned work is disclosed. Reject silent additions, omissions, or unrelated work even if described as cleanup. | required |
| Claim_accuracy | Candidate title, description, and checklist read against the actual diff, test fixtures, and observable results. | Pass if material claims about implementation, added tests, unchanged behavior, and successful checks are supported or clearly qualified. Reject false completion claims and assertions of nonexistent changes or passing tests. | required |
| Test_evidence | Issue reproduction, plan's expected outcome, candidate test-evidence commands and printed output, and the repo-facts block's required checks. | Pass if the core change has observable verification and the repository's prescribed checks have reported outcomes, or specific unavailable checks are honestly disclosed with reasons. A written success claim or shell comment is not command output. Disclosure cannot replace all proof of the core fix. | required |
| Test_coverage | Plan's named regression cases and controls compared with test fixtures in the diff and the candidate test evidence. | Pass if claimed tests exist and the planned behavior is covered by relevant tests or equivalent observed verification. Explicit, justified gaps may pass when remaining evidence supports the core fix; missing cases falsely claimed as tested fail. | required |
| Diff_quality | Candidate unified diff and commits, including changed files, code hunks, and incidental artifacts. | Pass if the issue-specific change is reviewable without unrelated refactors, debug leftovers, dead code, accidental files, or broad formatting churn. Allow localized supporting changes necessary for the issue. | required |
| Standards | Repo-facts PR template, contribution policy, AI-disclosure requirements, and relevant maintainer directions compared with the candidate description and submission. | Pass if all expressly required sections, issue references, substantive disclosures, and applicable maintainer instructions are addressed. Reject missing mandatory information or untouched boilerplate. Do not invent repository rules not stated in the evidence. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept only when every required check passes.

A failed or unclear required check means reject. An unclear grade
means the available evidence cannot establish the check's condition.

Preferred checks, if added later, never change the verdict.

An honestly disclosed shortfall is not an automatic rejection.
Grade it under the stated pass condition: distinguish missing proof
of an essential result from a transparently reported limitation.
