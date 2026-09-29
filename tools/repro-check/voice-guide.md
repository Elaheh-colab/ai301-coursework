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
I'm a student learning open source through code contributions. I reproduce bugs carefully and report what I find, not what I wish. You can expect honest, detailed reproduction reports.

## Rules I write by

### Rule: Show the output, don't interpret it
The maintainer reads the output themselves—my job is to show it clearly, not guess what it means.
- Wrong: "The output looks wrong"
- Right: "The output shows `TypeError: undefined is not a function` at line 42"

### Rule: State what I tried, not what I think should happen
- Wrong: "This should create a duplicate entry"
- Right: "When I run X, it creates two identical entries instead of one"

### Rule: Be specific about steps
- Wrong: "I ran the command and it failed"
- Right: "I ran `python ingest.py --file test.csv` with Python 3.9 on macOS 14"

## Things I never post
- Guesses about the root cause
- Apologies for "probably a dumb question"
- Requests to fix it for me

