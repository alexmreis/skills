## What it does

`to-spec-with-evidence` runs [to-spec](https://aihero.dev/skills-to-spec) and changes one thing about the document it writes: every entry under **Implementation Decisions** that was settled by something which actually ran carries the run that settled it, named in a line of its own (what ran, what came back, what it ruled out).

Decisions reached by argument are left exactly as `to-spec` writes them. The two are meant to look different on the page, because that difference is the only way a later reader can tell a decision a slice already proved from one that is still the best available reasoning.

## When to reach for it

You invoke this by typing `/to-spec-with-evidence`; the [agent](https://www.aihero.dev/ai-coding-dictionary/agent) won't reach for it on its own.

| What the thread you're collapsing contains | What to run |
| --- | --- |
| Decisions argued through in conversation | [to-spec](https://aihero.dev/skills-to-spec) |
| Decisions settled by slices that ran and merged | `/to-spec-with-evidence` |
| A [wayfinder-tracer](https://aihero.dev/skills-wayfinder-tracer) map graduating a proven chunk | `/to-spec-with-evidence`, which is the step that map graduates through |

Where nothing in the thread ran, this degrades to plain `to-spec`: there is no evidence to cite, and inventing some would be worse than the default.

## Prerequisites

Everything `to-spec` needs, since this runs it: a tracker and the triage-label vocabulary configured by [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills). The `to-spec` skill itself has to be installed alongside this one, which reads it rather than restating it.

## Evidence, not confidence

The line each proved decision carries is **evidence**: a record of an event, in the past tense. "The sandbox rejected the payload with `INVALID_ACCOUNT_ID`, so the id has to be resolved before the call" is evidence. "This is the right shape because it keeps the adapter thin" is reasoning, and belongs in the entry unchanged, without a line pretending otherwise.

That distinction is worth more later than it looks now. A spec is read by someone deciding whether they may revisit a decision. Reasoning may be re-argued cheaply, and often should be. Something a run proved may not, at least not without a run that disagrees with it.

## It's working if

- Some decisions in the spec carry an evidence line and some don't, and you recognise which is which.
- Every evidence line names a specific run, not a general belief that the approach works.
- Nothing gained an evidence line that you cannot point at a merged slice or a captured output for.
- The rest of the document is indistinguishable from what `to-spec` would have written.

## Where it fits

A drop-in variant of a chain step, in the same place `to-spec` sits:

```txt
grill-with-docs → to-spec-with-evidence → to-tickets → implement → code-review
```

Its neighbour is [to-spec](https://aihero.dev/skills-to-spec), which it runs and which stays the right call when nothing ran; upstream, [wayfinder-tracer](https://aihero.dev/skills-wayfinder-tracer) is where the evidence usually comes from, since a tracer map graduates a proven chunk through this skill and on to [to-tickets](https://aihero.dev/skills-to-tickets). When you're unsure which skill or flow fits, [ask-matt](https://aihero.dev/skills-ask-matt) routes you.
