
# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

<!-- Where the plan states its scope, boundary, and deviation notes,
and where the diff shows what actually changed. What it means for a
diff to match the plan, for an honest deviation to re-tie a mismatch,
and what silent drift looks like in each direction (more than the
plan, or less with no note). The description's fidelity claims read
against the diff live here too: a description claiming more or less
than the diff delivers is silent drift, not a comms problem. -->

**Eval:** Compare the `Plan context` scope, excluded work, named files,
test plan, and deviations against `Candidate PR` commits, `Diff`,
title, description, and checklist.

**Live:** Compare `plan.md`, including `## Deviations`, against
`git diff main...HEAD`, branch commits, and `pr_draft.md`. Use the
issue and discussion to verify the intended change.

**Good evidence:** Every changed file and substantive behavior is
explained by the plan or an issue-related deviation. Planned omissions
are disclosed, and description claims match the diff. Extra work or
missing work concealed by a completion claim is silent drift.

## Test evidence (harness category: not-tested)

<!-- Where the PR shows its proof: the test-evidence section's
before/after against the plan's test plan and the reproduction's own
steps, and the outcome of the repo's own checks or suite. What
decisive looks like (an observable behavior named, the expected-after
stated, the checks' outcome visible) next to "tests pass". -->

**Eval:** Compare the plan's reproduction and test plan with
`Candidate PR` test evidence and the test fixtures in `Diff`.
Read `Repo facts` for prescribed checks.

**Live:** Read the issue's reproduction, `plan.md` test plan,
`test_evidence.md`, changed tests in the committed diff,
and the PR template's testing requirements.

**Good evidence:** A command and its printed result demonstrate
the relevant behavior or reported failure. The expected outcome
can be compared with the actual outcome. Required checks have
recorded results or specific, honestly explained limitations.
A `# passed` comment or prose claim alone is not test output.

## Diff quality (harness category: unreviewable)

<!-- Where the change itself lives: the unified diff and the commit
list. What a reviewable change looks like (the fix visible, nothing
unrelated riding along) and the debris tells: debug leftovers, dead
code, commented-out blocks, formatting churn, drive-by edits. -->

**Eval:** Inspect the candidate `Diff` and `Commits`, including
every changed file and substantive hunk.

**Live:** Inspect `git diff main...HEAD`, its `--stat` summary,
and `git log main..HEAD --oneline`.

**Good evidence:** A reviewer can isolate the issue-specific fix
without unrelated refactors or broad reformatting. Debug prints,
commented-out experiments, accidental files, dead code, and unrelated
edits are absent. Necessary localized supporting changes are allowed.

## Standards and comms (harness category: standards-wall)

<!-- Where the repo states its asks (the repo-facts block's PR
template sections, contributing instructions, and stated policy,
including AI-use disclosure) and where the PR honors them: the
stated sections filled with real content, the disclosure present,
explicit maintainer direction in the thread engaged. What compliant
looks like next to boilerplate or a visibly ignored ask. (Whether
the description's claims match the diff is plan fidelity, above.) -->

**Eval:** Read `Repo facts` for PR-template requirements,
contribution rules, and AI-use policy. Compare these with the
candidate description and applicable `Thread highlights`.

**Live:** Read `.github/PULL_REQUEST_TEMPLATE.md`,
`docs/CONTRIBUTING.md`, the issue thread, `pr_draft.md`, and
the Path Review house rules from `scope.md`.

**Good evidence:** Required PR sections contain meaningful answers,
relevant issue references are present, and mandatory policy or
AI-use disclosures are supplied. Specific maintainer directions
are addressed. Empty template placeholders and omitted mandatory
requirements fail. Do not invent rules absent from the repository.
