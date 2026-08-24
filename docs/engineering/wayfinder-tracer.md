## What it does

`wayfinder-tracer` runs [wayfinder](https://aihero.dev/skills-wayfinder) for an effort whose destination is merged code rather than a [spec](https://www.aihero.dev/ai-coding-dictionary/spec): the same shared map on the same issue tracker, but its tickets are **tracers**, the simplest stupid thing that could possibly work, end to end, against the real dependency.

Charting stops at one ticket. Where wayfinder opens with a breadth-first sweep and writes everything it can see into **Not yet specified**, this creates the map with a single tracer and an empty fog section, and grows it only where a merged tracer has actually run into something. Foresight is not a licence to chart: a question earns a [ticket](https://www.aihero.dev/ai-coding-dictionary/ticket) once a slice has hit it, and not before.

## When to reach for it

You invoke this by typing `/wayfinder-tracer`; the [agent](https://www.aihero.dev/ai-coding-dictionary/agent) won't reach for it on its own.

Reach for it when the effort is genuinely bigger than one [session](https://www.aihero.dev/ai-coding-dictionary/session), which is wayfinder's own bar, *and* what you want at the end is working software rather than a document to hand off.

| What you have in front of you | What to run |
| --- | --- |
| A multi-session effort ending in a decision, a spec, or a plan to hand off | [wayfinder](https://aihero.dev/skills-wayfinder) |
| A multi-session effort ending in merged, working code | `/wayfinder-tracer` |
| A wayfinder map already charted, now front-loading design | `/wayfinder-tracer`, which has a retrofit mode for exactly this |
| A well-scoped feature you can settle in one sitting | [grill-with-docs](https://aihero.dev/skills-grill-with-docs), then [to-tickets](https://aihero.dev/skills-to-tickets) |
| A plan already settled, needing slicing into thin end-to-end tickets | [to-tickets](https://aihero.dev/skills-to-tickets), which already produces tracer-bullet tickets |

The line against `to-tickets` is worth holding. Both produce thin end-to-end slices, but `to-tickets` slices a plan you already have, while this one is for when you cannot yet write that plan and the slice is how you find out what it should say.

## Prerequisites

It does not restate wayfinder, it reads it. The `wayfinder` skill has to be installed alongside it, because the map format, ticket mechanics, frontier and claiming all come from that sibling `SKILL.md` unchanged. That also means it inherits wayfinder's own prerequisite: the tracker wiring laid down by [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills), including native blocking so the frontier renders in the tracker's UI.

## The tracer

A tracer is a fifth ticket type beside wayfinder's `research`, `prototype`, `grilling` and `task`. The first one is a **walking skeleton**: one slice touching every layer, hardcoding everything it isn't proving and skipping everything it isn't testing. Narrow and ugly is the point.

The ticket itself is a **question**, not a design. It says what the slice has to reach end to end and what evidence it has to bring back, and stops there. Which module it lands in, which library it leans on, how the code is arranged: all of that is settled by the session that picks the ticket up, grilling it against the code as it stands then rather than as it stood on the day the map was charted. So a tracer is settled with you and then built without you, where wayfinder's other ticket types sit on one side of that line or the other.

It resolves by **evidence**. The resolution comment says what ran, what came back, and what that rules out, because a number from the real dependency outranks a conclusion reached about it.

The distinction against [prototype](https://aihero.dev/skills-prototype) is ownership of the code afterwards. A prototype is throwaway code answering a design question; a tracer is kept code answering it. Reach for a prototype when an artifact only has to be reacted to, and a tracer when it has to run.

## The doctrine, and why it lives on the map

The standing rules are not kept in the skill. They are written into the map's `## Notes` as a **doctrine**, and wayfinder loads Notes at the start of every session, so a plain `/wayfinder` run months later still inherits them without anyone remembering this skill exists. The rules that do the work:

- **A tracer blocks the questions it answers.** The interface and the schema get read off two real callers rather than argued ahead of one. A question may only jump the queue where a wrong answer cannot be cheaply reverted, which is to say where the blast radius outlives the branch: money moved, data migrated, a contract published to someone else.
- **Decide at the last responsible moment.** Where a decision can wait, put a seam where it will land and leave it undecided, and record the seam rather than the verdict. [codebase-design](https://aihero.dev/skills-codebase-design) is the vocabulary for where that seam goes.
- **One decision per merge.** Between any two merged tracers, at most one grilling or research ticket closes. When that budget is spent and the way still looks foggy, the next tracer is what clears it.

## Graduating a chunk off the map

A map made of tracers never clears in one go. What happens instead is that a tracer merges and the work it leaves behind is repetition: the second and third caller, the other six endpoints, the remaining field mappings. That chunk has had a slice run through it end to end, so it is no longer fog, and it leaves the map for the normal build chain rather than earning more tracers of its own. In practice you notice it mid-grilling, when picking up one tracer starts generating work for slices other than its own.

The gate is a merged tracer, never agreement. Reaching shared understanding in a grilling graduates nothing, because understanding is what the map is full of already. Every ticket that leaves has to widen a path a tracer has walked; one that opens a new path is itself a tracer, and stays.

What leaves goes through [to-spec-with-evidence](https://aihero.dev/skills-to-spec-with-evidence) (so the decisions the tracers proved arrive carrying the runs that proved them) and then [to-tickets](https://aihero.dev/skills-to-tickets), fanned out one [subagent](https://www.aihero.dev/ai-coding-dictionary/subagent) per unblocked ticket. The map keeps a one-line pointer at the spec and nothing else about that chunk, so what remains on it is only what a slice still has to prove. It closes when nothing does.

## Common questions

This skill is new, so these are the questions it plainly invites rather than ones observed in the wild.

**Isn't a one-ticket frontier just a slower map?**
For a team, at first, yes, and the skill says so rather than hiding it. Nothing can run in parallel until the first slice merges, where a breadth-first chart hands several people work immediately. What you buy is that the second, third and fourth tickets are chosen against evidence instead of a guess, so the ones that turn out unnecessary are never charted at all. Questions surfaced by a merged tracer can run in parallel beside the next one, so the serial stretch is the opening, not the whole map.

**The map's Notes are written by the agent. Doesn't a doctrine that says "this map carries execution" just let it grant itself permission?**
That hazard is real and it has been reported against wayfinder itself, where an agent wrote an execution override into its own Notes and read it back in later sessions as its own licence. Two things differ here. The override arrives because a human typed a skill name, not because a mid-map agent decided it was warranted. And the doctrine constrains far more than it permits: it caps charting at one ticket, caps decisions at one per merge, and refuses a ticket to any question no slice has hit. An agent that installs it has given itself a shorter leash, not a longer one. It is still worth reading the Notes on any map you did not chart yourself.

**One tracer at a time sounds endless. Does the whole build really go through the map?**
No, and that is what graduation is for. Only work that is still fog stays on the map; the moment a merged tracer has proven a path, everything that merely repeats along it leaves through `to-spec-with-evidence` and `to-tickets` and gets built the normal way, in parallel. The map is a fog-clearing instrument, not a project plan, so it should be shrinking while the work is still going on.

**What happens to a map I already charted the normal way?**
Retrofit mode installs the doctrine, charts the tracer that would settle the most open questions, and wires those questions to block on it. Closed tickets stay closed, because the map records the route actually walked and a decision made early is still a decision made. The existing **Not yet specified** section stays where it is but goes inert: recorded thinking rather than a backlog, and nothing in it becomes a ticket until a merged tracer reaches it.

## It's working if

- The freshly charted map has exactly one open child, and **Not yet specified** is empty.
- Every question ticket on the map names the tracer that surfaced it. A ticket that cannot name one was charted from foresight.
- Something is merged and running before the interface is settled, and the interface argument happens with two real callers in front of you.
- Resolution comments read like evidence (what ran, what came back) rather than like conclusions.
- **Not yet specified** grows and shrinks as slices land, instead of being longest on the day the map was created.
- Chunks leave the map for the build chain as tracers prove them, so the map gets smaller in the middle of the effort rather than only at the end.

## Where it fits

A variant on-ramp: it sits exactly where [wayfinder](https://aihero.dev/skills-wayfinder) sits, for the same too-big-for-one-session efforts, and differs only in what the map is made of. It does not replace wayfinder, it reads it, so the two are installed together.

Its neighbours are [grill-with-docs](https://aihero.dev/skills-grill-with-docs), which opens each tracer by settling its design with you, [tdd](https://aihero.dev/skills-tdd), which then drives it to green, and [to-tickets](https://aihero.dev/skills-to-tickets), which produces the same thin slices once the plan is already known. Where a cleared wayfinder map hands off once, to [to-spec](https://aihero.dev/skills-to-spec), a tracer map hands off repeatedly and a chunk at a time, through [to-spec-with-evidence](https://aihero.dev/skills-to-spec-with-evidence). For the whole set, [ask-matt](https://aihero.dev/skills-ask-matt) routes.
