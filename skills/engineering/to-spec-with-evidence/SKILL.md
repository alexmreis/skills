---
name: to-spec-with-evidence
description: "to-spec, but every implementation decision that something proved carries the run that proved it."
disable-model-invocation: true
---

Run `/to-spec`, adding one line to each entry under **Implementation Decisions**: where the decision was settled by something that ran, name the evidence, which is what ran, what came back, and what it ruled out.

Decisions reached by argument stay exactly as `to-spec` writes them. Keeping the two visibly different is the point: it tells a later reader which decisions a slice has already proved, and which are still the best available reasoning.
