---
name: wayfinder-tracer
description: "Wayfinder, but the map starts as one stupid slice that works and grows only where a merged tracer actually hits fog."
disable-model-invocation: true
---

Wayfinder charts a way made of **decision tickets**, surveyed **breadth-first** across the whole space. This charts one made of **tracers**, followed **depth-first** down a single thread: the simplest stupid thing that could possibly work, merged, and then the next one.

Two inversions. What clears fog is a slice that ran, not a conclusion that was reasoned. And what gets charted is that one slice, never the space of unknowns, however clearly you can already see it. Seeing an unknown is not the same as needing it charted, and a map you could survey up front was never foggy enough to need one.

Read the sibling `wayfinder/SKILL.md` first. Map format, ticket mechanics, frontier, HITL/AFK and the two invocation modes all come from there unchanged. This skill overrides ticket types, how much gets charted, and what goes in **Notes**, and adds a way off the map.

## The tracer ticket

A fifth `wayfinder:<type>`, alongside `research`, `prototype`, `grilling`, `task`:

- **Tracer** (HITL to settle the slice, then AFK to build it): the simplest, stupidest thing that could possibly work, end to end, against the real dependency, merged. The first one is a **walking skeleton**: a single slice touching every layer, hardcoding everything it isn't proving and skipping everything it isn't testing. Narrow and ugly is the point. It resolves by **evidence**: what ran, what came back, what that rules out.

Its body is a **question**, in wayfinder's ticket format: what the slice must reach end to end, and what evidence it must bring back. How it gets built belongs to the session that picks it up, which grills it against the code as it stands then rather than as it stood at charting.

Where `prototype` is throwaway code answering a design question, a tracer is **kept** code answering it. Reach for prototype when an artifact only has to be reacted to; reach for tracer when it has to run.

## Chart

Follow wayfinder's **Chart the map**, replacing two of its steps by name.

1. **Name the destination in a sentence**: a change, merged, exercised against the real dependency. Grill only as far as that sentence needs. The destination fixes scope; it isn't a design.
2. Instead of **Map the frontier**, **find the first tracer, depth-first.** Rather than fanning out, put one question to the effort: *what is the stupidest thing that could run end to end and teach us something?* Follow that single thread until you can state the slice in a sentence, then stop asking. That sentence is the whole ticket; the questions the next one would have answered belong to the grilling that opens it. The rest of the space gets charted by the tracers that hit it, not by this conversation.
3. **Create the map** with the destination, the doctrine in `## Notes`, and **Decisions so far and Not yet specified both empty**. `## Out of scope` may carry what the destination consciously rules out, since narrowing is not surveying.
4. Instead of **Create the tickets you can specify now**, **create one tracer ticket.** There are no blocking edges to wire, because there is nothing yet to wire it to. Wayfinder's research-subagent step then has nothing to fire, since a first tracer creates no research tickets.

**Done when** the map has exactly one open child, that child is a tracer whose body states reach and evidence and settles no design question, and Not yet specified is empty.

The cost is real: a one-ticket frontier gives concurrent sessions nothing to parallelise until the first slice merges. That is the trade, scope bought with evidence rather than foresight.

## Retrofit a charted map

Given an existing map, in one session:

1. Install the doctrine into its `## Notes`.
2. Chart the tracer that would settle the most open questions at once, and wire those questions to block on it.
3. Leave `## Not yet specified` untouched but **inert**: it is now recorded thinking, not a backlog. Nothing in it becomes a ticket until a merged tracer reaches it.
4. Closed tickets stay closed. The map records the route walked, and a decision made early is still a decision made.

**Done when** the first frontier ticket is a tracer, and every open question is either blocked on one or names why it outranks one.

## Graduate

A tracer merges and the work it leaves behind is repetition: the second and third caller, the other six endpoints, the remaining field mappings. That chunk is no longer fog, because a slice has already run through it end to end, so it leaves the map for the main flow rather than earning more tracers. In practice the trigger fires mid-grilling: when a tracer's pickup starts generating work for slices other than its own, this is what is happening.

**The gate is evidence, not agreement.** Reaching shared understanding in a grilling graduates nothing; a merged tracer through the chunk does. Every ticket that leaves must widen a path that tracer already walked; one that opens a new path is a tracer, and stays on the map.

1. **Name the chunk against the evidence**: what the merged tracer proved, and which repetitions follow from it.
2. Run **to-spec-with-evidence**, drawing its Implementation Decisions from the map's Decisions so far and the tracers' resolutions.
3. Run **to-tickets** to slice the spec, then fan the tickets out: one subagent per unblocked ticket, each in its own worktree so concurrent sessions cannot trample each other, each closing through the repo's own checks.
4. **Record one line in the map's Decisions so far** pointing at the spec, and clear whatever in Not yet specified it now covers.

**Done when** every graduated ticket repeats a path a merged tracer walked, the spec is linked from Decisions so far, and the map holds only what a slice still has to prove. The map closes when nothing does.

## The doctrine

Install verbatim into the map's `## Notes`, replacing any skills paragraph. Wayfinder loads Notes every session, so this binds every later plain `wayfinder` run, including the charting decisions made in them.

```markdown
**This map finds its way by building.** Wayfinder's "plan, don't do" default is
overridden, and so is its ticket order: the destination is merged code.

**Chart what you hit, not what you foresee.** A question earns a ticket only once
a merged tracer has actually run into it, and every question ticket names that
tracer. Foresight goes to Not yet specified and stays inert there until a slice
reaches it, however obvious it looks from here. You are not going to need it
until you need it.

**A tracer ticket is a question, not a design.** It names what the slice must
reach end to end and what evidence it must bring back. Which module it lands in,
which library it leans on, how the code is arranged: all settled by the session
that picks it up, against the code as it stands then. Charting stops at the
sentence.

**Depth-first: the frontier carries one tracer.** When it merges, chart the next
stupidest thing that could work, one thread at a time. Questions a merged tracer
surfaced may run in parallel beside it.

**A tracer blocks the questions it answers.** The interface, the schema and the
shape get read off two real callers rather than argued ahead of one. A question
may block a tracer only where a wrong answer cannot be cheaply reverted, where
the blast radius outlives the branch: money moved, data migrated, a contract
published to someone else.

**Decide at the last responsible moment.** Where a decision can wait, put a seam
where it will land and leave it undecided. Record the seam, not the verdict.
Consult codebase-design for where a seam goes.

**One decision per merge.** Between any two merged tracers, at most one grilling
or research ticket closes. When that is spent and the way still looks foggy, the
next tracer is what clears it.

**Resolutions carry evidence.** A resolution says what ran, what came back, and
what that rules out. A number from the real dependency outranks a conclusion
reached about it.

**Proven work graduates off the map.** When a merged tracer has run end to end
through a chunk and the work left is repetition along that path, the chunk is no
longer fog: to-spec-with-evidence over what the tracers proved, to-tickets to
slice it, and those tickets fan out to subagents in their own worktrees. Record
the spec in Decisions so far. Shared understanding in a grilling graduates
nothing; a merged tracer does. The map keeps only what a slice still has to
prove.

**Skills.** grill-with-docs opens a tracer: the slice's design is settled there,
with the human, and tdd then drives it. Same skill for a question no slice can
settle. prototype where an artifact only has to be reacted to.
```
