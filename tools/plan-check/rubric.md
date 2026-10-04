# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis | The plan's stated cause read against the issue context and the repro evidence's trigger, observed behavior, and relevant artifacts. | Pass if the diagnosis explains the reproduced behavior without contradicting the evidence, and the proposed fix is aimed at the cause the evidence supports rather than only hiding the symptom. | required |
| Scope | The plan's in-scope and out-of-scope statements, files or areas to touch, and intended change read against the issue and diagnosis. | Pass if the plan describes one bounded change needed for the issue, including necessary regression-test work, without unrelated refactors or behavior changes. | required |
| Executability | The plan's files or areas to touch, implementation approach, and order of work read against the diagnosis and available repo facts. | Pass if a stranger could begin implementing the plan without having to invent a core design decision, guess what behavior should change, or determine the main files or areas on their own. | required |
| Test_plan | The plan's test plan read against the repro evidence's trigger, steps, observed failure, and expected behavior. | Pass if the plan exercises the same bug-triggering condition through the real code, names an observable expected result after the fix, and includes a regression check that distinguishes the broken behavior from the fixed behavior. | required |
| Honesty | The plan's diagnosis, risks, unknowns, assumptions, and Deviations read against the repro and other evidence available in the package. | Pass if established facts, hypotheses, and unknowns are kept distinct; unsupported assumptions are not presented as proven; and any known deviation is stated with what changed and why. | required |
| Comms | The candidate plan comment read against the candidate plan, issue thread or thread highlights, repo-facts block, and repository contribution or disclosure rules. | Pass if the comment is specific to this issue, accurately represents the planned change and verification, responds to relevant maintainer guidance, and follows repository-specific posting, template, and disclosure requirements. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept when every applicable required check passes.

A failed or unclear required check means reject.

Preferred checks, if any are added later, never change the verdict.
