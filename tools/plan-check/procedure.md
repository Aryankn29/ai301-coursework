# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

1. Read the issue context and repo facts first. Record the reported behavior, expected behavior, relevant constraints, maintainer guidance, and repository conventions without looking to the candidate plan to define the problem.
2. Read the repro evidence next. Record the exact trigger, observed result, expected result, environment or code state when relevant, and any artifact that constrains the diagnosis.
3. Read the candidate plan. Separately note its diagnosis, scope and non-goals, files or areas to touch, implementation approach, test plan, risks, unknowns, and Deviations.
4. Read the candidate plan comment last. Record what it promises to change or verify and any response it makes to the issue thread.
5. Use these notes for grading so the candidate plan cannot overwrite or redefine what the issue and repro evidence actually established.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

1. For Diagnosis, compare the plan's stated cause with the issue and the repro evidence. Record the behavior the diagnosis must explain and any evidence that supports or contradicts the claimed cause.
2. For Scope, record the plan's in-scope change, stated non-goals, named files or areas, and whether each planned change is necessary for the reported issue.
3. For Executability, record the concrete implementation actions, the files or areas they apply to, their purpose, and any core decision the author has left unresolved.
4. For Test_plan, record the original repro trigger and failure beside the proposed post-fix checks, including the observable result the plan expects after the change.
5. For Honesty, record every stated risk, assumption, unknown, or deviation and compare confident claims with the evidence that is supposed to support them.
6. For Comms, compare the candidate plan comment with the full plan, issue thread or thread highlights, repo facts, contribution templates, and any disclosure requirements.
7. In eval mode, gather only from the supplied package. In live mode, use the locations defined by the evidence guide. Never invent a missing fact.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. Grade checks in this order: Diagnosis, Scope, Executability, Test_plan, Honesty, then Comms.
2. For each check, use only the evidence gathered for that check and apply the pass condition from rubric.md exactly.
3. Grade `pass` when the available evidence satisfies the pass condition.
4. Grade `fail` when the evidence shows that the pass condition is not satisfied.
5. Grade `unclear` when evidence needed to decide is genuinely missing, conflicting, or too incomplete to decide without guessing.
6. Do not fail a plan merely because it is short or lacks a particular formatting structure; grade the planned outcome and evidence, not the shape of the write-up.
7. Do not turn a clearly labeled hypothesis or unknown into a failure merely because it is unresolved; use the Honesty check to decide whether the uncertainty is represented correctly.
8. Record the specific fact or quote that decided each grade so another executor could reproduce the same judgment.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->

1. Collect the grade for every rubric check using the exact check names from rubric.md.
2. If every required check is `pass`, return `accept`.
3. If any required check is `fail`, return `reject`.
4. If any required check is `unclear`, count it as failing for verdict purposes and return `reject`.
5. Preferred checks, if any exist, may be reported but never change the verdict.
6. For each check, include one concise evidence statement naming the fact or quote that decided it.
7. Emit the final JSON in the format required by SKILL.md and ensure its verdict matches the rule above.
