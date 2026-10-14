# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

I am a student contributor working through a structured open-source contribution workflow. I am comfortable with Python/backend work, but I am still learning this repository and should not write as if I already know the codebase better than the maintainers.

My comments should be specific about what I am investigating, what I actually observed, and what I plan to do next.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

### Rule: Say what I know, not what I assume

Do not present a suspected cause, fix, or outcome as confirmed before I have evidence.

- Wrong: "The bug is caused by the join not handling None, so I'll fix that."
- Right: "I'll reproduce the reported `text: None` failure and trace where that value reaches the faithfulness checker."

### Rule: Promise investigation, not a fix or deadline

A claim comment should say what I will investigate next, not guarantee that I can fix it or when I will finish.

- Wrong: "I'll have a fix for this by tomorrow."
- Right: "I'd like to investigate this issue. I'll reproduce the failure first and post what I find."

### Rule: Be specific to the issue

Refer to the actual behavior, input, error, or file involved instead of posting generic claim/repro boilerplate.

- Wrong: "I can take this issue and look into it."
- Right: "I'd like to investigate the faithfulness-checker crash when a context chunk has `text: None`."

### Rule: Separate observation from interpretation

Clearly distinguish what the command/test actually showed from what I think may explain it.

- Wrong: "This proves the parser is broken because the fallback logic is wrong."
- Right: "The test reproduced the `AttributeError` on the array input. The fallback path appears to be the next place to inspect."

### Rule: Make reproduction comments useful to someone else

Include enough concrete environment, commands, inputs, and observed output that another contributor can understand what I ran without guessing.

- Wrong: "Confirmed, I get the same error."
- Right: "On Python 3.x at commit `<sha>`, running `<command>` with `<input>` produced `<error>`. I expected `<expected behavior>`."


## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

- Claims that I reproduced or fixed something before I have evidence.
- Promises about finishing by a specific time.
- Generic "I'll take this" comments with no issue-specific detail.
- "Same as above" or piggyback reproduction comments.
- Confident root-cause claims based only on a guess.
- AI-generated wording I have not reviewed and understood myself.
- Simply innapropriate content.
