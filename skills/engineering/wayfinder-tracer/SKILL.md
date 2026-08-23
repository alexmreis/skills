---
name: wayfinder-tracer
description: "Wayfinder, but the map starts as one stupid slice that works and grows only where a merged tracer actually hits fog."
disable-model-invocation: true
---

Wayfinder charts a way made of **decision tickets**, surveyed **breadth-first** across the whole space. This charts one made of **tracers**, followed **depth-first** down a single thread: the simplest stupid thing that could possibly work, merged, and then the next one.

Two inversions. What clears fog is a slice that ran, not a conclusion that was reasoned. And what gets charted is that one slice, never the space of unknowns, however clearly you can already see it. Seeing an unknown is not the same as needing it charted, and a map you could survey up front was never foggy enough to need one.

Read the sibling `wayfinder/SKILL.md` first. Map format, ticket mechanics, frontier, HITL/AFK and the two invocation modes all come from there unchanged. This skill overrides ticket types, how much gets charted, and what goes in **Notes**.

## The tracer ticket

A fifth `wayfinder:<type>`, alongside `research`, `prototype`, `grilling`, `task`:

- **Tracer** (AFK): the simplest, stupidest thing that could possibly work, end to end, against the real dependency, merged. The first one is a **walking skeleton**: a single slice touching every layer, hardcoding everything it isn't proving and skipping everything it isn't testing. Narrow and ugly is the point. It resolves by **evidence**: what ran, what came back, what that rules out.

Where `prototype` is throwaway code answering a design question, a tracer is **kept** code answering it. Reach for prototype when an artifact only has to be reacted to; reach for tracer when it has to run.

## Chart

Follow wayfinder's **Chart the map**, replacing two of its steps by name.

1. **Name the destination in a sentence**: a change, merged, exercised against the real dependency. Grill only as far as that sentence needs. The destination fixes scope; it isn't a design.
2. Instead of **Map the frontier**, **find the first tracer, depth-first.** Rather than fanning out, put one question to the effort: *what is the stupidest thing that could run end to end and teach us something?* Follow that single thread until you can state the slice in a sentence, then stop asking. The rest of the space gets charted by the tracers that hit it, not by this conversation.
3. **Create the map** with the destination, the doctrine in `## Notes`, and **Decisions so far and Not yet specified both empty**. `## Out of scope` may carry what the destination consciously rules out, since narrowing is not surveying.
4. Instead of **Create the tickets you can specify now**, **create one tracer ticket.** There are no blocking edges to wire, because there is nothing yet to wire it to. Wayfinder's research-subagent step then has nothing to fire, since a first tracer creates no research tickets.

**Done when** the map has exactly one open child, that child is a tracer, and Not yet specified is empty.

The cost is real: a one-ticket frontier gives concurrent sessions nothing to parallelise until the first slice merges. That is the trade, scope bought with evidence rather than foresight.

## Retrofit a charted map

Given an existing map, in one session:

1. Install the doctrine into its `## Notes`.
2. Chart the tracer that would settle the most open questions at once, and wire those questions to block on it.
3. Leave `## Not yet specified` untouched but **inert**: it is now recorded thinking, not a backlog. Nothing in it becomes a ticket until a merged tracer reaches it.
4. Closed tickets stay closed. The map records the route walked, and a decision made early is still a decision made.

**Done when** the first frontier ticket is a tracer, and every open question is either blocked on one or names why it outranks one.

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

**Skills.** tdd drives tracers. prototype where an artifact only has to be
reacted to. grilling and domain-modeling for what no slice can settle.
```
