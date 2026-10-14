
---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

<!-- State, in your words, the one question this tool answers and what
a PR package is: what artifacts it contains and what they are read
against. CONTRACT.md fixes the question; your frame has to say it so
the tool cannot wander into grading something else. -->

Decide whether exactly one pull request package is ready to submit.

A PR package contains a title, description, commits, diff, and test
evidence. Judge these against the accepted plan, its issue, and the
repository's stated requirements. Apply the written rubric rather
than personal impressions or general code-quality preferences.

## Inputs and modes

<!-- Define both modes. Live mode: name every input (your plan.md with
its deviation notes, your branch's diff, your draft PR title and
description, your test evidence, your issue), where each comes from,
and what a house-chain student reads instead. The branch's diff is
everything the branch changes relative to the repo's default branch:
`git diff main...HEAD` (three dots), run from the working copy, is
the command that produces it; name the source that concretely. Eval
mode: state that the bundle is the whole world, nothing is fetched,
and every check runs with the full verdict rule. -->

**Live mode:** Read the following from the student's Path Review
working copy and issue:

- `plan.md`, including its `## Deviations` section.
- The committed branch diff from `git diff main...HEAD` and its
  commits from `git log main..HEAD --oneline`.
- The draft PR title and description from `pr_draft.md`.
- Captured test commands and results from `test_evidence.md`.
- The issue URL, issue body, and relevant discussion thread.
- `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`.

For a house-chain submission, use the supplied house issue, plan,
reproduction pack, and working branch in the corresponding roles.
Apply the same checks.

**Eval mode:** Read only the supplied frozen package bundle: repo
facts, issue, thread highlights, plan context, candidate title,
description, commits, diff, and test evidence. Treat the bundle as
the complete evidence set. Do not fetch live pages, run commands,
or consult outside files. Execute every rubric check and the full
verdict rule for the one package.

## The scope seam (live mode only)

<!-- Tell the tool when to read scope.md, what to do with the rules it
finds there, what to refuse, and what to do when the scope's repo line
is an unfilled placeholder. State that eval mode ignores scope.md
entirely. CONTRACT.md names the required behavior; your frame has to
instruct it. -->

In live mode, read `scope.md` before grading anything else. Apply
its `Repo:` boundary and Path Review house rules. Refuse to grade
a PR targeting another repository. If `Repo:` is still a placeholder,
stop without grading and tell the student to fill it with the
section's Path Review repository. Do not guess the repository.

In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

<!-- Tell the tool when to read voice-guide.md, which outgoing text it
gates (the PR title and description), how to report a broken rule, and
why it never changes the verdict on its own. State that eval mode
ignores it entirely. -->

In live mode, read `voice-guide.md` and compare the proposed PR
title and description with its rules. Identify specific violations
and suggest precise corrections in the readable summary.

Voice violations alone do not affect accept/reject unless an
explicit rubric check also covers the violation.

In eval mode, ignore `voice-guide.md` entirely.

## Component reads

<!-- Tell the tool how the pieces connect: rubric.md defines the
checks and the verdict rule, references/evidence-guide.md maps where
each evidence family lives, procedure.md is executed as written. Say
what the tool does when the procedure is silent on a step (report the
gap, never improvise around it) and what it does when rubric.md or
procedure.md has no content (the refusal rule, stated as an
instruction). -->

Read `rubric.md` for the named checks, pass conditions, weights,
and verdict rule. Read `references/evidence-guide.md` to locate
the evidence for each check. Execute `procedure.md` in order.

If `rubric.md` or `procedure.md` has no operative instructions,
refuse to grade and identify the missing component. Template
comments alone do not count as instructions.

If the procedure does not specify how to perform a necessary step,
report the gap rather than inventing a new grading method.

## Verdict and output

<!-- State the binary verdict space (accept means submit, reject means
hold) and instruct the tool to end its reply with the fenced JSON
block below, valid and last, with nothing after it. The schema is
CONTRACT.md's, verbatim; do not edit it. -->

Use only `accept` (ready to submit) or `reject` (hold).
Provide a readable per-check summary with specific evidence before
the JSON. End with the following valid fenced JSON block, including
every rubric check in order, and put nothing after it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

<!-- Write the standing rules the tool grades under: evidence first,
grade the thing not the polish, the rubric decides, the procedure
decides how, and how unclear grades are treated when the rubric's
verdict rule is silent. CONTRACT.md states each as a guarantee; your
frame has to make them instructions. -->

- Ground every grade in a concrete fact, quote, diff hunk, or
  observable command result. Do not invent evidence.
- Judge the PR's actual behavior and stated obligations, not its
  writing style, length, or number of commits.
- Follow the rubric's pass conditions and verdict rule exactly.
  Do not change a grade based on intuition.
- Follow the procedure as written. Report gaps rather than silently
  improvising missing steps.
- Distinguish honest limitations from unsupported claims of success.
- Grade genuinely missing or ambiguous evidence `unclear`; when the
  rubric is silent, treat an unverifiable required claim as failing.
