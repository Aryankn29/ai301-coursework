# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

Where it lives:
- Eval mode: the issue context, repro-evidence block, and the candidate plan's diagnosis or explanation of the failure.
- Live mode: the GitHub issue and thread, the student's posted Unit 2 repro comment, and the diagnosis in draft plan.md.

What good looks like:
The stated cause accounts for the behavior actually demonstrated by the reproduction and does not contradict it. The planned change addresses the supported failure mechanism rather than merely suppressing an observable symptom.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

Where it lives:
- Eval mode: the candidate plan's scope, non-goals, files or areas to touch, issue context, and repro evidence.
- Live mode: the same parts of draft plan.md, checked against the issue and current repository when needed.

What good looks like:
The plan bounds itself to the change necessary to address the issue plus directly necessary regression tests. Unrelated cleanup, broad redesign, or changes without a connection to the diagnosis are outside a ready scope.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

Where it lives:
- Eval mode: the candidate plan's files or areas to touch, implementation approach, work order, and relevant repo facts.
- Live mode: draft plan.md plus the current repository files or documentation needed to understand those named areas.

What good looks like:
Another contributor can identify where to begin, what behavior is changing, and what the planned edits are meant to accomplish without asking the author to choose the core implementation strategy. Exact line numbers are not required when the file, area, and intended change are otherwise clear.

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

Where it lives:
- Eval mode: the candidate plan's test plan read directly against the repro-evidence block's trigger, commands or steps, observed result, and expected result.
- Live mode: the draft test plan read against the student's posted Unit 2 reproduction evidence.

What good looks like:
The plan exercises the original bug-triggering condition through the real code and names an observable post-fix result. It includes a regression check capable of distinguishing the broken behavior from the intended fixed behavior rather than merely saying to run tests.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

Where it lives:
- Eval mode: the candidate plan's diagnosis, risks, unknowns, assumptions, and Deviations, read against the repro evidence and other package facts.
- Live mode: those parts of plan.md and the evidence available from the issue, reproduction, and repository.

What good looks like:
Facts supported by evidence are stated as facts; hypotheses and unresolved questions remain labeled as such. A plan does not claim certainty, completion, or proof that its evidence does not provide, and any known build deviation records what changed and why.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

Where it lives:
- Eval mode: the candidate plan comment read against the candidate plan, thread highlights, repo-facts block, contribution policy, templates, and disclosure requirements.
- Live mode: the draft comment read against the live issue thread, draft plan, repository contribution docs or templates, and applicable disclosure policy.

What good looks like:
The comment is specific to the issue, accurately reflects the planned change and verification, and accounts for relevant maintainer direction instead of posting generic boilerplate. It follows repository-specific contribution and disclosure requirements and does not piggyback on another student's plan.
