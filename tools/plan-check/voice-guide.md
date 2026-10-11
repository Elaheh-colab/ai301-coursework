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
I'm a student learning open source through code contributions. I propose fixes grounded in the reproduction evidence, with clear scope and observable test plans. You can expect honest, detailed plans backed by evidence, not speculation.

## Rules I write by

### Rule: Ground diagnosis in the repro, don't speculate
My cause must point to something the reproduction evidence actually shows—a specific code location, a mechanism, an observed behavior explained by the cause.
- Wrong: "The bug is probably in the editor code somewhere"
- Right: "The repro shows the undo stack is lost when toggling editors; the bug is that editor state is not preserved during the toggle in `editors.js` lines 142–168"

### Rule: Name specific files and scope, don't be vague
Scope is bounded: which files will change, which will not. Readers should know exactly what I'm modifying.
- Wrong: "Fix the pager navigation"
- Right: "Modify `src/output.rs` to call `generate_default_bindings()` before custom bindings; not touching the syntax highlighting pipeline"

### Rule: Include observable test steps, not wishes
The test plan names what to actually do and what to watch for—steps someone could run and verify.
- Wrong: "Verify the fix works"
- Right: "Open 94k-line log, press Shift+G: should land on last line immediately (under 1 second); also verify search keys `/`, `?`, `n` work"

## Things I never post
- Speculative diagnoses without evidence ("probably in the editor code")
- Unbounded scope ("rewrite the whole module")
- Unobservable tests ("make sure it works")
- Plans written as exploration ("I'll figure it out this weekend")

