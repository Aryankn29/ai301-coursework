# Rubric: is this a good first issue?



## Checks


| Check                | Evidence                                                                                   | Pass condition                                                                                                                                                                                           | Weight    |
| -------------------- | ------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| maintained           | Repo facts: last 5 human commits and maintainer replies.                                   | At least 1 human commit or merged PR within 180 days, OR a maintainer reply within 90 days.                                                                                                              | required  |
| repo-active          | Repo facts: archived status, last push, latest release.                                    | Not archived, AND at least 1 release within 365 days OR meaningful code activity within 180 days.                                                                                                        | required  |
| in_scope             | Issue body, comment thread, and linked PRs: requested change, intended outcome, design settlement, and abandoned attempts. | Pass when the issue names one coherent deliverable whose intended outcome is identifiable from the body or a settled maintainer comment. A terse bug report that states the missing or broken behavior is enough; multi-file edits and optional lower-priority follow-ons still pass when they serve that same deliverable. Listed root causes or implementation ideas for a diagnosed bug are ordinary engineering choices, not open design. Fail when any of these hold: umbrella/tracking lists or open-ended "anywhere in the codebase" campaigns; support questions; major architectural rewrites; a product/design choice required for success that remains unresolved (including required assets or specs marked TBD); prolonged design debate in the thread with no maintainer settlement; OR two or more linked closed-unmerged implementation PRs (repeated abandoned attempts signal the work is not settled for a first contribution). | required  |
| unclaimed            | Repo facts: assignees and linked PRs. Issue comments: contributor claims and unlinked PRs. | No assignee, open implementation PR, or active unresolved claim. A PR mentioned only in comments counts. A closed, unmerged PR alone does not block the issue. Follow scope.md house rules in live mode. | required  |
| contribution-allowed | Repo facts: contribution policy. In live mode: CONTRIBUTING.md and AI policy.              | No explicit ban on the course's AI-assisted workflow. Disclosure, testing, and human-review requirements are acceptable if followed.                                                                     | required  |
| easy-to-verify       | Issue body: reproduction steps, expected results, and acceptance criteria.                 | A concrete reproduction example, acceptance criterion, or practical way to test the fix exists.                                                                                                          | preferred |




## Verdict rule
Accept only if every required check passes. A failed or
unclear required check means reject. Preferred checks only
rank accepted issues. During evaluation, use only the frozen
bundle. In live mode, follow scope.md.
