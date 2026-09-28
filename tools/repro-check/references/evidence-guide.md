# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

# Evidence guide: where proof lives in a reproduction package

## Environment

Where it lives:
- Eval mode: the repro report's environment record and the issue context.
- Live mode: the student's repro draft, issue page, and repository setup/version documentation.

What good looks like:
The report names the operating system, relevant program/runtime versions, and code state used for the attempt. If those differ in an important way from the issue's target environment, the difference is stated rather than hidden.

## Steps

Where it lives:
- Eval mode: the repro report's setup, commands/actions, inputs, and starting state.
- Live mode: the student's repro draft and any repository setup instructions it depends on.

What good looks like:
A stranger can start from the stated setup and follow the sequence to the observed result without guessing a required command, input, configuration, or setup step. Commands should be exact when commands are what produced the result.

## Behavior shown

Where it lives:
- Eval mode: the issue description compared with the repro report's output excerpts, logs, stack traces, screenshots, test results, or other artifacts.
- Live mode: the issue page compared with the evidence in the student's repro draft.

What good looks like:
The artifacts show the same failure or condition described by the issue, or an equivalent manifestation of that same bug. An unrelated or adjacent error is not evidence of reproduction. For a cannot-reproduce result, the artifacts should still show that the correct target condition was attempted and what actually happened instead.

## Honesty

Where it lives:
- The repro report's conclusion read against its steps and artifacts.
- Any statements about reproduction, root cause, success, or failure.

What good looks like:
The report says exactly what the evidence supports. A successful reproduction is only claimed when the target behavior is actually shown. A cannot-reproduce result is valid when the attempt and observed result are documented clearly. Possible causes or guesses are labeled as such rather than stated as proven.

## Comms

Where it lives:
- Eval mode: the claim comment, repro comment, issue context, repo-facts block, and stated contribution/disclosure policy.
- Live mode: the issue thread, repository contribution docs/templates, and the student's claim/repro drafts.

What good looks like:
The claim names the specific issue and says what the student will investigate next without pretending work is already complete. The repro comment presents the student's own evidence, follows repository-specific comment/template rules, and satisfies any required disclosure of AI assistance or other contribution-policy requirements.
